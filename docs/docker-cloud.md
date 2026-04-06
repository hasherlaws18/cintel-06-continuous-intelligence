# Alternative Execution: Containers in the Cloud (GitHub Actions)

This project can be packaged and executed
in a Docker container without installing Docker locally.

Instead of running the pipeline on your machine,
you can use GitHub Actions to:

- build a container image from a Dockerfile
- run the project inside that container
- view logs from the execution

This approach avoids local setup issues and
provides a reproducible execution environment.

## Docker Containers

Containers package an application with its environment:

- Python version
- dependencies
- project files

It ensures the project runs the same way across systems.

In industry, containers are commonly used for deployment and scaling.
We illustrate them as an optional extension
to understand packaging and reproducibility.

## Requirements

Adding this option requires:

- a Dockerfile in the project root
- a GitHub Actions workflow file

No Docker installation is required on your local machine.
Docker Desktop is **not** recommended on many Windows machines.

## Step 1. Add a Dockerfile

Create a file named `Dockerfile` in the project root:

```dockerfile
FROM python:3.14-slim

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir uv

RUN uv self update
RUN uv python pin 3.14
RUN uv sync --extra dev --extra docs --upgrade

CMD ["uv", "run", "python", "-m", "cintel.continuous_intelligence_case"]
```

IMPORTANT: Adjust the final command when your custom project
entry point (the module name) differs.

## Step 2. Add a GitHub Actions Workflow

Create the file:

.github/workflows/docker-build.yml

```yaml
name: Container Build and Run

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  build-run:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Build container
        run: docker build -t cintel-pipeline .

      - name: Run container
        run: docker run cintel-pipeline
```

## Step 3. Run the Workflow

1. Push your changes to GitHub
2. Open the Actions tab
3. Select the workflow
4. View logs for:
   - container build steps
   - pipeline execution output

You should see:

Pipeline executed successfully!

## What to Observe

As the workflow runs, note:

- how dependencies are installed inside the container
- how the pipeline runs without your local environment
- any errors during build or execution

These logs provide insight into how software is packaged and executed in production systems.

## Optional: Share Your Results

If you experiment with containers, document:

- your operating system (if you also tried locally)
- any setup steps
- issues encountered
- performance observations
- link to your repository

## Summary

- Containers package code and environment together
- GitHub Actions can build and run containers in the cloud
- This avoids local setup issues while exposing real-world tooling

This is an optional extension. The core project does not require containers.

## Notes

This pattern is reusable across projects:

- Dockerfile defines execution environment
- GitHub Actions provides remote execution
- No local Docker required
