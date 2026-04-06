# UI Automation Testing Framework

Enterprise-grade UI automation testing framework built with **Playwright** + **Python** + **Pytest**.

## Overview

A modern, scalable, and maintainable UI automation testing solution designed for enterprise applications. This framework follows industry best practices including Page Object Model (POM) pattern, layered architecture, and data-driven testing.

## Tech Stack

| Category | Technology |
|----------|------------|
| Framework | Playwright 1.40 |
| Language | Python 3.9+ |
| Test Runner | Pytest 7.2+ |
| Reporting | Pytest HTML |
| Data Validation | Pydantic 2.5 |
| Configuration | PyYAML |

## Architecture

```
UI_Auto_demo/
├── core/                       # Core Layer
│   ├── base_page.py           # BasePage - Page Object Model base class
│   ├── logger.py              # Logging utilities
│   ├── custom_assertions.py   # Custom assertion methods
│   └── data_models.py         # Pydantic data models
├── pages/                      # Page Object Layer
│   ├── login_page.py          # Login page object
│   ├── dashboard_page.py      # Dashboard page object
│   └── components/            # Reusable UI components
├── tests/                      # Test Cases Layer
│   ├── conftest.py           # Pytest fixtures and configuration
│   └── smoke/
│       └── test_login.py     # Login functionality tests
├── data/                       # Data Layer
│   ├── users.json            # User test data
│   ├── config.yaml           # Environment configurations
│   └── demo_app.html         # Demo application for testing
├── helpers/                    # Helper Utilities
│   └── data_generator.py     # Test data generator
├── reports/                    # Test Reports
├── screenshots/               # Failure screenshots
├── traces/                     # Playwright traces
├── pytest.ini                 # Pytest configuration
├── requirements.txt           # Python dependencies
└── .env                      # Environment variables
```

## Features

### Core Principles

- **Robustness**: Intelligent waiting mechanisms, no flaky tests
- **Maintainability**: Clean code architecture with POM pattern
- **Scalability**: Modular design for easy expansion

### Key Features

- Page Object Model (POM) architecture
- Data-driven testing with JSON/YAML
- Multi-environment support (staging, production, development, demo)
- Automatic screenshot capture on failure
- Playwright trace viewer support
- Comprehensive HTML test reports
- Custom assertions library
- Test data generation utilities

## Installation

### Prerequisites

- Python 3.9+
- pip

### Setup

```bash
# Clone the repository
git clone https://github.com/cylDemo/UI_Auto_demo.git
cd UI_Auto_demo

# Install dependencies
pip install -r requirements.txt

# Install Playwright browsers
playwright install chromium
```

## Configuration

### Environment Variables (.env)

```env
BASE_URL=https://staging.example.com
HEADLESS=false
CI=false
TIMEOUT=30000
RETRY_COUNT=2
PARALLEL_WORKERS=4
ENV=demo
```

### Environment Config (data/config.yaml)

Supported environments: `staging`, `production`, `development`, `demo`

## Usage

### Run All Tests

```bash
python -m pytest tests/smoke/test_login.py -v
```

### Run by Marker

```bash
# Smoke tests only
python -m pytest -m smoke -v

# Regression tests only
python -m pytest -m regression -v

# By priority
python -m pytest -m P0 -v
```

### Generate HTML Report

```bash
python -m pytest --html=reports/pytest-report.html --self-contained-html
```

### Parallel Execution

```bash
python -m pytest -n 4
```

## Test Cases

### Login Tests (Smoke)

| Test Case | Priority | Description |
|-----------|----------|-------------|
| `test_login_success` | P0 | Verify successful login with valid credentials |
| `test_login_page_elements` | P0 | Verify all login page elements are visible |
| `test_login_button_state` | P0 | Verify login button is enabled |

### Login Tests (Regression)

| Test Case | Priority | Description |
|-----------|----------|-------------|
| `test_login_failed_with_invalid_password` | P1 | Verify error message for invalid password |
| `test_login_failed_with_nonexistent_user` | P1 | Verify error message for non-existent user |
| `test_login_empty_fields` | P2 | Verify validation for empty username/password |

### Dashboard Tests

| Test Case | Priority | Description |
|-----------|----------|-------------|
| `test_dashboard_elements_visible` | P2 | Verify dashboard elements after login |
| `test_logout` | P2 | Verify logout functionality |

## Test Data

### Valid User Credentials

```json
{
  "username": "testuser@example.com",
  "password": "Test123456"
}
```

### Demo Application

A demo login application is included at `data/demo_app.html` for testing purposes.

## Project Structure Details

### Core Layer (`core/`)

- **base_page.py**: Base class for all Page Objects providing common methods
- **logger.py**: Centralized logging configuration
- **custom_assertions.py**: Reusable assertion methods
- **data_models.py**: Pydantic models for data validation

### Page Object Layer (`pages/`)

- **login_page.py**: Login page locators and actions
- **dashboard_page.py**: Dashboard page locators and actions

### Test Layer (`tests/`)

- **conftest.py**: Pytest fixtures, hooks, and configuration
- **test_login.py**: Login functionality test cases

### Data Layer (`data/`)

- **users.json**: User credentials and test data
- **config.yaml**: Environment-specific configurations

## CI/CD Integration

### GitHub Actions Example

```yaml
name: UI Automation Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          playwright install chromium
      - name: Run tests
        run: pytest --workers=4
```

## Best Practices

1. **Always use Page Object Model** - Never write `page.locator()` in test files
2. **No hardcoded data** - Use JSON/YAML files for test data
3. **Smart waits** - Use Playwright's auto-wait instead of `time.sleep()`
4. **Descriptive naming** - Use clear, descriptive test names
5. **Atomic tests** - Each test should be independent
6. **Failure screenshots** - Enable automatic screenshot capture

## Quality Metrics

| Metric | Target |
|--------|--------|
| Pass Rate | >= 98% |
| Execution Time | < 15 min (full suite) |
| Flaky Rate | < 2% |
| Code Coverage | >= 80% |

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## License

MIT License

## Support

For questions or issues, please open an issue on GitHub.
