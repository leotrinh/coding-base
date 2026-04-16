# Node.js Naming Convention

## Standard

| Target | Convention | Example |
|---|---|---|
| Folder / Package | lowercase, prefer `kebab-case` | `sales-order`, `customer-api` |
| File Name | lowercase, prefer `kebab-case.js` or PascalCase `UserService.js` | `sales-order.service.js`, `auth-middleware.js`, `UserService.js` |
| Class | `PascalCase` | `UserServiceImpl` |
| Property/ Func | `camelCase` | `salesOrderId`, `createdAt`, `retryCount` |
> Node.js itself does not define one universal internal source-file naming style for applications.  
> This guide adopts `kebab-case` for folders and files as the public team standard.

## Rules

### Folder / Package
- use lowercase only
- prefer `kebab-case`
- avoid spaces and uppercase

### File Name
- use lowercase
- prefer `kebab-case`
- keep suffixes meaningful

### Property
- use `camelCase`
- constants may use `SCREAMING_SNAKE_CASE`
- booleans should read like flags: `isActive`, `hasAccess`

## Good
```javascript
const payload = {
  salesOrderId: "SO-1001",
  customerId: "C-1001",
  retryCount: 2,
  isActive: true
};
```

## Bad
```javascript
const payload = {
  SALES_ORDER_ID: "SO-1001",
  customer_id: "C-1001",
  RetryCount: 2
};
```

## CLASS Examples

### 1. Plain Class Declaration
```javascript
class SalesOrder {
  // body
}
```

### 2. Class with Constructor
```javascript
class SalesOrder {
  constructor(id, status) {
    this.id = id;
    this.status = status;
  }
}
```

### 3. Class Properties (public, private)
```javascript
class SalesOrder {
  id;        // public
  #secret;   // private (ES2022+)
}
```

### 4. Static Fields / Methods
```javascript
class SalesOrder {
  static count = 0;

  static getNextId() {
    return ++SalesOrder.count;
  }
}
```

### 5. Abstract Class
```javascript
// Use experimental syntax or TypeScript for abstract classes
// Abstract class pattern using constructor protection
class BaseService {
  constructor() {
    if (new.target === BaseService) {
      throw new Error('Cannot instantiate abstract class');
    }
  }
  process() {
    throw new Error('Abstract method must be implemented');
  }
}
```

### 6. Interface (TypeScript)
```typescript
interface OrderProcessor {
  process(order: SalesOrder): Promise<void>;
  canHandle(orderType: string): boolean;
}
```

### 7. Enum
```javascript
const OrderStatus = Object.freeze({
  Draft: 'DRAFT',
  Active: 'ACTIVE',
  Completed: 'COMPLETED'
});

const OrderType = Object.freeze({
  Standard: 0,
  Express: 1,
  Bulk: 2
});
```

### 8. Generic Class
```typescript
class Box<T> {
  constructor(public value: T) {}
  get(): T { return this.value; }
}
```

## FUNCTION / METHOD Examples

### 1. Function Declaration
```javascript
function calculateTotal(items) {
  return items.reduce((sum, item) => sum + item.price, 0);
}
```

### 2. Parameters Naming Convention
```javascript
function createOrder(salesOrderId, customerId, lineItems) {
  // camelCase for all params
  return { salesOrderId, customerId, lineItems };
}
```

### 3. Return Type (TypeScript)
```typescript
function calculateTotal(items: LineItem[]): number {
  return items.reduce((sum, item) => sum + item.price, 0);
}
```

### 4. Arrow Function
```javascript
const calculateTotal = (items) =>
  items.reduce((sum, item) => sum + item.price, 0);
```

### 5. Async Function
```javascript
async function fetchOrder(id) {
  const response = await api.get(`/orders/${id}`);
  return response.data;
}
```

### 6. Generator Function
```javascript
function* orderIterator(orders) {
  for (const order of orders) {
    yield order;
  }
}
```

### 7. Instance Method
```javascript
class SalesOrder {
  getId() { return this.id; }
  setStatus(status) { this.status = status; }
}
```

### 8. Static Method
```javascript
class SalesOrder {
  static fromJson(json) {
    return new SalesOrder(json.id, json.status);
  }
}
