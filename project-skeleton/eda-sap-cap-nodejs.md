# EDA SAP CAP Node.js Project Skeleton

## Recommended structure

```text
eda-sap-cap-nodejs/
├── app/
├── db/
├── srv/
│   ├── service.cds
│   ├── handlers/
│   ├── application/
│   ├── domain/
│   ├── infrastructure/
│   └── server.js
└── test/
```

## CAP-specific structure rules
- keep standard CAP folders: `db/`, `srv/`, `app/`
- `srv/handlers` is the adapter layer
- `srv/application` is orchestration
- `srv/domain` is pure business logic
- `srv/infrastructure` is concrete integration
