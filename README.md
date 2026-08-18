# Advanced Playwright Framework 2.x

A TypeScript-based end-to-end testing framework built with [Playwright](https://playwright.dev/). It includes environment-aware configuration, HTML reporting, and a set of supporting libraries for data handling, API assertions, logging, and test-data generation.

## Prerequisites

- Node.js 20 or later
- npm

## Setup

Install project dependencies and Playwright's Chromium browser:

```bash
npm install
npx playwright install chromium
```

## Run tests

The test suite is located in `src/tests` and is configured to run in Chromium.

```bash
npx playwright test
```

Useful variations:

```bash
npx playwright test --headed
npx playwright test src/tests/example.spec.ts
npx playwright test --debug
npx playwright show-report
```

On CI, failed tests are retried twice. Locally, tests are not retried by default.

## Configuration

The central Playwright settings live in `playwright.config.ts`:

- Test directory: `src/tests`
- Browser project: Chromium (Desktop Chrome device profile)
- Test timeout: 60 seconds
- Expect timeout: 10 seconds
- Execution: fully parallel
- Artifacts: screenshots on failure, plus video and trace for each run
- Reporters: HTML, list, and the configured custom reporter path `src/utils/CustomReporter.ts`

The custom reporter path is configured, but the corresponding source file is not currently present in this repository. Create it or remove that reporter entry before running tests if Playwright reports a module-resolution error.

## Environments

Configuration loads variables from `src/.env` using `dotenv`. `BASE_URL`, when provided, has priority over environment-specific URLs. Otherwise, `TTA_ENV` selects a target URL.

| `TTA_ENV` value | URL variable used | Default |
| --- | --- | --- |
| `api` | `API_BASE_URL` | `https://restful-booker.herokuapp.com` |
| `dev` / `local` | `DEV_BASE_URL` | `http://localhost:3000` |
| `stg` / `stage` / `staging` | `STG_BASE_URL` | `https://stage.thetestingacademy.com` |
| `prod` / `production` | `PROD_BASE_URL` | `https://app.thetestingacademy.com` |
| `qa` or unset | `QA_BASE_URL` | `https://app.thetestingacademy.com` |

Example:

```powershell
$env:TTA_ENV = 'stg'
npx playwright test
```

Do not commit credentials or other secrets in `.env`; use your CI platform's protected environment variables for shared or production values.

## Project layout

```text
src/
  .env                  Local environment configuration
  tests/                Playwright test specifications
playwright.config.ts    Playwright projects, reporting, timeouts, and base URL logic
tsconfig.json           TypeScript compiler configuration and import aliases
```

TypeScript aliases are available for future framework modules: `@api`, `@config`, `@fixtures`, `@pages`, `@testdata`, and `@utils`.

## Included tooling

| Package | Purpose |
| --- | --- |
| `@playwright/test` | Browser automation and test runner |
| `dotenv` | Environment-variable loading |
| `csv-parse`, `xlsx` | CSV and Excel test-data parsing |
| `@faker-js/faker` | Generated test data |
| `ajv`, `ajv-formats` | JSON-schema validation |
| `jsonpath-plus` | JSONPath queries |
| `winston` | Application/test logging |
| `allure-playwright` | Allure reporting integration |

## Reports and artifacts

After a test run, use `npx playwright show-report` to open the generated HTML report. Playwright output directories such as `playwright-report`, `test-results`, and trace/video artifacts are excluded from version control.

## Type checking

```bash
npx tsc --noEmit
```

