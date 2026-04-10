# Node.js Naming Convention

## Standard

| Target | Convention | Example |
|---|---|---|
| Folder / Package | lowercase, prefer `kebab-case` | `sales-order`, `customer-api` |
| File Name | lowercase, prefer `kebab-case.js` | `sales-order.service.js`, `auth-middleware.js` |
| Property | `camelCase` | `salesOrderId`, `createdAt`, `retryCount` |

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
