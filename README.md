**English** | [Русский](README.ru.md)

# eShopOnWeb Integration Testing

**eShopOnWeb Integration Testing** is an integration and E2E testing project for the open-source **Microsoft eShopOnWeb** application.

The eShopOnWeb source code is not copied into this repository. It contains only my testing artifacts: strategy, test plan, test cases, Postman smoke collection, findings, report, and supporting instructions.

## System under test

Microsoft eShopOnWeb is an ASP.NET Core reference application with a catalog, basket, checkout, Identity authentication, an admin interface, and a Public API.

Original project:

```text
https://github.com/dotnet-architecture/eShopOnWeb
```

## My contributions

The project includes:

- integration test plan;
- a Big Bang Integration Testing strategy;
- manual test cases;
- an E2E checklist for key user workflows;
- Postman smoke collection;
- a register of findings and risks;
- security checklist;
- a final test report;
- environment setup instructions;
- helper scripts for starting the application;
- CI validation of the testing artifact structure.

## Structure

```text
eshoponweb-integration-testing/
├── docs/
│   ├── environment.md
│   ├── security-checklist.md
│   ├── test-cases.md
│   ├── test-plan.md
│   └── test-strategy.md
├── checklists/
│   └── e2e-checklist.md
├── postman/
├── reports/
│   ├── anomalies.md
│   ├── findings.csv
│   ├── findings.md
│   └── test-report.md
├── scripts/
├── tools/
│   └── validate_artifacts.py
├── .github/workflows/ci.yml
└── README.md
```

## Approach

The educational analysis uses **Big Bang Integration Testing**: the application is treated as an already integrated system, and checks focus on end-to-end workflows.

Coverage includes:

- catalog access and functionality;
- filtering and pagination;
- basket;
- authentication;
- checkout;
- order history;
- administration;
- basic API/smoke checks through Postman.

The approach's limitations are also documented: a failure in a long E2E flow makes the faulty component harder to isolate, so the report recommends further decomposition of the tests.

## Quick start

Clone the repository:

```bash
git clone https://github.com/nikamurkaa/eshoponweb-integration-testing.git
cd eshoponweb-integration-testing
```

Clone the original application separately:

```bash
cd ..
git clone https://github.com/dotnet-architecture/eShopOnWeb.git
```

Recommended directory structure:

```text
workspace/
├── eShopOnWeb/
└── eshoponweb-integration-testing/
```

Start the original project from the `eShopOnWeb` directory:

```bash
cd eShopOnWeb
docker compose build
docker compose up
```

Web: http://localhost:5106, Public API: http://localhost:5200.
For SQL Server setup or in-memory mode, see
[`docs/environment.md`](docs/environment.md). The Microsoft repository is archived;
to make the report reproducible, record the SHA actually tested using
`git rev-parse HEAD`. Do not carry results across revisions without retesting.

The `scripts/run-eshoponweb.ps1` and
`scripts/run-eshoponweb.sh` helpers are also available from this repository; they start Web through .NET after database setup.

After startup, import the following into Postman:

```text
postman/eshoponweb.smoke.postman_collection.json
postman/eshoponweb.local.postman_environment.json
```

## Key artifacts

1. [`docs/test-plan.md`](docs/test-plan.md) — testing scope and objectives.
2. [`docs/test-strategy.md`](docs/test-strategy.md) — selected integration approach and limitations.
3. [`docs/test-cases.md`](docs/test-cases.md) — manual scenarios.
4. [`checklists/e2e-checklist.md`](checklists/e2e-checklist.md) — E2E coverage.
5. [`reports/findings.md`](reports/findings.md) — identified issues and risks.
6. [`reports/test-report.md`](reports/test-report.md) — final conclusions.
7. [`docs/security-checklist.md`](docs/security-checklist.md) — security-oriented checks.

## Artifact validation

```bash
python tools/validate_artifacts.py
```

The CI workflow also validates the project structure automatically.

## Status

The project is complete. Its main technical focus is **integration testing, E2E, API testing, test design, and technical documentation**.

## Author

[Nicole Zhurbenko](https://github.com/nikamurkaa)
