# Public Standard

This page is the shortest possible version of the repository.

## Core principles

- 4-Eyes Principle
- SOLID
- DRY
- YAGNI
- KISS

## Naming standard

| Language | Folder / Package | File Name | Property |
|---|---|---|---|
| Java | lowercase reverse-domain package | `PascalCase.java` | `camelCase` |
| Node.js | lowercase, prefer `kebab-case` | lowercase, prefer `kebab-case.js` | `camelCase` |
| Python | lowercase, prefer `snake_case` | `snake_case.py` | `snake_case` |
| SAP ABAP | SAP namespace + object convention | mirror repository object naming | descriptive names for local code; keep SAP prefixes where required |
| SAP CDS | namespace + RAP/VDM object prefix when applicable | file matches main artifact | artifact readable, elements usually `camelCase` |
| SAP UI5 | standard `webapp` structure + stable namespace | `.controller.js`, `.view.xml`, `.fragment.xml` suffixes | `camelCase` |

## References

See [../REFERENCES.md](../REFERENCES.md) for the primary sources used by this repository.
