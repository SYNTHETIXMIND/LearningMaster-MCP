```markdown
# Technology Context - LearningMaster-MCP

This document outlines the technologies, tools, development environment, testing strategy, deployment process, and continuous integration approach used for the LearningMaster-MCP project.

## Technologies Used

*   **Programming Language:** Python 3.11
*   **Framework:** FastAPI (for building the API)
*   **Database:** Notion API (as a data source, not a traditional database management system)
*   **Data Serialization:** JSON
*   **Asynchronous Programming:** `asyncio` (for handling concurrent requests)
*   **HTTP Client:** `httpx` (for making requests to the Notion API)
*   **Environment Variables:** `python-dotenv` (for managing API keys and other sensitive information)
*   **Data Validation and Serialization:** Pydantic
*   **Logging:** Python's `logging` module

## Software Development Tools

*   **IDE:** Visual Studio Code (VS Code) with the following extensions:
    *   Python extension for code completion, linting, and debugging.
    *   Pylance for enhanced Python language support.
    *   Black formatter for code formatting.
    *   isort for import sorting.
*   **Version Control:** Git (hosted on GitHub)
*   **Package Manager:** pip (with `venv` for virtual environment management)
*   **Documentation Generator:** MkDocs with Material for MkDocs theme
*   **Task Management:** GitHub Issues and Projects
*   **Communication:** Slack

## Development Environment

*   **Operating System:** macOS (developers), Ubuntu Server (production)
*   **Virtual Environment:** Python's `venv` used for dependency isolation. Each developer will create their own virtual environment.
    *   Creation: `python3 -m venv .venv`
    *   Activation: `source .venv/bin/activate`
*   **Configuration:** Environment variables stored in a `.env` file (not committed to version control).  Example:
    ```
    NOTION_API_KEY=secret_key
    DATABASE_ID=database_id
    ```
*   **Coding Standards:** Follow PEP 8 guidelines. Code will be formatted using Black and imports sorted using isort.

## Testing Strategy

*   **Unit Tests:** Using `pytest` framework.  Focus on testing individual functions and classes in isolation.  Aim for high code coverage.
*   **Integration Tests:** Testing the interaction between different components, particularly the FastAPI endpoints and the Notion API. Mocking the Notion API will be used to avoid rate limits and dependency on external services during testing.
*   **End-to-End (E2E) Tests:** Testing the entire application flow from the API endpoint to the Notion database and back. These tests will be more limited in scope due to the complexity of managing a real Notion database during testing.
*   **Test Data:** Mock data will be used extensively for unit and integration tests.  For E2E tests, a dedicated test Notion database will be used.
*   **Test Coverage:**  Tracked using `pytest-cov`. Aim for at least 80% code coverage.
*   **Continuous Integration:** Tests will be run automatically on every push to the main branch using GitHub Actions.

## Deployment Process

*   **Environment:** Ubuntu Server (cloud provider - AWS, GCP, or Azure will be determined later).
*   **Containerization:** Docker will be used to package the application and its dependencies.
*   **Orchestration:** Docker Compose will be used for managing the application container.
*   **Deployment Steps:**
    1.  Build the Docker image.
    2.  Push the Docker image to a container registry (e.g., Docker Hub).
    3.  Pull the Docker image from the registry to the production server.
    4.  Run the Docker container using Docker Compose.
    5.  Monitor the application logs and health.
*   **Infrastructure as Code (IaC):** Terraform (planned for future iterations) will be used to manage the infrastructure.
*   **Monitoring:** Prometheus and Grafana (planned for future iterations) will be used for monitoring the application and infrastructure.

## Continuous Integration Approach

*   **Platform:** GitHub Actions
*   **Workflow:**
    1.  On every push to the `main` branch:
        *   Run linters and formatters (Black, isort, Pylint).
        *   Run unit tests and integration tests with `pytest`.
        *   Calculate code coverage.
        *   Build the Docker image.
        *   Push the Docker image to Docker Hub (or a private container registry).
    2.  On every pull request to the `main` branch:
        *   Run the same checks as on push.
        *   Prevent merging if any checks fail.
*   **Artifacts:** Docker images will be stored as artifacts.
*   **Notifications:** Slack notifications will be sent on build failures.

Created on 25.05.2025
```