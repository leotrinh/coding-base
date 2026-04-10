# EDA Java Spring Project Skeleton

## Recommended structure

```text
eda-java-spring/
├── docs/
├── src/main/java/com/example/ordering/
│   ├── OrderingApplication.java
│   ├── shared/
│   ├── ordering/
│   │   ├── api/
│   │   ├── application/
│   │   ├── domain/
│   │   ├── infrastructure/
│   │   └── contract/
│   ├── inventory/
│   └── billing/
└── src/test/
```

## Layer intent
- `api/` adapters only
- `application/` use cases and orchestration
- `domain/` business rules
- `infrastructure/` database, broker, external clients
- `contract/` public event/API contracts
