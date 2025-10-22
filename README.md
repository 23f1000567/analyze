# Python Data Processing & CI/CD Project

This repository contains a Python-based data processing solution designed to transform Excel data into a structured JSON output, coupled with a robust Continuous Integration/Continuous Deployment (CI/CD) pipeline using GitHub Actions.

## Project Overview

-   **`execute.py`**: A Python script responsible for reading, processing, and aggregating data from an Excel file.
-   **`data.xlsx`**: The source Excel file containing the raw data to be processed.
-   **`data.csv`**: A CSV version of `data.xlsx`, generated and committed for ease of use or as an intermediate step.
-   **`.github/workflows/ci.yml`**: Defines the CI/CD pipeline using GitHub Actions, ensuring code quality and automated data processing and deployment.
-   **`result.json`**: The output of `execute.py`, containing the processed data in JSON format, which is generated during CI and published to GitHub Pages.

## Features

-   **Automated Data Conversion**: Converts `data.xlsx` to `data.csv`.
-   **Intelligent Data Processing**: `execute.py` handles potential data inconsistencies (e.g., non-numeric values in numeric columns) by converting them to appropriate types, ensuring robust aggregation.
-   **Code Quality Enforcement**: Integrates [Ruff](https://beta.ruff.rs/docs/) for fast Python linting, ensuring high code quality standards.
-   **Automated Testing & Generation**: The CI pipeline automatically runs the processing script upon pushes to `main`.
-   **GitHub Pages Deployment**: The generated `result.json` is published via GitHub Pages, making the processed data easily accessible online.
-   **Responsive Frontend**: A simple, responsive `index.html` (using Tailwind CSS) provides a basic web presence for the project.

## Setup and Local Execution

To run the `execute.py` script locally, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-name>
    ```

2.  **Set up Python Environment:**
    Ensure you have Python 3.11+ installed. It's recommended to use a virtual environment.
    ```bash
    python -m venv .venv
    source .venv/bin/activate  # On Windows: .venv\Scripts\activate
    ```

3.  **Install Dependencies:**
    ```bash
    pip install pandas==2.3.0 ruff
    ```

4.  **Prepare Data (if `data.csv` is not committed or needs regeneration):**
    The project expects `data.xlsx` and converts it to `data.csv`. If `data.csv` is missing or outdated, you can regenerate it (though in this project it's committed):
    ```bash
    python -c "import pandas as pd; df = pd.read_excel('data.xlsx'); df.to_csv('data.csv', index=False)"
    ```

5.  **Run the Python Script:**
    ```bash
    python execute.py > result.json
    ```
    This will execute the data processing logic and save the output to `result.json` in the current directory.

## CI/CD Workflow (`.github/workflows/ci.yml`)

The GitHub Actions workflow automates the following steps on `push` to `main` and `pull_request` to `main`:

1.  **Checkout Repository**: Retrieves the latest code.
2.  **Setup Python 3.11**: Configures the Python environment.
3.  **Install Dependencies**: Installs `pandas` and `ruff`.
4.  **Convert `data.xlsx` to `data.csv`**: Ensures `data.csv` is available for `execute.py`.
5.  **Run Ruff Linter**: Performs static code analysis on `execute.py` and other Python files, displaying results in the CI log.
6.  **Execute Python Script**: Runs `python execute.py` and redirects its output to `result.json`.
7.  **Upload `result.json` as Artifact**: Stores `result.json` as a build artifact for later use.
8.  **Deploy to GitHub Pages**: Uses the `result.json` artifact to publish the processed data onto GitHub Pages, making it publicly accessible (e.g., `https://<your-username>.github.io/<repository-name>/result.json`).

## License

This project is licensed under the MIT License - see the `LICENSE` file for details.