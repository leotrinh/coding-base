# React Clean Architecture Project Skeleton

## Recommended structure

```text
react-clean-architecture/
├── public/
├── src/
│   ├── app/
│   ├── core/
│   ├── domain/
│   ├── application/
│   ├── infrastructure/
│   ├── presentation/
│   ├── ui/
│   ├── state/
│   └── test/
└── docs/
```

## Dependency rule

```text
ui -> presentation -> application -> domain
infrastructure -> application/domain contracts
app -> ui + composition
```
