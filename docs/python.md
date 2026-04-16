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

## CLASS Examples

### 1. Plain Class Declaration
```python
class SalesOrder:
    pass
```

### 2. Class with Constructor
```python
class SalesOrder:
    def __init__(self, sales_order_id: str, created_at: str) -> None:
        self.sales_order_id = sales_order_id
        self.created_at = created_at
        self._retry_count = 0  # protected
```

### 3. Class Properties (public, private)
```python
class SalesOrder:
    def __init__(self, sales_order_id: str) -> None:
        self.sales_order_id = sales_order_id  # public
        self._internal_state = None           # protected
        self.__secret = None                  # private (name-mangled)
```

### 4. Static Fields / Methods
```python
class SalesOrder:
    _count: int = 0  # class variable / static field

    @staticmethod
    def get_next_id() -> int:
        SalesOrder._count += 1
        return SalesOrder._count
```

### 5. Abstract Class
```python
from abc import ABC, abstractmethod

class OrderService(ABC):
    @abstractmethod
    def process(self, order: SalesOrder) -> None:
        pass
```

### 6. Interface (Protocol)
```python
from typing import Protocol

class OrderProcessor(Protocol):
    def process(self, order: SalesOrder) -> None: ...
    def can_handle(self, order_type: str) -> bool: ...
```

### 7. Enum
```python
from enum import Enum, auto

class OrderStatus(Enum):
    DRAFT = auto()
    ACTIVE = auto()
    COMPLETED = auto()

class OrderType(Enum):
    STANDARD = 0
    EXPRESS = 1
    BULK = 2
```

### 8. Generic Class
```python
from typing import Generic, TypeVar

T = TypeVar('T')

class Box(Generic[T]):
    def __init__(self, value: T) -> None:
        self._value = value

    def get(self) -> T:
        return self._value
```

## FUNCTION / METHOD Examples

### 1. Function Declaration
```python
def calculate_total(items: list[dict]) -> float:
    return sum(item['price'] for item in items)
```

### 2. Parameters Naming Convention
```python
def create_order(sales_order_id: str, customer_id: str, line_items: list) -> dict:
    return {
        'sales_order_id': sales_order_id,
        'customer_id': customer_id,
        'line_items': line_items
    }
```

### 3. Return Type
```python
def calculate_total(items: list[dict]) -> float:
    return sum(item['price'] for item in items)
```

### 4. Arrow Function (Lambda)
```python
calculate_total = lambda items: sum(item['price'] for item in items)
```

### 5. Async Function
```python
import asyncio

async def fetch_order(order_id: str) -> dict:
    await asyncio.sleep(0.1)  # simulate async call
    return {'id': order_id, 'status': 'ACTIVE'}
```

### 6. Generator Function
```python
def order_iterator(orders: list):
    for order in orders:
        yield order
```

### 7. Instance Method
```python
class SalesOrder:
    def get_id(self) -> str:
        return self.sales_order_id

    def set_status(self, status: str) -> None:
        self.status = status
```

### 8. Static Method
```python
class SalesOrder:
    @staticmethod
    def from_dict(data: dict) -> 'SalesOrder':
        return SalesOrder(data['sales_order_id'])
```
