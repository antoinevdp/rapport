# Bloc 2 DevOps Addition Design

## Goal

Add a DevOps-focused subsection to Bloc 2 in `main.tex` based on the repository `antoinevdp/fizzbuzz-Efrei`, and update the Bloc 2 evidence table at the end of the section.

The new text should explain what was implemented in the repository from a DevOps perspective, using `nous`, and stay proportionate to the actual scope of the project. Target length: about one page.

## Repository Findings

The repository is intentionally simple on the application side: a Python implementation of FizzBuzz with unit tests. Its value for Bloc 2 is not the business logic, but the delivery chain built around it.

Relevant elements found in the repository:

- `main.py`: small Python application entry point.
- `test.py`: unit tests with `unittest`.
- `.github/workflows/python-package.yml`: GitHub Actions workflow triggered on `dev`, `main`, and `docker`.
- Workflow steps: dependency installation, `flake8`, `python -m unittest`, `coverage run`, `coverage report`.
- Matrix execution on Python `3.9`, `3.10`, `3.11`.
- `Dockerfile`: container image based on `python:3.12.8-slim`, non-root user, dependency installation, port exposure, runtime command.
- `compose.yaml`: local reproducible execution with Docker Compose.
- `README.Docker.md`: build and push guidance for a container registry.

## Chosen Approach

Add a new subsection dedicated to the DevOps project instead of blending the content into the existing Spark explanation.

This keeps the structure of Bloc 2 readable:

1. `Projet Spark` remains the main proof for distributed processing and large-scale data handling.
2. `Projet DevOps : fizzbuzz-Efrei` becomes the support for CI/CD, testing automation, and containerization.
3. The final Bloc 2 evidence table explicitly references both projects depending on the skill being justified.

## Planned Text Structure

### 1. `\subsubsection{Projet DevOps : fizzbuzz-Efrei}`

Position the repository as a support project used to demonstrate industrialization practices:

- continuous integration;
- automated quality checks;
- containerization;
- preparation for deployment.

The text must avoid overstating the project. It should clearly say that the functional scope is simple, but that this simplicity helps focus on the delivery chain itself.

### 2. CI pipeline explanation

Explain that the GitHub Actions workflow validates the code automatically on several branches and Python versions.

Key points to mention:

- branch triggers on `dev`, `main`, and `docker`;
- matrix execution on three Python versions;
- installation of dependencies;
- linting with `flake8`;
- automated tests with `unittest`;
- code coverage measurement with `coverage`.

The wording should connect these choices to integration reliability and regression prevention.

### 3. Containerization explanation

Explain the Docker setup in concrete terms:

- `python:3.12.8-slim` image;
- dependency installation inside the image;
- non-privileged runtime user;
- exposed port and runtime command;
- `docker compose up --build` for reproducible local startup.

The wording should connect this to portability, environment consistency, and easier deployment.

### 4. Deployment framing

Explain the deployment story carefully.

What can be claimed:

- the repository prepares an application for deployment by producing a containerized artifact;
- the documentation shows how to build and push the image to a registry;
- the CI workflow industrializes validation before delivery.

What should not be claimed:

- no fully automated production deployment is visible in the repository;
- no orchestrator or cloud runtime is configured in the repository itself.

The final wording should therefore present the project as a realistic CI/CD foundation rather than a complete production platform.

### 5. Bloc 2 evidence table update

Replace the placeholder line:

- current: `A completer (partie DevOps \& MLOps à rédiger).`

With a concrete summary tying the competency to `fizzbuzz-Efrei`:

- automated validation by GitHub Actions;
- tests and coverage;
- linting;
- Docker image build and reproducible execution with Compose;
- preparation for deployment through container packaging.

## Insertion Point in `main.tex`

Insert the new DevOps subsection in Bloc 2 after the current Spark presentation and before `\subsection{Analyse attendue}`.

Update only the final row of the Bloc 2 proof table unless a small wording adjustment elsewhere is necessary for coherence.

## Writing Constraints

- Use `nous` consistently.
- Keep the tone aligned with the rest of `main.tex`: explanatory, academic, and evidence-driven.
- Stay close to the repository contents.
- Do not invent infrastructure that is not present in the repository.
- Keep the section to about one page.

## Expected Outcome

After implementation, Bloc 2 will justify the DevOps/CI-CD competency with a concrete repository example, while keeping Spark as the main example for distributed data processing.
