```markdown
# PROG8860 – CI/CD Assignment

A minimal Flask application with unit tests, Docker containerization, and a GitHub Actions pipeline.

---

## Prerequisites

- **Git** (v2.20+)
- **Python 3.11** (or higher)
- **Docker Desktop** (Linux‑container mode)
- A GitHub account with permissions to push branches and open pull requests

---

## Project Structure

```

prog8860-ci-cd/
├── .github/
│   └── workflows/
│       └── sumanth-ci-pipeline.yml   # GitHub Actions workflow
├── app/
│   ├── Dockerfile                    # Docker build instructions
│   ├── requirements.txt              # Python dependencies (Flask, etc.)
│   ├── app.py                        # Flask application (single endpoint)
│   └── test\_app.py                   # Unit tests for the Flask app
└── README.md                         # This file

````

- **app/app.py**  
  Contains a basic Flask “Hello World” endpoint.
- **app/test_app.py**  
  Validates the Flask endpoint using Python’s `unittest`.
- **app/requirements.txt**  
  Lists required Python packages (e.g., `Flask==2.x`).
- **app/Dockerfile**  
  Builds a Docker image that installs dependencies and runs `app.py`.
- **.github/workflows/sumanth-ci-pipeline.yml**  
  Defines CI/CD steps: checkout, test, build Docker image, run container, cleanup.

---

## Local Setup & Testing

1. **Clone the repository**  
   ```bash
   git clone https://github.com/<your-username>/prog8860-ci-cd.git
   cd prog8860-ci-cd
````

2. **Checkout your assignment branch**

   ```bash
   git checkout -b assignment1-sumanth-9040660
   ```

3. **Install Python dependencies**

   ```bash
   cd app
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. **Run unit tests**

   ```bash
   python -m unittest test_app.py
   ```

   * Expected output:

     ```
     .
     ----------------------------------------------------------------------
     Ran 3 test in 0.00s

     OK
     ```
   * Fix any test failures before proceeding.

---

## Docker — Build & Run Locally

> All Docker commands assume you are in the **repository root** (where `README.md` is located).

1. **Build the Docker image**

   ```bash
   docker build -f app/Dockerfile -t flask-app app
   ```

   * `-f app/Dockerfile`: points Docker to the Dockerfile inside `app/`.
   * `app` (final argument): uses the `app/` folder as the build context.

2. **Run the container**

   ```bash
   docker run -d -p 5000:5000 --name flask-app flask-app
   ```

   * Maps host port 5000 → container port 5000.
   * Run `docker ps` to verify that `flask-app` is “Up”.

3. **Verify the app**

   * Open your browser to `http://localhost:5000/`.
   * You should see “Hello, world!” (or equivalent response from `app.py`).

4. **Stop & remove the container**

   ```bash
   docker stop flask-app
   docker rm flask-app
   ```

   * After stopping, `docker ps -a` should show `flask-app` in an `Exited` state (or it may disappear after removal).

---

## Git & GitHub Flow

1. **Stage, commit, and push changes**

   ```bash
   cd ..
   git add .
   git commit -m "Complete CI/CD assignment"
   git push origin assignment1-sumanth-9040660
   ```

2. **Create a Pull Request**

   * Navigate to your GitHub repository.
   * Click **Pull requests → New pull request**.

     * **Base branch**: `main`
     * **Compare branch**: `assignment1-sumanth-9040660`
   * Title your PR:

     ```
     Assignment 1: CI/CD pipeline setup (Flask + Docker + GitHub Actions)
     ```
   * Add your instructor (or designated reviewer) as a reviewer.
   * Click **Create pull request**.

---

## CI/CD Pipeline Overview

File: `.github/workflows/sumanth-ci-pipeline.yml`

This workflow automatically runs on every push or pull request to the `assignment1-sumanth-9040660` branch. Its steps are:

1. **Checkout Code**
   Uses `actions/checkout@v3`.

2. **Setup Python 3.11**
   Uses `actions/setup-python@v4`.

3. **Install Dependencies**
   Runs:

   ```bash
   pip install -r app/requirements.txt
   ```

4. **Run Unit Tests**
   Runs:

   ```bash
   python -m unittest app/test_app.py
   ```

5. **Setup Docker Buildx**
   Uses `docker/setup-buildx-action@v2`.

6. **Build Docker Image**

   ```bash
   docker build -f app/Dockerfile -t flask-app app
   ```

7. **Run Docker Container**

   ```bash
   docker run -d -p 5000:5000 --name flask-app flask-app
   ```

8. **Show Running Containers**
   Displays:

   ```bash
   docker ps
   ```

9. **Stop & Remove Container**

   ```bash
   docker stop flask-app
   docker rm flask-app
   ```

All steps must succeed for the workflow to complete. A green checkmark indicates a successful pipeline.



## Common Commands Reference

```bash
# Clone & create assignment branch
git clone https://github.com/<username>/prog8860-ci-cd.git
cd prog8860-ci-cd
git checkout -b assignment1-sumanth-9040660

# Install Python dependencies (locally)
cd app
pip install --upgrade pip
pip install -r requirements.txt

# Run unit tests
python -m unittest test_app.py

# Build Docker image
# (run from repo root)
docker build -f app/Dockerfile -t flask-app app

# Run Docker container
docker run -d -p 5000:5000 --name flask-app flask-app

# Verify container is running
docker ps

# Stop & remove container
docker stop flask-app
docker rm flask-app

# Commit & push changes
cd ..
git add .
git commit -m "Complete CI/CD assignment"
git push origin assignment1-sumanth-9040660
```


