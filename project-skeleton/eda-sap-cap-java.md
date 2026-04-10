# EDA SAP CAP Java Project Skeleton

## Recommended structure

```text
eda-sap-cap-java/
├── db/
├── srv/
├── app/
├── src/main/java/com/example/cap/
│   ├── handlers/
│   ├── application/
│   ├── domain/
│   ├── infrastructure/
│   └── shared/
└── src/test/java/
```

## CAP-specific rules
- keep CDS model first-class
- handlers are adapters, not the whole business layer
- use `Before`, `On`, and `After` phases intentionally
