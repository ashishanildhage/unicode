# GitHub Actions for MLOps & AI Engineering  
**A Complete Beginner-to-Intermediate Guide**

Welcome! If you're new to MLOps or GitHub Actions, this document will take you from zero to building, testing, training, and deploying machine learning models automatically—all inside GitHub. Even if you already have some experience, you'll find best practices, advanced patterns, and a full reference to build real-world pipelines.

---

## 1. What Is GitHub Actions?

Imagine you could write down a series of steps that GitHub automatically executes whenever you commit code, open a pull request, or even on a time schedule. That’s exactly what GitHub Actions does. It's an automation platform built right into GitHub, often called a CI/CD (Continuous Integration / Continuous Deployment) tool.

For **MLOps** (Machine Learning Operations), GitHub Actions acts as the “conductor” of your machine learning orchestra. It can:

- Run experiments when you push new code.
- Test your data processing scripts.
- Train models on powerful GPU machines.
- Save and version models.
- Deploy models to production with approval gates.

All of this lives as `.yml` files inside your repository in a folder named `.github/workflows/`. Let’s break down the core ideas first.

---

## 2. Core Concepts – Explained Simply

Before we write any YAML, you need to understand the building blocks. Think of GitHub Actions like a factory assembly line.

| Concept | Everyday Analogy | What It Does |
|--------|-----------------|----------------|
| **Workflow** | A full production line with multiple stations. | An automated process defined in one `.yml` file. A repo can have many workflows, e.g., one for training and one for testing. |
| **Event** | A button that starts the assembly line (e.g., "Go!"). | The trigger that awakens the workflow. Common events: `push` (code pushed), `pull_request`, `schedule` (like a cron job), `workflow_dispatch` (manual “Run workflow” button). |
| **Job** | A collection of work that a specific worker does. | A set of steps that run on the same machine (called a runner). Jobs run in parallel by default, but you can chain them with `needs`. |
| **Step** | A single task the worker performs. | A step can be a shell command (`run: python train.py`) or a reusable piece of code called an **action** (`uses: actions/checkout@v4`). |
| **Action** | A pre-built tool you plug into your line. | Reusable unit of code. There are thousands of community actions on the GitHub Marketplace; you can also create your own. |
| **Runner** | The machine (the actual robot arm) that executes steps. | GitHub provides free cloud machines (like `ubuntu-latest`) with basic specs. For heavy ML work, you can set up your own powerful machines (self-hosted runners) with GPUs. |
| **Artifact** | The product that comes out of a job (e.g., a trained model file). | Files you can save and pass to later jobs or download manually. |
| **Secret** | A locked safe containing sensitive keys. | Encrypted environment variables like API tokens, passwords, cloud credentials. They are stored in your repository settings and never revealed in logs. |

Now you’re ready to see a workflow file.

---

## 3. Your First Workflow – Structure & Syntax

A workflow file is just YAML (a human‑readable text format) placed under `.github/workflows/`. The name can be anything, e.g., `ml-pipeline.yml`.

Here is a real example with commentary:

```yaml
# The name that appears in the GitHub Actions tab
name: MLOps Training Pipeline

# What triggers this workflow?
on:
  push:                        # whenever code is pushed
    branches: [main, develop]
  pull_request:                # when a PR targets main
    branches: [main]
  schedule:                    # automated cron job
    - cron: '0 2 * * 1'       # runs every Monday at 2 AM UTC (learn cron: minute hour day month weekday)
  workflow_dispatch:           # allows manual trigger from GitHub UI
    inputs:                    # parameters you can fill in when starting manually
      dataset-version:
        description: 'Which dataset version to use?'
        required: true
        default: 'v1.2'

jobs:                          # begin the list of jobs
  train-and-evaluate:          # a job named train-and-evaluate
    runs-on: ubuntu-latest     # use GitHub's free Linux runner (CPU only)
    timeout-minutes: 120       # kill the job if it runs longer than 2 hours

    env:                       # environment variables for all steps in this job
      MLFLOW_TRACKING_URI: ${{ secrets.MLFLOW_TRACKING_URI }}

    steps:                     # the actual steps to run
      # Step 1: Download the repository code onto the runner
      - uses: actions/checkout@v4
        with:
          lfs: true            # also pull large files stored with Git LFS

      # Step 2: Set up Python
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'
          cache: 'pip'         # automatically cache pip packages between runs

      # Step 3: Install Python dependencies
      - name: Install dependencies
        run: |
          pip install --upgrade pip
          pip install -r requirements.txt

      # Step 4: Run training, optionally using the manual input dataset version
      - name: Run Training
        run: python train.py --dataset ${{ github.event.inputs.dataset-version || 'v1.2' }}

      # Step 5: Save the trained model as an artifact (so later jobs can use it)
      - name: Upload trained model
        uses: actions/upload-artifact@v4
        with:
          name: model-artifacts
          path: models/        # the folder containing your model files
```

**Key beginner takeaways:**
- The `on` section defines when the workflow runs.
- `jobs` contains one or more independent tasks.
- Each job runs on a runner specified by `runs-on`.
- Steps use `uses` (to call a pre‑built action) or `run` (to execute commands).
- `${{ }}` is how you access variables, secrets, and inputs.

---

## 4. Expressions, Contexts & Functions – Making Workflows Dynamic

The magic of GitHub Actions lies in the `${{ }}` syntax. Inside those double curly braces, you can access a world of information about the current run.

### 4.1 Contexts
Contexts are pre-defined objects that hold data:

- `github.ref` – The branch or tag that triggered the workflow (e.g., `refs/heads/main`).
- `github.sha` – The exact commit hash (very useful for versioning models).
- `github.event_name` – Which event triggered it (`push`, `pull_request`, `schedule`…).
- `github.run_id` – A unique number for this workflow run.
- `github.event.inputs.*` – Values from the `workflow_dispatch` inputs you defined.
- `env.*` – Environment variables you set at workflow, job, or step level.
- `secrets.*` – Your encrypted secrets (never exposed in logs).
- `matrix.*` – When using a matrix strategy (explained later), you can access each combination’s values.

### 4.2 Functions
You can transform data with built‑in functions:

- `fromJSON('{"key":"value"}')` – Convert a string to an object. Handy for passing lists of hyperparameters.
- `toJSON(value)` – Convert an object to JSON string.
- `hashFiles('path/*')` – Get a unique hash of files. Perfect for caching keys.
- `contains('hello', 'ell')` – Check if a string contains another.
- `format('{0} {1}', 'hello', 'world')` – Format strings.

**Example:** Tag a Docker image with the commit hash:
```yaml
- name: Build and push Docker image
  uses: docker/build-push-action@v5
  with:
    tags: ghcr.io/${{ github.repository }}/model:${{ github.sha }}
```
Here, `github.repository` is the owner/repo name and `github.sha` is the commit hash.

---

## 5. Secrets & Environment Variables – Handling Sensitive Data

ML workflows are full of secrets: cloud keys, API tokens, database passwords, etc. You must never hardcode them.

- **Where to store them:** Go to your GitHub repository → Settings → Secrets and variables → Actions → New repository secret.
- **How to use them:** `${{ secrets.THE_NAME }}`
- **Environment protection:** You can create **environments** (like `staging`, `production`) with their own secrets and rules (e.g., require manual approval before deploying). In your workflow, you tell a job which environment it uses: `environment: production`.

**Example: Safely passing an MLflow tracking password:**
```yaml
env:
  MLFLOW_TRACKING_PASSWORD: ${{ secrets.MLFLOW_PASSWORD }}
```

**Important:** Secrets are automatically masked in logs. But if you echo a secret indirectly, it might leak. Never print a secret to the console. If you generate a token dynamically, use `::add-mask::` to hide it.

---

## 6. Managing Dependencies & Caching – Speeding Up Your Pipelines

ML projects often have huge dependencies (PyTorch, TensorFlow, Hugging Face models). Re‑downloading them every run wastes time and money. Caching solves this.

### 6.1 Python / pip dependencies
`actions/setup-python@v5` already includes a `cache: 'pip'` option that auto‑caches based on your requirements files. If you need custom cache control, use the generic `actions/cache@v4`:

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.cache/pip            # the directory to cache
    key: ${{ runner.os }}-pip-${{ hashFiles('requirements.txt') }}
    restore-keys: |
      ${{ runner.os }}-pip-
```
The `key` is like a fingerprint. When requirements change, the hash changes, and a new cache is saved.

### 6.2 Conda environments
If you use Conda, the setup‑miniconda action helps:
```yaml
- uses: conda-incubator/setup-miniconda@v3
  with:
    python-version: 3.10
    activate-environment: mlops-env
    environment-file: environment.yml

- uses: actions/cache@v4
  with:
    path: /usr/share/miniconda/envs/mlops-env
    key: conda-${{ runner.os }}-${{ hashFiles('environment.yml') }}
```

### 6.3 Hugging Face models and other large assets
You can cache the Hugging Face cache directory (`~/.cache/huggingface`) similarly with a key based on the specific model versions you use.

### 6.4 Datasets & model checkpoints
For datasets that change rarely, use DVC (Data Version Control) with remote storage (S3, GCS, etc.) rather than storing them in the GitHub cache (which has a 10 GB limit per repo). DVC integration:

```yaml
- uses: iterative/setup-dvc@v1
- name: Pull data
  env:
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  run: dvc pull
```

On self‑hosted runners, you can mount a persistent disk directly, so datasets live there permanently.

---

## 7. Choosing the Right Runner – The Machine Behind the Scenes

### 7.1 GitHub‑hosted runners (the free/paid standard machines)
These are maintained by GitHub. They come with:

| Label          | OS          | CPUs | RAM   | Disk (SSD) | GPU? |
|----------------|-------------|------|-------|------------|------|
| ubuntu-latest  | Ubuntu 22   | 4    | 16 GB | 14 GB      | No   |
| windows-latest | Windows Server 2022 | 4 | 16 GB | 14 GB | No |
| macos-latest   | macOS 12    | 3    | 14 GB | 14 GB      | No   |

Additionally, you can pay for **larger runners** with up to 64 vCPUs and 256 GB RAM, but still no GPUs.

**Beginner note:** Most non‑GPU tasks (linting, testing, data validation) run perfectly on `ubuntu-latest` for free on public repositories (private repos get 2,000–3,000 minutes depending on plan). GPU training is not possible here.

### 7.2 Self‑hosted runners (your own machine)
If you need a GPU (or specific hardware), you install the GitHub Actions runner software on your own server (cloud VM, on‑premise). Then in your workflow you specify the labels you gave it:

```yaml
runs-on: [self-hosted, linux, gpu]
```
**How a beginner can set one up:**
- Create an Ubuntu GPU VM on AWS/GCP/Azure.
- Install NVIDIA drivers, Docker, and the runner agent.
- Label it during registration (e.g., `gpu`, `a100`).
- Use the `--ephemeral` flag so the runner cleans itself after each job, preventing leftover files that could corrupt the next run.

**Security tip:** Always restrict network access to your self‑hosted runner; only allow GitHub’s IP addresses.

---

## 8. Artifacts & Model Versioning – Saving Your Work

After training, you need to save the model, evaluation plots, and logs.

### 8.1 Workflow artifacts
These are files you can keep for up to 90 days (retention can be changed). They are perfect for sharing data between jobs.

- Upload: `actions/upload-artifact@v4`
- Download: `actions/download-artifact@v4`

Example: after training, upload the model folder:
```yaml
- uses: actions/upload-artifact@v4
  with:
    name: model-${{ github.sha }}
    path: output/model.onnx
```

Later, in a deployment job, you can download it:
```yaml
- uses: actions/download-artifact@v4
  with:
    name: model-${{ github.sha }}
```

### 8.2 Model registries (better for production)
For long‑term model storage and versioning, you should push models to a dedicated registry. Popular options:

- **MLflow Model Registry** – Use `mlflow models register` with tracking server.
- **Hugging Face Hub** – Push using `huggingface_hub` library.
- **DVC** – Treat the model file as a DVC output, push it to remote storage.
- **Docker image** – Package the model inside a serving container and push to GHCR/Docker Hub.

Example: push to Hugging Face Hub:
```yaml
- name: Upload to Hugging Face
  env:
    HF_TOKEN: ${{ secrets.HF_TOKEN }}
  run: |
    python -c "
    from huggingface_hub import HfApi
    api = HfApi()
    api.upload_folder(
        folder_path='output',
        repo_id='my-org/my-model',
        commit_message='CI model from ${{ github.sha }}'
    )"
```

---

## 9. Common ML Pipeline Patterns Explained (with beginner-friendly comments)

### 9.1 Continuous Training (CT)
Train a model automatically every time code changes. This is the “CI” for ML.

```yaml
name: Continuous Training
on:
  push:
    branches: [main]
    paths:            # only run when files in these directories change
      - 'src/**'
      - 'configs/**'
      - 'data/*.yaml'
jobs:
  train:
    runs-on: [self-hosted, gpu]   # assuming you set up a GPU runner
    steps:
      - uses: actions/checkout@v4
      - name: Pull data with DVC
        run: dvc pull   # download the latest dataset from remote storage
      - name: Train
        run: python train.py
      - name: Evaluate model quality
        id: eval
        run: |
          score=$(python evaluate.py)
          echo "score=$score" >> $GITHUB_OUTPUT   # save output for next steps
      - name: Register model if good enough
        if: steps.eval.outputs.score > 0.9
        run: python promote.py --version ${{ github.sha }}
```

### 9.2 CI for ML Code (testing)
Before merging a pull request, automatically run linting, unit tests, and maybe a small training test. Use a matrix to test against multiple Python versions.

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.9, 3.10, 3.11]   # run 3 parallel jobs
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
      - run: pip install -e ".[dev]"
      - name: Lint
        run: ruff check src tests
      - name: Type check
        run: mypy src
      - name: Run tests
        run: pytest --cov=src
```

### 9.3 Scheduled Drift Detection
Hourly/daily checks on production data to see if model performance degrades or data distribution changes.

```yaml
on:
  schedule:
    - cron: '0 3 * * *'   # 3 AM UTC daily
jobs:
  drift-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Pull latest production data (via DVC)
        run: dvc pull data/prod/
      - name: Run drift monitor
        run: python drift_monitor.py
      - name: Create GitHub Issue if drift detected
        if: failure()          # this step only runs if previous step failed
        uses: peter-evans/create-issue-from-file@v4
        with:
          title: Data Drift Detected on ${{ github.run_id }}
          content-filepath: drift_report.md
```

### 9.4 Multi‑Environment Deployment with Manual Approval
Promote a model through staging to production using GitHub Environments. In the repository settings, you can configure the `production` environment to require one or more reviewers. No changes happen without a human clicking “Approve”.

```yaml
deploy-staging:
  needs: train
  environment: staging
  steps:
    - run: python deploy.py --env staging

deploy-prod:
  needs: deploy-staging          # must run after staging
  environment:
    name: production
    url: https://api.myapp.com/models   # shown in the deployment UI
  steps:
    - run: python deploy.py --env production
```

### 9.5 Hyperparameter Optimization (HPO) with Matrix Strategy
You can run many training jobs in parallel with different hyperparameters. The matrix is limited to 256 combinations, but it’s a simple way to do small sweeps.

```yaml
jobs:
  hpo:
    runs-on: [self-hosted, gpu]
    strategy:
      fail-fast: false   # don't cancel others if one fails
      matrix:
        learning_rate: [0.001, 0.0001]
        batch_size: [32, 64]   # will create 4 jobs (2x2)
    steps:
      - run: python train.py --lr ${{ matrix.learning_rate }} --bs ${{ matrix.batch_size }}
```
*Pro tip:* For serious HPO, use Optuna or Ray Tune and let them manage the search; GitHub Actions just kicks off the script.

---

## 10. Containerized ML – Docker in Actions

Using Docker ensures your training environment is identical every time: same CUDA version, same libraries. You build the image and push it to GitHub Container Registry (GHCR) or another registry.

```yaml
jobs:
  build-and-push:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write          # needed to push to GHCR
    steps:
      - uses: actions/checkout@v4
      - uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}   # auto-generated token
      - uses: docker/build-push-action@v5
        with:
          context: .
          file: docker/training.Dockerfile
          push: true
          tags: ghcr.io/${{ github.repository }}-train:${{ github.sha }}
          cache-from: type=gha     # cache Docker layers using GitHub Actions cache
          cache-to: type=gha,mode=max
```

**For GPU containers:** Your Dockerfile must start with a CUDA base image (e.g., `nvidia/cuda:12.1.0-runtime-ubuntu22.04`) and the self‑hosted runner must have `nvidia-docker` installed.

---

## 11. Integrating with the MLOps Ecosystem – What Beginners Need to Know

You don’t have to build everything from scratch. Here’s how popular tools plug into your actions:

- **DVC (Data Version Control):** Use the `iterative/setup-dvc@v1` action. Then `dvc pull`, `dvc repro`, `dvc push` inside your steps. DVC automatically handles data and model versioning, syncing with cloud storage (S3, GCS, etc.).
- **MLflow:** Set `MLFLOW_TRACKING_URI` as an environment variable pointing to your tracking server. Your training script logs metrics and parameters to MLflow. You can also register the model after training using `mlflow models register`.
- **Kubernetes deployment:** Use `kubectl` commands or the `azure/k8s-deploy` action to update a deployment image.
- **Hugging Face:** Push models and datasets directly from a step using the `huggingface_hub` Python library.
- **Cloud‑specific deployments:** Use OIDC (OpenID Connect) to authenticate to AWS/GCP/Azure without storing long‑lived credentials. For example, `aws-actions/configure-aws-credentials` uses OIDC to get temporary tokens.

---

## 12. Example: Deploying a Model to a Cloud Endpoint

Here’s a simplified deployment to AWS SageMaker:

```yaml
- name: Configure AWS credentials (OIDC)
  uses: aws-actions/configure-aws-credentials@v4
  with:
    role-to-assume: arn:aws:iam::123456789:role/github-actions-role
    aws-region: us-east-1

- name: Create SageMaker Model and Endpoint
  run: |
    aws sagemaker create-model --model-name "churn-model-${{ github.sha }}" --primary-container Image=123456789.dkr.ecr.us-east-1.amazonaws.com/model-serving:latest
    aws sagemaker create-endpoint-config --endpoint-config-name "churn-config-${{ github.sha }}" --production-variants ...
    aws sagemaker create-endpoint --endpoint-name "churn-endpoint" --endpoint-config-name "churn-config-${{ github.sha }}"
```
(This is a simplified illustration; real‑world scripts are more robust.)

---

## 13. Reusable Actions & Workflows – Don’t Repeat Yourself

As your pipelines grow, you’ll want to package common steps into reusable blocks.

### Composite Action (a single repository action)
Create a file `action.yml` (or `.github/actions/my-action/action.yml`) that bundles steps:

```yaml
name: 'DVC Pull and Reproduce'
inputs:
  remote:
    description: 'DVC remote name'
    required: true
runs:
  using: "composite"
  steps:
    - uses: iterative/setup-dvc@v1
    - shell: bash
      run: |
        dvc remote default ${{ inputs.remote }}
        dvc pull
        dvc repro
```
Then you can call it from any workflow: `uses: ./.github/actions/dvc-pull-and-repro`

### Reusable Workflow (called from other repositories)
Define a workflow in `.github/workflows/train.yml` that accepts inputs and secrets:

```yaml
on:
  workflow_call:
    inputs:
      dataset-version:
        required: true
        type: string
    secrets:
      MLFLOW_TOKEN:
        required: true
jobs:
  train:
    runs-on: [self-hosted, gpu]
    steps:
      - run: python train.py --dataset-version ${{ inputs.dataset-version }}
```
Other repos can then reference it.

---

## 14. Security Basics – Keep Your Automation Safe

- **Least privilege:** In the workflow, add a `permissions` block to restrict the default `GITHUB_TOKEN` scope.  
  Example: `permissions: contents: read`
- **OIDC instead of secrets:** For cloud providers, use OpenID Connect to allow temporary tokens, eliminating the risk of leaked long‑lived keys.
- **Protected environments:** Require reviewers and wait timers before deploying to production. No code can automatically deploy to prod without a human.
- **Scan your code and containers:** Add steps that check for known vulnerabilities (e.g., `pip-audit`, `trivy`).
- **Be careful with pull requests from forks:** Secrets are not passed to PRs from outside contributors for safety. If you need to run ML tests on PRs from forks, you might need a `pull_request_target` event, but that requires careful handling to avoid secret exposure.

---

## 15. Keeping Costs and Time Under Control

- **Cache everything you can:** pip, conda, Hugging Face models, Docker layers. Avoid re‑downloading.
- **Use `paths` and `paths-ignore`:** Don’t run training when you only change the README.
- **Concurrency:** Set `concurrency: ci-${{ github.ref }}` to automatically cancel old runs of the same branch when a new push happens.
- **Self‑hosted runner scaling:** Start GPU instances only when needed (e.g., via webhook auto‑scaling) and shut them down when idle.
- **Larger GitHub‑hosted runners:** If you just need more RAM or CPU for a short job, you can use paid larger runners without managing servers.

---

## 16. Monitoring Your Pipelines

- **Workflow visualisation:** On the Actions tab, you see a DAG view of your jobs. Click around.
- **Status badges:** Add to your `README.md`:  
  `![CI](https://github.com/owner/repo/actions/workflows/ci.yml/badge.svg)`
- **Notifications:** Send a Slack or Teams message on failure/success using an action like `slackapi/slack-github-action@v1.24.0`.

```yaml
- name: Notify Slack
  uses: slackapi/slack-github-action@v1.24.0
  with:
    payload: '{"text":"Model training ${{ job.status }}: ${{ github.sha }}"}'
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
```

---

## 17. Common Beginner Pitfalls (and How to Avoid Them)

1. **Disk full on `ubuntu-latest`** – Clean up unnecessary tools in a step:  
   `sudo rm -rf /usr/share/dotnet /opt/ghc /usr/local/share/boost`
2. **Git LFS bandwidth exceeded** – Use DVC instead for large files, or purchase LFS data packs.
3. **Secrets missing in PR from fork** – That’s intentional. Use `pull_request_target` only if you fully understand the security implications.
4. **Self‑hosted runner state pollution** – Always use `--ephemeral` when registering the runner so it wipes everything after each job.
5. **Artifact upload timeout** – Compress large folders (e.g., models) into a single tar.gz, or better, push directly to an external registry or cloud storage.

---

## 18. Full End‑to‑End Beginner‑Friendly Example

Below is a complete workflow that ties almost everything together. Read the inline comments to understand each piece.

```yaml
name: MLOps Full Pipeline
on:
  push:
    branches: [main]
    paths:               # only run if these files change
      - 'src/**'
      - 'configs/**'
      - 'Dockerfile'
      - '.github/workflows/mlops.yml'

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}-model

jobs:
  # Step 1: Validate that the data is correct before training
  data-validation:
    runs-on: ubuntu-latest
    outputs:           # this job exports a value for later jobs to check
      data_ok: ${{ steps.validate.outputs.ok }}
    steps:
      - uses: actions/checkout@v4
      - name: Install DVC
        uses: iterative/setup-dvc@v1
      - name: Pull raw data
        run: dvc pull data/raw
      - name: Validate data schema and statistics
        id: validate
        run: |
          python validate_data.py
          echo "ok=true" >> $GITHUB_OUTPUT   # assume script exits 0 if ok

  # Step 2: Train the model only if data is valid, uses a GPU self‑hosted runner
  train:
    needs: data-validation
    if: needs.data-validation.outputs.data_ok == 'true'
    runs-on: [self-hosted, linux, gpu]      # change to your GPU runner label
    steps:
      - uses: actions/checkout@v4
      - name: DVC Pull all data
        run: dvc pull
      - name: Train with MLflow tracking
        run: python train.py                # script logs to MLflow
      - name: Evaluate model
        id: eval
        run: |
          python evaluate.py
          echo "f1_score=$(cat metrics/f1.txt)" >> $GITHUB_OUTPUT
      - name: Register model if performance is good
        if: steps.eval.outputs.f1_score > 0.85
        run: python register_model.py       # registers in MLflow registry
      # Build and push a Docker image for serving the model
      - name: Build and push Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }}
      # Keep evaluation plots as artifacts (for human review)
      - name: Upload evaluation plots
        uses: actions/upload-artifact@v4
        with:
          name: eval-plots
          path: plots/

  # Step 3: Deploy to staging environment (no manual approval needed)
  deploy-staging:
    needs: train
    environment: staging
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Update Kubernetes deployment in staging
        run: |
          kubectl set image deployment/model-staging \
            model=${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }} \
            --namespace=staging

  # Step 4: Deploy to production (requires manual approval in GitHub Environments)
  deploy-prod:
    needs: deploy-staging
    environment: production        # protected with required reviewers
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Update Kubernetes deployment in production
        run: |
          kubectl set image deployment/model-prod \
            model=${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }} \
            --namespace=production
```

**How to read this as a beginner:**  
The workflow starts when code is pushed to the main branch and any of the listed paths change. It first validates the dataset, then—if the data is OK—trains a model on a GPU machine, registers it, pushes a Docker image, and finally deploys it to staging and then to production. The production deployment requires a human to approve it in the GitHub UI.

---

## 19. Where to Learn More

- [Official GitHub Actions Documentation](https://docs.github.com/actions)
- [Workflow syntax reference](https://docs.github.com/actions/using-workflows/workflow-syntax-for-github-actions)
- [Security hardening guide](https://docs.github.com/actions/security-guides)
- [DVC and GitHub Actions](https://dvc.org/doc/user-guide/ci/github-actions)
- [MLflow Tracking](https://mlflow.org/docs/latest/tracking.html)
- [Hugging Face GitHub Actions](https://huggingface.co/docs/hub/github-actions)
- [Using OIDC with cloud providers](https://docs.github.com/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-cloud-providers)

---

*This guide starts with the basics and grows with you. Save it, experiment, and let it evolve alongside your MLOps journey. Happy automating!*

---
---

# GitHub Actions for MLOps & AI Engineering  
**A Comprehensive Guide for Engineers with 3+ Years of Experience**

---

## 1. Introduction

GitHub Actions (GHA) is a powerful CI/CD and automation platform deeply integrated with GitHub repositories. For MLOps and AI engineers, it acts as the orchestration backbone for building, testing, training, deploying, and monitoring machine learning pipelines—directly from your codebase.

This documentation assumes you already understand ML workflow stages (data prep, training, evaluation, deployment) and have some CI/CD familiarity. It focuses on adapting GHA’s concepts, syntax, and ecosystem to the unique challenges of MLOps: large datasets, GPU needs, model versioning, experiment tracking, and production serving.

---

## 2. Core Concepts Refresher

| Concept      | Description                                                                 |
|--------------|-----------------------------------------------------------------------------|
| **Workflow** | A configurable automated process defined in `.github/workflows/*.yml`. A repo can have many workflows. |
| **Event**    | A trigger that starts a workflow (push, pull_request, schedule, workflow_dispatch, etc.). |
| **Job**      | A set of steps executed on the same runner. Jobs run in parallel by default; can be sequenced with `needs`. |
| **Step**     | An individual task: a shell command or an action (`uses: ...`).             |
| **Action**   | Reusable unit of code. Can be JavaScript or Docker container. Public marketplace or private. |
| **Runner**   | The machine (GitHub-hosted or self-hosted) that executes jobs.              |
| **Artifact** | Files produced by a workflow (models, reports, logs) for later use.        |
| **Secret**   | Encrypted environment variable stored in repo/org settings, not exposed in logs. |

---

## 3. YAML Structure & Best Practices

A typical workflow file:

```yaml
name: MLOps Training Pipeline
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 2 * * 1'   # Every Monday at 2 AM UTC
  workflow_dispatch:       # Manual trigger with inputs
    inputs:
      dataset-version:
        description: 'Version of dataset to use'
        required: true
        default: 'v1.2'

jobs:
  train-and-evaluate:
    runs-on: ubuntu-latest   # or self-hosted, e.g., [self-hosted, linux, gpu]
    timeout-minutes: 120
    env:
      MLFLOW_TRACKING_URI: ${{ secrets.MLFLOW_TRACKING_URI }}
    steps:
      - uses: actions/checkout@v4
        with:
          lfs: true          # pull Git LFS files if used

      # Setup Python, caching dependencies
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'
          cache: 'pip'

      - name: Install dependencies
        run: |
          pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run Training
        run: python train.py --dataset ${{ github.event.inputs.dataset-version || 'v1.2' }}

      - name: Upload trained model
        uses: actions/upload-artifact@v4
        with:
          name: model-artifacts
          path: models/
```

**Key Points:**
- Use `cron` for retraining schedules.
- `workflow_dispatch` with inputs enables manual runs with parameters.
- Environment variables can reference secrets and GitHub context (`${{ ... }}`).
- Always set a `timeout-minutes` to prevent runaway costs.

---

## 4. Context, Expressions & Functions

GitHub Actions provides a rich expression syntax inside `${{ }}`. Common contexts useful for MLOps:

- `github.ref`: branch or tag name (e.g., `refs/heads/experiment/fastercnn`).
- `github.sha`: commit SHA, used for artifact/model versioning.
- `github.event_name`: push, pull_request, schedule, etc.
- `github.run_id`: unique run identifier.
- `github.event.inputs.*`: inputs from `workflow_dispatch`.
- `env.*`: environment variables at workflow/job/step level.
- `secrets.*`: encrypted secrets (never printed).
- `matrix.*`: when using matrix strategies.

**Functions:**
- `fromJSON()`: parse JSON strings (e.g., list of hyperparameters).
- `toJSON()`: convert object to JSON (useful for passing complex data between jobs).
- `hashFiles('path/to/*')`: generate a hash for cache keys.
- `contains()`, `startsWith()`, `format()`: string/array operations.

Example: setting a dynamic tag for a Docker image:

```yaml
- name: Build and push
  uses: docker/build-push-action@v5
  with:
    tags: ghcr.io/${{ github.repository }}/model:${{ github.sha }}
```

---

## 5. Secrets & Environment Variables for ML Pipelines

ML projects involve many sensitive assets: API keys (MLflow, cloud storage), model registry credentials, Docker registry tokens, etc.

- **Store as encrypted secrets:** Go to Settings → Secrets and variables → Actions.
- **Access in workflows:** `${{ secrets.WANDB_API_KEY }}`.
- **Environment-level protection:** Use environments (e.g., `production`) with approval gates and environment-specific secrets.
- Use **environment files** for dynamic variables (e.g., `echo "MODEL_VERSION=${GITHUB_SHA}" >> $GITHUB_ENV`).

**Security note:** Secrets are masked in logs, but avoid echoing them accidentally. Use `::add-mask::` if you need to hide a dynamically generated token.

---

## 6. Managing ML Dependencies & Caching

### 6.1 Python/Pip Dependencies

`actions/setup-python@v5` with `cache: 'pip'` automatically caches dependencies based on `requirements.txt` or `pyproject.toml`. However, for complex ML stacks you may need more control.

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-${{ hashFiles('requirements.txt') }}
    restore-keys: |
      ${{ runner.os }}-pip-
```

### 6.2 Conda Environments

For projects using Conda, use a cache around the conda environment path:

```yaml
- uses: conda-incubator/setup-miniconda@v3
  with:
    python-version: 3.10
    activate-environment: mlops-env
    environment-file: environment.yml

- uses: actions/cache@v4
  with:
    path: /usr/share/miniconda/envs/mlops-env
    key: conda-${{ runner.os }}-${{ hashFiles('environment.yml') }}
```

### 6.3 Model & Dataset Caching

Large model checkpoints and datasets shouldn't be re-downloaded each run.

- **Use GitHub Cache** (max 10 GB per repo): ideal for pre-trained weights and small/medium datasets.
- **Use S3/GCS with DVC**: Pull only changed data via DVC.
- **For GPUs self-hosted runners** maintain a persistent shared volume to store `/data` and `/models`.

Example DVC cache approach:

```yaml
- uses: iterative/setup-dvc@v1
- name: Pull data
  env:
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  run: dvc pull
```

---

## 7. Runner Selection for ML Workloads

### 7.1 GitHub-Hosted Runners

| Runner        | OS         | vCPUs | RAM   | Disk (SSD) | GPU Support?       |
|---------------|------------|-------|-------|------------|--------------------|
| ubuntu-latest | Ubuntu 22  | 4     | 16 GB | 14 GB      | No                 |
| windows-latest| Win Server 2022 | 4 | 16 GB | 14 GB      | No                 |
| macos-latest  | macOS 12   | 3     | 14 GB | 14 GB      | No                 |
| Larger runners (paid) | Ubuntu / Windows | 8/16/32/64 vCPUs | 32/64/128/256 GB | various | No native GPU |

**ML specific limitations:**
- CPU only, no CUDA.
- Disk space limited for large datasets/models.
- Timeout: 6 hours (private repos), 72 hours for larger runners.

### 7.2 Self-Hosted Runners

Essential for GPU training, large memory, or special hardware (TPU). Install the runner agent on your cloud VM or on-prem server.

**Labels:** Tag runners with attributes: `self-hosted, linux, gpu, a100`.

Workflow example:

```yaml
runs-on: [self-hosted, linux, gpu]
```

**Best practices:**
- Use ephemeral runners to avoid state pollution.
- Mount a persistent volume for datasets/models to avoid repeated downloads.
- Secure runners with appropriate firewall rules and restrict GitHub IPs.
- Use a dedicated GitHub App or fine-grained PAT for runner registration.
- Disposal: ensure runners clean up temporary files and stop after job to save costs.

**GPU runner setup snippet (Ubuntu):**
```bash
sudo apt install -y nvidia-container-toolkit
# Ensure Docker can access GPU, then run actions/runner image configured with GPU support.
```

---

## 8. Artifacts, Packages, Model Versioning

ML models are the primary build outputs. Use a combination of GitHub artifacts and container/package registries.

### 8.1 Workflow Artifacts

- Store models, evaluation plots, logs between jobs.
- Max retention: 90 days (can be customized).
- Use `actions/upload-artifact@v4` and `actions/download-artifact@v4`.
- For large models (>10 GB), compression or external storage is better.

```yaml
- uses: actions/upload-artifact@v4
  with:
    name: model-${{ github.sha }}
    path: output/model.onnx
```

### 8.2 Model Registries & External Storage

Integrate with dedicated model registries:

- **MLflow Model Registry** – Use MLflow CLI to register models.
- **DVC with remote storage** – Treat models as DVC-tracked outputs.
- **Hugging Face Hub** – Push models using `huggingface_hub` library.
- **Container Registries** – Package the model inside a Docker image pushed to GHCR/Docker Hub.

Example: push to Hugging Face Hub:

```yaml
- name: Upload model to Hugging Face
  env:
    HF_TOKEN: ${{ secrets.HF_TOKEN }}
  run: |
    python -c "
    from huggingface_hub import HfApi
    api = HfApi()
    api.upload_folder(
        folder_path='output',
        repo_id='my-org/my-model',
        commit_message='CI model from ${{ github.sha }}'
    )"
```

---

## 9. ML Pipeline Patterns with GitHub Actions

### 9.1 Continuous Training (CT)

Triggered on code/data changes to retrain, evaluate, and conditionally promote.

```yaml
name: Continuous Training
on:
  push:
    branches: [main]
    paths:
      - 'src/**'
      - 'configs/**'
      - 'requirements.txt'
      - 'data/*.yaml'   # DVC pipeline definitions

jobs:
  train:
    runs-on: [self-hosted, gpu]
    steps:
      - uses: actions/checkout@v4
        with: { lfs: true }
      - name: DVC Pull Data
        run: dvc pull
      - name: Run Training
        run: python train.py
      - name: Evaluate
        id: eval
        run: |
          score=$(python evaluate.py)
          echo "score=$score" >> $GITHUB_OUTPUT
      - name: Promote Model
        if: steps.eval.outputs.score > 0.9
        run: python promote.py --version ${{ github.sha }}
```

### 9.2 CI for ML Code & Testing

- Run linting, unit tests, integration tests on PR.
- Use matrix to test multiple Python versions, OS, or even different model frameworks.

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.9, 3.10, 3.11]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: pip install -e ".[dev]"
      - name: Lint
        run: ruff check src tests
      - name: Type check
        run: mypy src
      - name: Test
        run: pytest --cov=src --cov-report=xml
      - name: Upload coverage
        uses: codecov/codecov-action@v3
```

### 9.3 Scheduled Drift Detection & Monitoring

Use cron to run data validation and model performance checks.

```yaml
on:
  schedule:
    - cron: '0 3 * * *'   # Daily at 3 AM
jobs:
  drift-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Pull latest production data
        run: dvc pull data/prod/
      - name: Detect drift
        run: python drift_monitor.py
      - name: Create Issue if drift detected
        if: failure()
        uses: peter-evans/create-issue-from-file@v4
        with:
          title: Data Drift Detected on ${{ github.run_id }}
          content-filepath: drift_report.md
```

### 9.4 Multi-Environment Deployment

Promote a model from dev → staging → production using GitHub Environments with protection rules and required reviewers.

```yaml
deploy-staging:
  needs: train
  environment: staging
  steps:
    - run: python deploy.py --env staging

deploy-prod:
  needs: deploy-staging
  environment:
    name: production
    url: https://api.myapp.com/models
  steps:
    - run: python deploy.py --env production
```

### 9.5 Hyperparameter Optimization (HPO) with Matrix

GitHub’s matrix strategy can spawn parallel runs for HPO on self-hosted runners, though it’s limited to 256 jobs. Combine with experiment tracking.

```yaml
jobs:
  hpo:
    runs-on: [self-hosted, gpu]
    strategy:
      fail-fast: false
      matrix:
        learning_rate: [0.001, 0.0001]
        batch_size: [32, 64]
    steps:
      - run: python train.py --lr ${{ matrix.learning_rate }} --bs ${{ matrix.batch_size }}
```

**Better alternative:** Use a dedicated tool like Optuna with a shared MLflow server; GHA triggers the HPO script which returns the best parameters.

---

## 10. Containerized ML Pipelines

Building Docker images for training and inference, pushing to a registry (GHCR), and using them in later steps or deployments.

```yaml
jobs:
  build-and-push-train:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - uses: actions/checkout@v4
      - uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      - uses: docker/build-push-action@v5
        with:
          context: .
          file: docker/training.Dockerfile
          push: true
          tags: ghcr.io/${{ github.repository }}-train:${{ github.sha }}
          cache-from: type=gha
          cache-to: type=gha,mode=max
```

**Using GPU-enabled containers:** Ensure the Dockerfile has the appropriate CUDA base image and that the runner has nvidia-docker runtime.

---

## 11. Integrating with MLOps Ecosystem

### 11.1 DVC (Data & Model Versioning)

- Use `iterative/setup-dvc@v1` to install DVC.
- Set up remote storage credentials (S3, GCS, Azure) as secrets.
- Pull/Push data and models within workflows.

```yaml
- name: Pull data
  run: dvc pull
- name: Reproduce pipeline
  run: dvc repro
- name: Push updated outputs
  run: dvc push
```

### 11.2 MLflow Tracking & Registry

- Set `MLFLOW_TRACKING_URI` to a central server (e.g., Databricks, self-hosted).
- Log parameters, metrics, artifacts from training scripts.
- Register a model after evaluation success.

```yaml
- name: Train
  run: python train.py
- name: Register model
  if: success()
  run: |
    mlflow models register-model --model-name "churn-predictor" \
      --run-id $MLFLOW_RUN_ID --tag "git_commit=${{ github.sha }}"
```

### 11.3 Kubernetes & Seldon/KFServing

Deploy models to Kubernetes using actions like `Azure/k8s-deploy`, or directly via `kubectl`. Use canary deployments with Seldon for A/B testing.

```yaml
- name: Deploy to K8s
  uses: azure/k8s-deploy@v4
  with:
    manifests: k8s/deployment.yaml
    images: myregistry.azurecr.io/model:${{ github.sha }}
    namespace: ml-models
```

### 11.4 Hugging Face & Transformers

- Cache HF models/hub using `cache: pip` or dedicated cache for `~/.cache/huggingface`.
- Use `huggingface_hub` Python library to push models/datasets.

---

## 12. CI/CD for Model Serving (Inference Endpoints)

Deploy a model to serverless platforms (e.g., AWS SageMaker, GCP Vertex AI, Azure ML) directly from the workflow.

**Example: Deploy to SageMaker endpoint:**

```yaml
- name: Deploy to SageMaker
  run: |
    aws sagemaker create-model --model-name "my-model-${{ github.sha }}" ...
    aws sagemaker create-endpoint-config ...
    aws sagemaker create-endpoint ...
```

Use `aws-actions/configure-aws-credentials` for OIDC authentication (no long-lived secrets).

---

## 13. Composite Actions & Reusable Workflows

Encapsulate common ML steps into reusable actions to avoid YAML duplication.

### Composite Action (`action.yml`):

```yaml
name: 'DVC Pull and Reproduce'
inputs:
  remote:
    description: 'DVC remote name'
    required: true
runs:
  using: "composite"
  steps:
    - uses: iterative/setup-dvc@v1
    - shell: bash
      run: |
        dvc remote default ${{ inputs.remote }}
        dvc pull
        dvc repro
```

### Reusable Workflow (called from other repos):

```yaml
# .github/workflows/train.yml
on:
  workflow_call:
    inputs:
      dataset-version:
        required: true
        type: string
    secrets:
      MLFLOW_TOKEN:
        required: true
jobs:
  train:
    runs-on: [self-hosted, gpu]
    steps:
      - name: Train
        run: python train.py --dataset-version ${{ inputs.dataset-version }}
```

---

## 14. Security Hardening

- **Least privilege:** Use `permissions` block to restrict token scope.
- **OIDC authentication** to cloud providers instead of static credentials.
- **Environment protection rules** for production deployments (reviewers, wait timer).
- **Scan dependencies** (e.g., `safety`, `pip-audit`) and Docker images (`docker/scout` or `trivy`).
- **Do not expose API keys** in pull_request workflows from forks unless explicitly allowed; use `pull_request_target` with extreme caution.

---

## 15. Cost & Time Optimisation

- **Caching:** Cache everything reasonable (pip, conda, HF models, Docker layers).
- **Selective runs:** Use `paths` and `paths-ignore` to skip unnecessary workflow runs.
- **Concurrency:** Limit concurrent runs with `concurrency: ci-${{ github.ref }}` to avoid resource contention.
- **Self-hosted runner scaling:** Pre-warm GPU instances during business hours, shut down overnight.
- **Use GitHub’s larger runners** if you occasionally need more CPU/RAM without maintaining infrastructure.
- **Parallel matrix jobs** can speed up HPO or cross-validation but beware of rate limits and costs.

---

## 16. Monitoring & Observability

- **Workflow visualization:** GitHub provides a built-in DAG view.
- **Status badges:** Add to README: `![CI](https://github.com/owner/repo/actions/workflows/ci.yml/badge.svg)`
- **Slack/Teams notifications:** Use `rtCamp/action-slack-notify` or the official Slack action.

```yaml
- name: Notify Slack
  uses: slackapi/slack-github-action@v1.24.0
  with:
    payload: '{"text":"Model training ${{ job.status }}: ${{ env.MODEL_VERSION }}"}'
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
```

- **Centralized logging:** Send training logs/metrics directly to MLflow/W&B from the job; the action itself just triggers it.

---

## 17. Common Pitfalls & Solutions

1. **Disk full on GitHub runners:**  
   Pre-clean with `sudo rm -rf /usr/share/dotnet /opt/ghc` and use `actions/cache` aggressively.

2. **Git LFS bandwidth quota exceeded:**  
   Use DVC for large files, or move to a dedicated LFS server.

3. **Secrets not available in pull_request from forks:**  
   Use `pull_request_target` event (with extreme care, review danger) or restrict the workflow trigger.

4. **Self-hosted runner state leakage:**  
   Always use `--ephemeral` flag when registering runners.

5. **Large artifact upload timeout:**  
   Compress into a single archive, use external storage for models > 10 GB, or stream directly to cloud storage from the training job.

---

## 18. Complete Example: End-to-End MLOps Workflow

```yaml
name: MLOps Full Pipeline
on:
  push:
    branches: [main]
    paths:
      - 'src/**'
      - 'configs/**'
      - 'Dockerfile'
      - 'docker-compose.yaml'
      - '.github/workflows/mlops.yml'

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}-model

jobs:
  data-validation:
    runs-on: ubuntu-latest
    outputs:
      data_ok: ${{ steps.validate.outputs.ok }}
    steps:
      - uses: actions/checkout@v4
      - name: Install DVC
        uses: iterative/setup-dvc@v1
      - name: Pull data
        run: dvc pull data/raw
      - name: Validate data
        id: validate
        run: |
          python validate_data.py
          echo "ok=true" >> $GITHUB_OUTPUT

  train:
    needs: data-validation
    if: needs.data-validation.outputs.data_ok == 'true'
    runs-on: [self-hosted, linux, gpu]
    steps:
      - uses: actions/checkout@v4
      - name: DVC Pull all data
        run: dvc pull
      - name: Train with MLflow tracking
        run: python train.py
      - name: Evaluate
        id: eval
        run: |
          python evaluate.py
          echo "f1_score=$(cat metrics/f1.txt)" >> $GITHUB_OUTPUT
      - name: Register model if good
        if: steps.eval.outputs.f1_score > 0.85
        run: python register_model.py
      - name: Build Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }}
      - name: Upload evaluation plots
        uses: actions/upload-artifact@v4
        with:
          name: eval-plots
          path: plots/

  deploy-staging:
    needs: train
    environment: staging
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to staging K8s
        run: |
          kubectl set image deployment/model-staging \
            model=${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }} \
            --namespace=staging

  deploy-prod:
    needs: deploy-staging
    environment: production
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Approve and deploy to prod
        run: |
          kubectl set image deployment/model-prod \
            model=${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }} \
            --namespace=production
```

---

## 19. References & Further Reading

- [GitHub Actions Documentation](https://docs.github.com/actions)
- [Workflow syntax reference](https://docs.github.com/actions/using-workflows/workflow-syntax-for-github-actions)
- [Security hardening](https://docs.github.com/actions/security-guides)
- [DVC & GitHub Actions](https://dvc.org/doc/user-guide/ci/github-actions)
- [MLflow Tracking in CI/CD](https://mlflow.org/docs/latest/tracking.html)
- [Hugging Face Actions](https://huggingface.co/docs/hub/github-actions)
- [Using OIDC with cloud providers](https://docs.github.com/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-cloud-providers)

---

*This living document covers the state of practice for MLOps with GitHub Actions. Adjust to your stack and keep it versioned alongside your code.*