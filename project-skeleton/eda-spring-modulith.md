# EDA Spring Modulith Project Skeleton

## Recommended structure

```text
eda-spring-modulith/
├── docs/
├── src/main/java/com/example/shop/
│   ├── ShopApplication.java
│   ├── shared/
│   ├── ordering/
│   │   ├── api/
│   │   ├── application/
│   │   ├── domain/
│   │   └── internal/
│   ├── inventory/
│   └── billing/
└── src/test/
```

## Modulith-specific guidance
- organize by application module
- use package boundaries intentionally
- prefer application events for cross-module collaboration
