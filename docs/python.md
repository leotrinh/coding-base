# Python Naming Convention

## Standard

| Target | Convention | Example |
|---|---|---|
| Package / Folder | lowercase, usually `snake_case` | `sales`, `sales_order` |
| File Name | `snake_case.py` | `sales_order_service.py` |
| Property | `snake_case` | `sales_order_id`, `created_at`, `retry_count` |

## Rules

### Package / Folder
- package names should be short and lowercase
- use underscores only when readability improves
- avoid hyphens

### File Name
- use `snake_case.py`
- keep module names import-friendly

### Property
- use `snake_case`
- constants use `SCREAMING_SNAKE_CASE`
- class names remain `PascalCase`

## Good
```python
class SalesOrder:
    def __init__(self, sales_order_id: str, created_at: str) -> None:
        self.sales_order_id = sales_order_id
        self.created_at = created_at
        self.retry_count = 0

MAX_RETRY_COUNT = 3
```

## Bad
```python
class SalesOrder:
    def __init__(self, salesOrderId, createdAt):
        self.salesOrderId = salesOrderId
        self.createdAt = createdAt
```
