I'll rework the entire document to keep every technical detail from the original, but wrap it in beginner-friendly explanations, definitions, and a progressive teaching style. Even someone completely new to Docker can follow along, while experienced engineers can still use it as a production reference.

Below is the full `Docker.md` file you can download or copy.

```markdown
# Docker for MLOps & AI Engineers  
**From Beginner to 3 Years of Experience**  
*Learn containerisation step by step – then master GPU training, model serving, and production pipelines.*

---

## Table of Contents
1. [What Is Docker and Why Do We Need It?](#what-is-docker-and-why-do-we-need-it)
2. [Docker Fundamentals – The Building Blocks](#docker-fundamentals--the-building-blocks)
3. [GPU & CUDA – Running ML on Graphics Cards](#gpu--cuda--running-ml-on-graphics-cards)
4. [Dockerfile Best Practices – Writing Clean, Efficient Images](#dockerfile-best-practices-for-machine-learning)
5. [Multi‑Stage Builds – Slim Images for Training & Inference](#multi‑stage-builds-for-training--inference)
6. [Reproducibility by Design – Freezing Your Environment](#reproducibility-by-design)
7. [Efficient Image Building & Caching – Speed Up Your Workflow](#efficient-image-building--caching)
8. [Docker Compose – Connecting Multiple Services](#docker-compose-for-end-to-end-ml-pipelines)
9. [Serving Models in Production – APIs and Inference Servers](#serving-models-in-production)
10. [Orchestration & Scaling – Going Big with Kubernetes](#orchestration--scaling)
11. [Logging, Monitoring & Health Checks](#observability-logging--health-checks)
12. [Security & Secrets Management](#security--secrets-management)
13. [CI/CD for ML Containers – Automating Builds and Tests](#cicd-for-ml-containers)
14. [Sample Project Structure – A Real‑World Layout](#sample-project-structure)
15. [Common Pitfalls & Solutions – Don’t Make These Mistakes](#common-pitfalls--solutions)
16. [Tooling & Ecosystem – Helpful Apps Around Docker](#tooling--ecosystem)
17. [Appendix: Quick Command Reference](#appendix-quick-reference)

---

## What Is Docker and Why Do We Need It?

Imagine you want to run a machine learning model on your laptop, your friend’s computer, and a cloud server. Each machine has a different operating system, different Python versions, and different libraries. The model might work on your laptop but crash on the server with a weird error.  

**Docker solves this problem.** It packages your code, your dependencies, and even the operating system libraries into a single unit called a **container**. A container is like a lightweight virtual machine – it runs exactly the same everywhere.  

For MLOps, Docker makes it possible to:

- Train a model on a GPU server and move it to a CPU‑only edge device without changing anything.
- Run four different Python versions for four different projects on the same machine.
- Ship a model to a colleague along with the exact libraries it needs.
- Deploy a model behind a web API that can serve millions of requests.

In short: **“It works on my machine” becomes “It works in a Docker container.”**

---

## Docker Fundamentals – The Building Blocks

You’ll hear these words constantly. They are your basic toolbox.

| Concept | What it means | ML example |
|--------|----------------|-------------|
| **Image** | A frozen snapshot of your entire environment: operating system base, Python, packages, your code, and sometimes the model itself. It’s like a blueprint. | `pytorch/pytorch:2.1.0-cuda12.1-cudnn8-runtime` |
| **Container** | A **running instance** of an image. You can start many containers from the same image, just like you can print many copies of a PDF. | One container for training, three containers for serving. |
| **Dockerfile** | A text file where you write the recipe for building an image. Each line is a step (install packages, copy code, set environment variables). | You’ll write `Dockerfile.train` and `Dockerfile.serve`. |
| **Volume / Bind Mount** | A way to connect a folder on your computer (host) to a folder inside the container. Data written inside the container can appear on your host, and vice versa. | Point your container to `/data/imagenet` on your host so it can read your dataset. |
| **Network** | Containers can talk to each other via virtual networks. You can give services names like `mlflow` or `database` and they’ll find each other. | A training container logs metrics to a running `mlflow` container. |
| **BuildKit** | The modern Docker build engine. It’s faster and supports advanced features like caching downloads, injecting secrets, and parallel builds. | You’ll enable it with `DOCKER_BUILDKIT=1`. |

### Your First Docker Commands

Open a terminal and try these:

```bash
# Build an image from a Dockerfile in the current folder
docker build -t my-first-image .

# Run a container from that image, open an interactive shell, then remove it when you exit
docker run -it --rm my-first-image bash

# If you have a GPU, start a container that can see it
docker run --gpus all -it --rm my-image nvidia-smi
```

> **Tip:** Always use `DOCKER_BUILDKIT=1` for faster, smarter builds. It’s the default in Docker Desktop and newer versions.

---

## GPU & CUDA – Running ML on Graphics Cards

### Why GPUs?
Training neural networks on a CPU can take weeks. A **GPU** (Graphics Processing Unit) has thousands of tiny cores that do matrix math very quickly. **CUDA** is NVIDIA’s software that lets programs use the GPU.

### How Docker Talks to the GPU

Docker itself cannot use a GPU – it needs a helper called the **NVIDIA Container Toolkit**. When you install it on your host machine, Docker can pass your physical GPU into the container.

**Inside the container**, the CUDA libraries must **match the version of the driver** on your host. Think of it like this:  
`Host GPU driver` (e.g., version 525) → `nvidia-container-toolkit` → `Container with CUDA 12.1`

If the versions don’t match, the container will crash with “CUDA error: no device found”.

### Choosing a Base Image

A **base image** is the starting point of your Dockerfile. For GPU workloads you have three common choices:

1. **NVIDIA official images** (`nvidia/cuda:12.1-cudnn8-runtime-ubuntu22.04`)  
   - Only CUDA and cuDNN; you add Python yourself. Maximum control.  
   - Use `runtime` for inference, `devel` if you need to compile custom CUDA code.

2. **Framework images** (`pytorch/pytorch:2.1.0-cuda12.1-cudnn8-runtime`)  
   - Come with PyTorch/TensorFlow, Python, and CUDA. Good for fast starts but harder to customise.

3. **Build your own** – start from a minimal Linux image and install everything. Best for production.

### Enabling GPU in Your Container

- Command line: `docker run --gpus all` gives the container access to all GPUs.
- Docker Compose: see the example in section 8.

Check inside the container:
```bash
docker run --gpus all --rm nvidia/cuda:12.1-base-ubuntu22.04 nvidia-smi
```

### Compatibility – A Must-Read

- The **major CUDA version** must be supported by your host driver.
- Use the [CUDA compatibility table](https://docs.nvidia.com/deploy/cuda-compatibility/) to pick the right image.
- To lock a specific version forever, use a **digest**: `pytorch/pytorch@sha256:abc123...` instead of a floating tag like `latest`.

---

## Dockerfile Best Practices for Machine Learning

A Dockerfile is a recipe. Small mistakes can make your image huge, slow, or insecure. Follow these rules from day one.

### 1. Layer Order Matters – Put Unchanging Stuff First

Every line in a Dockerfile creates a new **layer**. Docker caches layers. If you change your code, Docker can reuse the layers from earlier steps (like installing Python) and only rebuild from the line where you copy your new code.

**Bad (code copied early, so every code change re‑runs pip install):**
```dockerfile
COPY src/ /app/src/
RUN pip install -r requirements.txt
```

**Good (dependencies installed first, cached):**
```dockerfile
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY src/ /app/src/
```

### 2. Use BuildKit Cache Mounts

When you run `pip install`, Docker normally downloads packages every time you rebuild. That’s slow. **Cache mounts** save your `~/.cache/pip` folder on the host and reuse it across builds.

```dockerfile
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install --no-cache-dir -r requirements.txt
```

### 3. Combine RUN Commands and Clean Up

Each `RUN` creates a new layer. To save space, chain commands with `&&` and remove temporary files in the **same** RUN line.

```dockerfile
RUN apt-get update && apt-get install -y \
    package1 package2 \
    && rm -rf /var/lib/apt/lists/*
```

### 4. Use ENTRYPOINT and CMD Correctly

- `ENTRYPOINT` is the main program that will always run.
- `CMD` gives default arguments that can be overridden at runtime.

```dockerfile
ENTRYPOINT ["python", "train.py"]
CMD ["--epochs", "10"]
```

### 5. Never Run as Root Inside the Container

Create a normal user for security:

```dockerfile
RUN groupadd -r mluser && useradd -r -g mluser mluser
USER mluser
```

If you need GPU access, the NVIDIA runtime normally handles device permissions automatically.

### 6. Set Useful Environment Variables

```dockerfile
ENV PYTHONUNBUFFERED=1   # See logs immediately, don't buffer them
ENV NVIDIA_VISIBLE_DEVICES=all
```

---

## Multi‑Stage Builds – Slim Images for Training & Inference

### The Problem
You build a training image that includes CUDA compilers, headers, and large build tools. But after training, you only need the lightweight runtime libraries to run inference. Carrying all that extra baggage makes your production image huge and less secure.

### The Solution: Multi‑Stage Builds

You write **two FROM lines** in one Dockerfile:

```dockerfile
# ---- Build Stage (heavy, with compilers) ----
FROM nvidia/cuda:12.1-cudnn8-devel-ubuntu22.04 AS builder
RUN apt-get install -y build-essential python3-pip
COPY requirements-build.txt .
RUN pip install -r requirements-build.txt
# Compile a custom C++ extension
RUN cd /src/custom_ops && make

# ---- Production Stage (lightweight, only runtime) ----
FROM nvidia/cuda:12.1-cudnn8-runtime-ubuntu22.04 AS production
# Copy only the compiled library and the runtime dependencies
COPY --from=builder /src/custom_ops/*.so /app/custom_ops/
COPY requirements-runtime.txt .
RUN pip install -r requirements-runtime.txt
COPY api/ /app/
CMD ["uvicorn", "api.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

Now the final image has no compilers, no development headers, and is often half the size.

---

## Reproducibility by Design

Reproducibility means that a year from now, you can rebuild the exact same container and get the same model behaviour. This is critical for science, debugging, and audits.

### Pin Everything

- **Base image digest:** `FROM python:3.10-slim@sha256:abc123...` instead of `python:3.10-slim`. Digests never change.
- **Python packages:** Use `requirements.txt` with exact versions (`numpy==1.25.2`), not ranges.
- **System libraries:** Pin versions when possible.

### Tools for Locking Dependencies

- **pip-tools:** generate a locked `requirements.txt` from a loose `requirements.in`.
- **conda-lock:** lock an `environment.yml` for a specific platform.

Then install from the locked file inside your Dockerfile.

### Verify Your Environment at Startup

Add a small script that checks library versions and fails early if something is wrong:

```dockerfile
COPY verify_environment.py /app/
RUN python /app/verify_environment.py
```

---

## Efficient Image Building & Caching

Building images can be slow, especially in CI/CD pipelines. Here’s how to speed it up.

- **Always use BuildKit** (`DOCKER_BUILDKIT=1`).
- **Use a registry cache.** Docker saves your build layers to a remote registry, then reuses them in future builds.
- **Separate source code copy.** First copy files that list dependencies (like `requirements.txt`), install them, then copy the rest of the code. This way, changing one line of Python doesn’t invalidate the pip cache.

### Docker Buildx Command with Cache

```bash
docker buildx build \
  --cache-from=type=registry,ref=myregistry.com/cache:ml \
  --cache-to=type=registry,ref=myregistry.com/cache:ml,mode=max \
  -t myapp:latest .
```

`--cache-from` pulls old layers, `--cache-to` pushes new ones. Now your CI builds are fast.

---

## Docker Compose – Connecting Multiple Services

### What Is Docker Compose?
It lets you define multiple containers (services) in a single YAML file and start them all with one command: `docker compose up`.  
For ML, you often need several things running together: a training job, a model server, a metrics tracker (MLflow), and a database.

### Example: A Local Training Stack

**docker-compose.yml**
```yaml
services:
  trainer:
    image: myproject:train
    build:
      context: .
      dockerfile: Dockerfile.train
    # Give it a GPU
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: 1
              capabilities: [gpu]
    volumes:
      - ./data:/data          # Mount dataset
      - ./models:/models      # Save trained model
    environment:
      - MLFLOW_TRACKING_URI=http://mlflow:5000
    command: ["python", "train.py", "--data-dir", "/data", "--output", "/models"]
    depends_on:
      - mlflow

  serving:
    image: myproject:serve
    ports:
      - "8000:8000"
    volumes:
      - ./models:/models
    environment:
      - MODEL_PATH=/models/latest

  mlflow:
    image: ghcr.io/mlflow/mlflow:v2.7.1
    command: mlflow server --host 0.0.0.0 --port 5000
    ports:
      - "5000:5000"
```

Run `docker compose up` and your trainer starts, logs metrics to MLflow, and the serving container loads the trained model.

---

## Serving Models in Production

Once your model is trained, you need to make it available to other applications – usually through a REST API.

### Popular Serving Solutions (from simple to advanced)

| Tool | What it does | Why use it |
|------|--------------|------------|
| **FastAPI + Uvicorn** | Write a Python web server with endpoints like `/predict`. | Full control, easy to customise. |
| **TensorFlow Serving** | A dedicated server for TensorFlow models. Loads models from disk automatically. | High performance, versioning. |
| **Triton Inference Server** (NVIDIA) | Supports PyTorch, TensorFlow, ONNX, and more. Can batch requests for better GPU utilisation. | Enterprise‑grade, dynamic batching. |
| **BentoML** | Packages your model and auto‑generates a REST API. | Simple packaging, less boilerplate. |
| **Ray Serve** | Scales your API across a cluster. | Advanced autoscaling. |

### A Minimal FastAPI Dockerfile

```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY model model/
COPY api/ .
EXPOSE 8000
HEALTHCHECK --interval=30s CMD python -c "import requests; requests.get('http://localhost:8000/health')"
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

Inside `api/main.py`, you load the model **once when the server starts** and reuse it for every request.

### Using TensorFlow Serving (No Code)

```bash
docker run -p 8501:8501 \
  -v /path/to/my_model:/models/my_model \
  -e MODEL_NAME=my_model \
  tensorflow/serving
```

Now your API is at `http://localhost:8501/v1/models/my_model:predict`.

---

## Orchestration & Scaling

When you need to run containers on 50 machines, Docker Compose isn’t enough. You need an **orchestrator**.

- **Kubernetes** is the industry standard. It schedules containers across a cluster, restarts them when they fail, and scales them up/down.
- **Kubeflow Pipelines** is built on Kubernetes and turns ML steps into container jobs.
- Cloud services like **AWS SageMaker**, **Vertex AI**, and **Azure ML** also run your Docker images, but they provide managed infrastructure.

**Key patterns for scaling ML:**
- **Init containers:** Run before the main container, download models from cloud storage.
- **Sidecar containers:** Run alongside your app to collect logs or metrics.
- **Ephemeral volumes:** Shared memory (`/dev/shm`) often needed by PyTorch DataLoader.

---

## Logging, Monitoring & Health Checks

In production, you need to know if your model server is alive, and if it’s returning errors.

- **Health checks:** Docker can periodically run a command to see if your app is healthy. If it fails, the container is restarted.
```dockerfile
HEALTHCHECK --interval=15s --timeout=5s --retries=3 \
  CMD curl --fail http://localhost:8000/health || exit 1
```
- **Logs must go to `stdout` / `stderr`.** Docker captures them, and you can forward them to tools like Elasticsearch.
- **GPU metrics:** Use `nvidia-dcgm-exporter` as a sidecar to expose GPU temperature, utilisation, and memory.
- **Prometheus** is the standard for collecting metrics; your server can expose a `/metrics` endpoint.

---

## Security & Secrets Management

- **Never put passwords or API keys in your Dockerfile.** It will be stored forever in the image history.
- Use **Docker secrets** (Swarm mode) or **Kubernetes secrets** to inject sensitive values safely.
- For private pip repositories, pass a netrc file using BuildKit’s `--secret`:
```dockerfile
RUN --mount=type=secret,id=netrc,target=/root/.netrc \
    pip install --extra-index-url ... my-private-package
```
- **Scan images for vulnerabilities** using `docker scout`, Trivy, or Snyk.
- Run containers as a non‑root user and consider a read‑only filesystem (`--read-only`).

---

## CI/CD for ML Containers

CI/CD (Continuous Integration / Continuous Delivery) means that every time you push code, a pipeline builds, tests, and possibly deploys your container.

A typical pipeline:

1. **Lint** – check the Dockerfile for mistakes (Hadolint).
2. **Build** – create the image with caching.
3. **Unit tests** – run inside the built container (`docker run ... pytest`).
4. **Integration tests** – bring up a mini‑stack with Docker Compose, train for a few steps, and test the serving endpoint.
5. **Vulnerability scan.**
6. **Push** the image to a registry with a version tag.
7. **Deploy** to staging or production.

Example GitHub Actions snippet:
```yaml
- name: Build and push
  uses: docker/build-push-action@v5
  with:
    context: .
    push: true
    tags: registry/repo:latest,registry/repo:${{ github.sha }}
    cache-from: type=registry,ref=registry/repo:buildcache
    cache-to: type=registry,ref=registry/repo:buildcache,mode=max
```

---

## Sample Project Structure

Here is how a professional ML project organises its files:

```
ml-project/
├── Dockerfile.train          # Image for training
├── Dockerfile.serve           # Image for serving
├── docker-compose.yml         # Local integration stack
├── .dockerignore              # Files NOT copied into the image
├── requirements/
│   ├── requirements.in        # Loose versions
│   ├── requirements.txt       # Locked
│   └── requirements-dev.txt   # Testing/linting tools
├── configs/
│   └── training_config.yaml
├── src/
│   ├── data/
│   ├── models/
│   └── train.py
├── api/                       # Serving app
│   ├── main.py
│   └── requirements.txt
├── scripts/
│   ├── entrypoint_train.sh
│   └── download_weights.sh
└── tests/
    └── test_inference.py
```

**The `.dockerignore` file is crucial.** It prevents large files (like datasets, model checkpoints, and Python caches) from being accidentally copied into the image, which would make it massive:

```
data
models
.git
__pycache__
*.pyc
.env
venv
```

---

## Common Pitfalls & Solutions

| Pitfall | What happens | How to fix it |
|--------|--------------|----------------|
| CUDA version mismatch | `CUDA error: no CUDA‑capable device` | Use a base image compatible with your host driver; check with `nvidia-smi`. |
| Image too big | 15 GB + | Multi‑stage builds, slim base images, don’t bake model weights inside. |
| Slow pip install every build | Re‑downloads packages | Use BuildKit pip cache mount. |
| PyTorch DataLoader freezes | Container hangs during training | Increase shared memory with `--shm-size=2g` or mount a `tmpfs`. |
| Permission denied on mounted data | User ID inside container doesn’t match host | Run container with the same UID: `docker run -u $(id -u)`. |
| Model disappears after restart | Not saved to mounted volume | Ensure your output path is a mounted volume or a named volume. |
| Container crashes silently | No logs | Set `PYTHONUNBUFFERED=1` and use an init process (`--init`). |
| Zombie processes | Defunct processes stay alive | Use `docker run --init` or add `tini` to your image. |

---

## Tooling & Ecosystem

Here are tools that make Docker life easier for ML:

- **nvidia-container-toolkit** – the bridge between Docker and your GPU.
- **buildx** – the modern Docker build engine (cache, secrets, multi‑platform).
- **Docker Compose** – local multi‑service orchestration.
- **dive** – inspect your image layers to see where space is wasted.
- **Hadolint** – lint your Dockerfiles.
- **Trivy / Grype** – scan images for known vulnerabilities.
- **Kaniko / Buildah** – build Docker images inside Kubernetes without needing a Docker daemon.

---

## Appendix: Quick Command Reference

### Dockerfile GPU Template (Start Here)

```dockerfile
FROM nvidia/cuda:12.1-cudnn8-runtime-ubuntu22.04
ENV DEBIAN_FRONTEND=noninteractive
ENV PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3.10 python3-pip \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY requirements.txt .
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install --no-cache-dir -r requirements.txt

COPY src/ src/
ENTRYPOINT ["python", "-m", "train"]
CMD ["--help"]
```

### Run Training with All GPUs

```bash
docker run --gpus all --shm-size=2g -v /mnt/data:/data mytrainer:latest
```

### Docker Compose GPU Service

```yaml
services:
  app:
    image: mygpuimage
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
```

### Check GPU from Inside Container

```bash
docker run --gpus all --rm myimage nvidia-smi
```

### Healthcheck Example

```dockerfile
HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD python -c "import requests; requests.get('http://localhost:8000/health')" || exit 1
```

---

*This documentation grows with you. Start with the basics, then come back when you need GPU orchestration or CI/CD pipelines. Docker is the foundation of reproducible, scalable ML. You’ve got this.*
```

---
---

# Docker for MLOps & AI Engineers

**Audience:** ML engineers, AI developers, and MLOps practitioners with ~3 years of experience.  
**Focus:** Production-grade containerisation for model training, inference, and pipeline orchestration.

---

## Table of Contents
1. [Why Docker in MLOps](#why-docker-in-mlops)
2. [Docker Fundamentals Refresher](#docker-fundamentals-refresher)
3. [GPU & CUDA Support](##gpu--cuda-support)
4. [Dockerfile Best Practices for Machine Learning](#dockerfile-best-practices-for-machine-learning)
5. [Multi-Stage Builds for Training & Inference](#multi-stage-builds-for-training--inference)
6. [Reproducibility by Design](#reproducibility-by-design)
7. [Efficient Image Building & Caching](#efficient-image-building--caching)
8. [Docker Compose for End-to-End ML Pipelines](#docker-compose-for-end-to-end-ml-pipelines)
9. [Serving Models in Production](#serving-models-in-production)
10. [Orchestration & Scaling](#orchestration--scaling)
11. [Observability, Logging & Health Checks](#observability-logging--health-checks)
12. [Security & Secrets Management](#security--secrets-management)
13. [CI/CD for ML Containers](#cicd-for-ml-containers)
14. [Sample Project Structure](#sample-project-structure)
15. [Common Pitfalls & Solutions](#common-pitfalls--solutions)
16. [Tooling & Ecosystem](#tooling--ecosystem)
17. [Appendix: Quick Reference](#appendix-quick-reference)

---

## Why Docker in MLOps

- **Environment Parity:** Same kernel, libraries, and drivers from development to production.
- **Portability:** Move workloads between cloud, on-prem, and hybrid Kubernetes clusters.
- **Resource Efficiency:** Avoid per-model VMs; co-locate inference services.
- **GPU Scheduling:** Isolate CUDA versions, control GPU visibility.
- **Reproducibility:** Ship frozen environments for audits, A/B testing, and rollbacks.
- **Microservice Integration:** Train, serve, preprocess, and monitor as separate services.

The days of "it works on my machine" end here. Docker is the unit of delivery for ML code, models, and dependencies.

---

## Docker Fundamentals Refresher

*Skip if you’re already comfortable. These are the concepts most frequently hit in ML pipelines.*

| Concept | ML-specific context |
|--------|----------------------|
| **Image** | Frozen stack: OS + CUDA + Python + libs + code + model weights |
| **Container** | Running instance of an image; one container per training job or serving replica |
| **Dockerfile** | Declarative recipe; ensure layers are cache-friendly |
| **Volume/Bind Mount** | Inject datasets, code (for development), or output model artifacts without rebuilding |
| **Network** | Connect preprocessing, training, and serving containers |
| **BuildKit** | Enables `--mount=type=cache` for pip/conda caches, secrets, and parallel builds |

### Essential Commands (ML usage)

```bash
# Build with GPU driver compatibility
DOCKER_BUILDKIT=1 docker build -t project:train .

# Run interactive shell in a fresh container, with GPU
docker run --gpus all -it --rm project:train bash

# Mount a local dataset and write model back to host
docker run --gpus all -v /data/imagenet:/data -v $PWD/models:/models project:train \
    python train.py --data-dir /data --output /models

# Show GPU usage in container
nvidia-smi  # (only if NVIDIA runtime is installed)
```

Always use `DOCKER_BUILDKIT=1` for modern builds; it’s the default in recent Docker versions.

---

## GPU & CUDA Support

### Choosing a Base Image

- **NVIDIA Official Images** (`nvidia/cuda:12.1-cudnn8-runtime-ubuntu22.04`)  
  Provide CUDA libraries, cuDNN. Use `runtime` for inference, `devel` for building custom CUDA kernels.
- **PyTorch & TensorFlow GPU images** are available on Docker Hub (e.g., `pytorch/pytorch:2.1.0-cuda12.1-cudnn8-runtime`). They are convenient but watch for version conflicts.
- **Build your own** when you need tight control over dependency versions.

### Enabling GPU Access

- Install `nvidia-container-toolkit` on the host.
- Use `--gpus all` or `--gpus '"device=0,1"'` to expose specific GPUs to the container.
- Inside the container, the NVIDIA driver (mounted by the runtime) must match the host’s driver version. Compatibility matrix: [NVIDIA Container Toolkit docs](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html).

### CUDA Compatibility

- **Major versions must match.** If host driver is 525, your base image’s CUDA version should be compatible with that driver.
- Use `nvidia-smi` to check host driver and refer to the [CUDA compatibility table](https://docs.nvidia.com/deploy/cuda-compatibility/).
- Pro-tip: Pin a known-good combination in your `docker-compose.yml` and lockbase image digests (e.g., `pytorch/pytorch@sha256:...`).

---

## Dockerfile Best Practices for Machine Learning

### 1. Order Layers for Caching

Place infrequently changed instructions early:

```dockerfile
FROM nvidia/cuda:12.1-cudnn8-runtime-ubuntu22.04

# System dependencies (rarely change)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libgl1-mesa-glx \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Python version
RUN apt-get update && apt-get install -y python3.10 python3-pip \
    && rm -rf /var/lib/apt/lists/*

# pip / conda installs – cache via BuildKit mount
COPY requirements.txt .
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install --no-cache-dir -r requirements.txt

# Copy code (changes most often)
COPY src/ /app/src/
COPY configs/ /app/configs/

WORKDIR /app
```

### 2. Use BuildKit Cache Mounts

For `pip`, `apt`, and `conda`, mount cache directories to speed up repeated builds:

```dockerfile
RUN --mount=type=cache,target=/var/cache/apt \
    --mount=type=cache,target=/root/.cache/pip \
    apt-get update && apt-get install ... && pip install ...
```

### 3. Combine RUN Commands & Clean Up

Reduce layer count and remove temporary files in the same `RUN`:

```dockerfile
RUN apt-get update && apt-get install -y \
    package1 \
    package2 \
    && rm -rf /var/lib/apt/lists/*
```

### 4. Entrypoint & CMD

- Use `ENTRYPOINT` for the main binary (e.g., `["python", "-m", "train"]`).
- Use `CMD` for default arguments, easily overridden at runtime.

### 5. Non‑root User

Improve security; avoid running training jobs as root.

```dockerfile
RUN groupadd -r mluser && useradd -r -g mluser mluser
USER mluser
```

For GPU devices, the user must have access to `/dev/nvidia*`. Using the NVIDIA runtime, this is typically handled automatically. If not, ensure the user is added to the `video` group (inside the container).

### 6. Environment Variables

- `PYTHONUNBUFFERED=1` – prevents Python output buffering (essential for log streaming).
- `NVIDIA_VISIBLE_DEVICES=all` – commonly set by the runtime.

---

## Multi-Stage Builds for Training & Inference

Separate heavy build-time dependencies from the final image.

### Example: Training Image with Custom CUDA Kernel, Lightweight Inference

```dockerfile
# ---- Build Stage ----
FROM nvidia/cuda:12.1-cudnn8-devel-ubuntu22.04 AS builder
RUN --mount=type=cache,target=/var/cache/apt \
    apt-get update && apt-get install -y python3.10 python3-pip
COPY requirements-build.txt .
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install --user -r requirements-build.txt
COPY src/ /src
# Compile custom op or Cython extension
RUN cd /src/custom_ops && make

# ---- Inference / Production Stage ----
FROM nvidia/cuda:12.1-cudnn8-runtime-ubuntu22.04 AS production
COPY --from=builder /root/.local /root/.local
COPY --from=builder /src/custom_ops/*.so /app/custom_ops/
COPY requirements-runtime.txt .
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install --no-cache-dir -r requirements-runtime.txt
COPY model/ /app/model/
COPY api/ /app/
ENV PATH=/root/.local/bin:$PATH
CMD ["uvicorn", "api.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

Multi-stage reduces image size, removes compilers and headers from production, and accelerates vulnerability scanning.

---

## Reproducibility by Design

### Pin Everything

- **Base image digest** (not just tag): `FROM python:3.10-slim@sha256:abc123...`
- **Python dependencies:** Exact versions in `requirements.txt`, `pyproject.toml`, or `environment.yml`.
- **System packages:** Pin versions where possible.
- **Model weights:** Reference by content hash (SHA256) in the Dockerfile or download at runtime with checksum validation.

### Use Conda‑lock or Pip‑tools

Generate a fully resolved environment:

```bash
pip-compile requirements.in   # → requirements.txt
conda-lock -f environment.yml -p linux-64  # → conda-linux-64.lock
```

Then install from the lock file inside the image.

### Environment Validation

Add a script that checks imported library versions against a manifest and fails fast on mismatch. Embed it in the `HEALTHCHECK` or at entrypoint.

```dockerfile
COPY verify_environment.py /app/
RUN python /app/verify_environment.py
```

---

## Efficient Image Building & Caching

- **BuildKit** is non‑negotiable. Set `DOCKER_BUILDKIT=1`.
- Use `--cache-from` and `--cache-to` with registry cache to reuse layers across CI/CD.
- Organise source code to avoid cache invalidation:
  - Copy only what’s needed: `COPY pyproject.toml poetry.lock ./` then `COPY src/ src/`.
- For large models, don’t bake them into the image; download at container startup or mount from a volume. Exception: small ONNX/TensorRT models (under 100MB) can be baked.

### Docker Build CLI Example

```bash
docker buildx build \
  --cache-from=type=registry,ref=myregistry.com/cache:ml \
  --cache-to=type=registry,ref=myregistry.com/cache:ml,mode=max \
  -t myapp:latest .
```

---

## Docker Compose for End-to-End ML Pipelines

Docker Compose is ideal for local development and integration testing of multi-service ML systems.

### Typical Services

- **Data preprocessing** (one-off or daemon)
- **Training job** (scheduled or triggered)
- **Model serving** (REST/gRPC)
- **Monitoring stack** (Prometheus, Grafana)
- **Feature store** (Redis)

### Example `docker-compose.yml` for a Training Pipeline

```yaml
services:
  trainer:
    image: myproject:train
    build:
      context: .
      dockerfile: Dockerfile.train
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: 1
              capabilities: [gpu]
    volumes:
      - ./data:/data
      - ./models:/models
      - ./configs:/app/configs
    environment:
      - MLFLOW_TRACKING_URI=http://mlflow:5000
    command: ["python", "/app/train.py", "--data-dir", "/data", "--output", "/models"]
    depends_on:
      - mlflow

  serving:
    image: myproject:serve
    build:
      dockerfile: Dockerfile.serve
    ports:
      - "8000:8000"
    volumes:
      - ./models:/models
    environment:
      - MODEL_PATH=/models/latest
    deploy:
      replicas: 2

  mlflow:
    image: ghcr.io/mlflow/mlflow:v2.7.1
    command: mlflow server --host 0.0.0.0 --port 5000
    ports:
      - "5000:5000"
    volumes:
      - mlflow_artifacts:/mlflow

volumes:
  mlflow_artifacts:
```

For GPU services, ensure the `nvidia` device driver is specified as shown.

---

## Serving Models in Production

### Options at a Glance

| Tool | Docker integration | Pros |
|------|-------------------|------|
| **FastAPI + Uvicorn** | Custom Dockerfile | Maximum flexibility, Python-native |
| **TensorFlow Serving** | Official image `tensorflow/serving` | High performance, versioned model loading |
| **Triton Inference Server** | `nvcr.io/nvidia/tritonserver` | Multi‑framework, dynamic batching, GPU metrics |
| **BentoML** | One‑command build | Packaging, API docs, adapters |
| **Ray Serve** | Ray cluster in containers | Advanced orchestration, autoscaling |

### FastAPI Example Dockerfile (Inference)

```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY model model/
COPY api/ .
EXPOSE 8000
HEALTHCHECK --interval=30s CMD python -c "import requests; requests.get('http://localhost:8000/health')"
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--workers", "2"]
```

Model loading strategy:
- Load model once during server startup (FastAPI `@app.on_event("startup")`).
- For multi-worker setups, ensure each worker loads its own copy or use a shared memory approach.
- GPU inference: set `CUDA_VISIBLE_DEVICES` per container; in Docker Compose, use `deploy.resources.devices`.

### TensorFlow Serving

```bash
docker run -t --rm -p 8501:8501 \
  -v "$PWD/models:/models/my_model" \
  -e MODEL_NAME=my_model \
  tensorflow/serving
```

---

## Orchestration & Scaling

When Compose isn't enough, containers become part of a larger scheduler.

- **Kubernetes** (de facto standard). Use GPU operator, node selectors, and sidecars for model downloading.
- **Kubeflow Pipelines** – runs each step in a container; components packaged as Docker images.
- **AWS SageMaker** – expects an ECR image with a specific HTTP API for training/serving.
- **Vertex AI** – custom container training and prediction.
- **Azure ML** – uses Docker images for environments and batch inference.

Key patterns:
- **Init containers** for downloading models/data from S3/GCS before the main container starts.
- **Sidecar containers** for logging, metric scraping, or authentication proxies.
- **Ephemeral volumes** (`emptyDir`) for shared `/dev/shm` when using PyTorch DataLoader workers.

---

## Observability, Logging & Health Checks

- All logs must go to `stdout`/`stderr`. Use Docker logging drivers to forward to Fluentd, ELK, etc.
- **Healthcheck** is mandatory for serving containers.
- **GPU metrics** can be exposed via `nvidia-dcgm-exporter` as a sidecar.
- **Structured logging** (JSON format) aids centralized analysis.
- **Prometheus metrics** endpoint (`/metrics`) on serving containers.

### Example Healthcheck (production)

```dockerfile
HEALTHCHECK --interval=15s --timeout=5s --retries=3 \
  CMD curl --fail http://localhost:8000/health || exit 1
```

For training containers, healthcheck can monitor process exit or training loop heartbeats via a simple HTTP endpoint.

---

## Security & Secrets Management

- Never bake secrets (API keys, passwords) into images.
- Use Docker secrets (Swarm), Kubernetes secrets, or environment variables injected at runtime.
- BuildKit `--secret` mount for private package feeds:

  ```dockerfile
  RUN --mount=type=secret,id=netrc,target=/root/.netrc \
      pip install --extra-index-url ... my-private-package
  ```

- Scan images for vulnerabilities (`docker scout quickview`, Trivy, or Snyk).
- Run as non-root, drop capabilities, use `--read-only` filesystem if possible.

---

## CI/CD for ML Containers

A typical CI pipeline for ML images:

1. **Lint** Dockerfile (Hadolint, Dockerfilelint)
2. **Build** image with BuildKit and pull/push layer cache.
3. **Run unit tests inside container** with `docker run ... pytest`.
4. **Integration tests** using Docker Compose (train a tiny epoch, check inference).
5. **Vulnerability scan**.
6. **Push** tagged image to registry (e.g., `model-train:prod-20260301`).
7. **Update** deployment manifests (Helm chart, ArgoCD).

Use `--cache-from` to accelerate builds. Example GitHub Actions step:

```yaml
- name: Build and push
  uses: docker/build-push-action@v5
  with:
    context: .
    push: true
    tags: registry/repo:latest,registry/repo:${{ github.sha }}
    cache-from: type=registry,ref=registry/repo:buildcache
    cache-to: type=registry,ref=registry/repo:buildcache,mode=max
```

---

## Sample Project Structure

```
ml-project/
├── Dockerfile.train          # Training image
├── Dockerfile.serve           # Inference/serving image
├── docker-compose.yml         # Local integration stack
├── .dockerignore              # Ignore data, .git, .env, .vscode, __pycache__
├── requirements/
│   ├── requirements.in
│   ├── requirements.txt       # Locked
│   └── requirements-dev.txt   # Tools for linting, testing
├── configs/
│   └── training_config.yaml
├── src/
│   ├── data/
│   ├── models/
│   └── train.py
├── api/                       # FastAPI serving app
│   ├── main.py
│   └── requirements.txt
├── scripts/
│   ├── entrypoint_train.sh
│   └── download_weights.sh
└── tests/
    └── test_inference.py
```

`.dockerignore` must exclude large files and directories:

```
model
data
.git
*.pyc
__pycache__
.env
.venv
venv
*.pth
!model/README.md   # keep small readme if needed
```

---

## Common Pitfalls & Solutions

| Pitfall | Symptom | Fix |
|--------|---------|-----|
| Mismatched CUDA/driver | `CUDA error: no CUDA-capable device` | Use compatible base image, check `nvidia-smi` in container |
| Large image size | >15 GB | Multi-stage, remove dev packages, use slim base, don’t bake model |
| Slow pip install | Minutes on every build | Use BuildKit cache mount, pin versions, use `pip install --no-deps` sparingly |
| Out‑of‑memory during training | Container killed by OOM | Set `--shm-size` (`/dev/shm`), use volume for datasets, tune DataLoader workers |
| Permission denied on volume mounts | User ID mismatch | Run container with same UID (`-u $(id -u)`) or adjust ownership in entrypoint |
| Model not found after 1st run | Volume not mounted correctly | Use named volumes or bind mount with absolute paths |
| Zombie processes | Defunct processes in container | Use an init process (`--init`) or `tini` |
| PyTorch DataLoader hang | No enough shared memory | `--shm-size=2g` or mount `/dev/shm` as `tmpfs` |

---

## Tooling & Ecosystem

- **nvidia-container-toolkit** – essential for GPU workloads.
- **Buildx** – multi-platform builds, advanced caching.
- **Docker Compose** – local orchestration.
- **Dive** – explore image layers and wasted space.
- **Hadolint** – Dockerfile linter.
- **Trivy / Grype** – vulnerability scanner.
- **dive** – check layer efficiency.
- **Skopeo** – inspect and copy images without pulling them.
- **Kaniko / Buildah** – building images in Kubernetes without Docker daemon.

---

## Appendix: Quick Reference

### Dockerfile GPU Code Snippet

```dockerfile
FROM nvidia/cuda:12.1-cudnn8-runtime-ubuntu22.04

# Set noninteractive to avoid prompts
ENV DEBIAN_FRONTEND=noninteractive
ENV PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3.10 python3-pip \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY requirements.txt .
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install --no-cache-dir -r requirements.txt

COPY src/ src/
ENTRYPOINT ["python", "-m", "train"]
CMD ["--help"]
```

### Run Training with All GPUs

```bash
docker run --gpus all --shm-size=2g -v /mnt/data:/data mytrainer:latest
```

### Docker Compose GPU Service

```yaml
services:
  app:
    image: mygpuimage
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
```

### Check GPU from Inside Container

```bash
docker run --gpus all --rm myimage nvidia-smi
```

---

*End of Docker.md – Built for MLOps engineers shipping ML in production.*