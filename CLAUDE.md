# Claude Code Instructions

## Overview

This repository is a TypeScript Playwright test-automation framework. Tests run from `src/tests` against the Chromium project configured in `playwright.config.ts`.

## Working in the Repository

- Put UI test specifications in `src/tests` and API test specifications in `src/tests/api`.
- Add page objects to `src/pages`, API clients to `src/api`, fixtures to `src/fixtures`, test data to `src/testdata`, and reusable helpers to `src/utils`.
- Use TypeScript path aliases from `tsconfig.json` (such as `@pages/*` and `@utils/*`) for framework imports.
- Preserve the existing TypeScript style: four-space indentation, single quotes, semicolons, and strict typing.

## Commands

```bash
npm install
npx playwright install chromium
npx playwright test
npx playwright test --headed
npx playwright show-report
npx tsc --noEmit
```

Run the smallest relevant test file while developing, then run the full suite when practical. Inspect the HTML report, trace, screenshots, and video artifacts for failures.

## Test Practices

- Write independent, parallel-safe tests using `@playwright/test`.
- Prefer accessible role, label, and text locators over brittle selectors.
- Name files `*.spec.ts` and use behavior-oriented test names.
- Make assertions on visible user outcomes; use fixtures or API helpers for setup where appropriate.

## Configuration and Security

`dotenv` loads `src/.env`; `BASE_URL` overrides environment-specific URLs selected by `TTA_ENV`. Never commit credentials, tokens, or production secrets. Keep local values in `src/.env` and use protected CI variables for shared environments.

## Before Finishing

Confirm modified tests pass and run `npx tsc --noEmit` when configuration permits. Do not edit generated output directories such as `playwright-report`, `test-results`, or `node_modules`.
