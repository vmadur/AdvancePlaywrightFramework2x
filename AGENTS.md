# Repository Guidelines

## Project Structure & Module Organization

This is a TypeScript Playwright automation framework. Keep executable tests in `src/tests`; place API-focused specifications in `src/tests/api`. Organize reusable framework code by concern: API clients in `src/api`, page objects in `src/pages`, fixtures in `src/fixtures`, environment/configuration helpers in `src/config`, test data in `src/testdata`, and shared utilities/reporting code in `src/utils`. Use the aliases declared in `tsconfig.json` (for example, `@pages/*` and `@utils/*`) instead of long relative imports. Keep design notes in `docs/` and repository rules in `rules/`.

## Build, Test, and Development Commands

Install dependencies with `npm install`, then install the configured browser with `npx playwright install chromium`.

```bash
npx playwright test                 # Run all Chromium tests
npx playwright test --headed        # Run with a visible browser
npx playwright test src/tests/example.spec.ts
npx playwright show-report          # Open the HTML report
npx tsc --noEmit                    # Type-check without emitting files
```

Playwright settings—including timeouts, reporters, screenshots, video, traces, and environment URL selection—are in `playwright.config.ts`.

## Coding Style & Naming Conventions

Use TypeScript with strict compiler settings. Follow the existing four-space indentation, single quotes, semicolons, and explicit imports. Name test files `*.spec.ts`; give tests behavior-focused names such as `test('user can create a booking', ...)`. Name page objects with a `Page` suffix (for example, `LoginPage.ts`) and helpers with a descriptive noun or verb. There is no configured formatter or linter, so keep changes stylistically consistent and use `npx tsc --noEmit` before submitting.

## Testing Guidelines

Use `@playwright/test` with independent, parallel-safe tests. Prefer role- and label-based locators over brittle CSS/XPath selectors. Set test data up through fixtures or API helpers where possible, and make assertions about observable user outcomes. Attach useful trace, video, or screenshot evidence when diagnosing failures. No coverage threshold is configured; add coverage only when the project adopts a coverage tool.

## Commit & Pull Request Guidelines

This repository has no commit history yet; use concise, imperative Conventional Commit-style messages, such as `feat: add booking API client` or `test: cover invalid login`. Keep each commit focused. Pull requests should describe the behavior change, list test commands run, link relevant issues, and include report screenshots or traces for UI-affecting changes.

## Security & Configuration

Local values belong in `src/.env`, which is ignored by Git. Never commit credentials, tokens, or production secrets. Use CI-provided protected variables for shared environments.
