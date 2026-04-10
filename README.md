# Coding Naming Convention

A public, opinionated, and review-friendly engineering standards pack for:

- Java
- Node.js
- Python
- SAP ABAP
- SAP CDS
- SAP UI5

It also includes:

- project skeleton guides
- architecture review checklists
- event catalog templates
- ADR templates
- public standards and contribution guidelines

**Author:** Leo  
**Git:** https://github.com/leotrinh/coding-base

---

## Why this repository exists

This repository is meant to be a **public standard pack** that teams can use for:

- consistent naming
- cleaner project structure
- easier code reviews
- safer architecture decisions
- better onboarding

This repo follows one core rule:

> Use the native ecosystem style first. Do not force one naming style across all languages.

---

## Naming styles reference

| Style | Example |
|---|---|
| PascalCase | `CustomerOrder` |
| camelCase | `customerOrder` |
| snake_case | `customer_order` |
| kebab-case | `customer-order` |
| flatcase | `customerorder` |
| SCREAMING_SNAKE_CASE | `CUSTOMER_ORDER` |
| Train-Case | `Customer-Order` |
| COBOL-CASE | `CUSTOMER-ORDER` |

---

## Naming standard

| Language | Folder / Package | File Name | Property |
|---|---|---|---|
| Java | lowercase reverse-domain package | `PascalCase.java` | `camelCase` |
| Node.js | lowercase, prefer `kebab-case` | lowercase, prefer `kebab-case.js` | `camelCase` |
| Python | lowercase, prefer `snake_case` | `snake_case.py` | `snake_case` |
| SAP ABAP | SAP namespace + object convention | mirror repository object naming | descriptive local names; keep SAP prefixes where required |
| SAP CDS | namespace + RAP/VDM object prefixes when applicable | file matches main artifact | business-readable artifact name, elements usually `camelCase` |
| SAP UI5 | standard `webapp` structure + stable namespace | `.controller.js`, `.view.xml`, `.fragment.xml` suffixes | `camelCase` |

---

## Language guides

- [Java](docs/java.md)
- [Node.js](docs/nodejs.md)
- [Python](docs/python.md)
- [SAP ABAP](docs/sap-abap.md)
- [SAP CDS](docs/sap-cds.md)
- [SAP UI5](docs/sap-ui5.md)

---

## Project skeleton guides

Core templates:
- [Architecture Review Checklist](project-skeleton/architecture-review-checklist.md)
- [Event Catalog Template](project-skeleton/event-catalog-template.md)
- [ADR Template](project-skeleton/adr-template.md)

Architecture skeletons:
- [EDA Java Spring](project-skeleton/eda-java-spring.md)
- [EDA Node.js](project-skeleton/eda-nodejs.md)
- [EDA SAP CAP Java](project-skeleton/eda-sap-cap-java.md)
- [EDA SAP CAP Node.js](project-skeleton/eda-sap-cap-nodejs.md)
- [EDA Spring Modulith](project-skeleton/eda-spring-modulith.md)
- [EDA NestJS](project-skeleton/eda-nestjs.md)
- [Clean FastAPI](project-skeleton/clean-fastapi.md)
- [React Clean Architecture](project-skeleton/react-clean-architecture.md)
- [React Vite Clean Architecture](project-skeleton/react-vite-clean-architecture.md)

---

## Repo governance and meta docs

- [Contributing](CONTRIBUTING.md)
- [Engineering Principles](docs/principles.md)
- [Public Standard](docs/public-standard.md)
- [Repository Map](docs/repository-map.md)
- [References](REFERENCES.md)

---

## Example trees

- [Java Spring EDA Tree](docs/examples/java-spring-eda-tree.md)
- [SAP CAP Node.js Tree](docs/examples/sap-cap-nodejs-tree.md)
- [React Next Clean Tree](docs/examples/react-next-clean-tree.md)
