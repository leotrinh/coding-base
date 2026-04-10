# Java Naming Convention

## Standard

| Target | Convention | Example |
|---|---|---|
| Package | lowercase reverse-domain package | `com.leo.sales.order` |
| File Name | `PascalCase.java`, must match top-level public type | `SalesOrderService.java` |
| Property | `camelCase` | `salesOrderId`, `createdAt`, `retryCount` |

## Rules

### Package
- use all lowercase
- prefer reverse-domain style
- do not use underscores

### File Name
- a Java source file should be named after its top-level public class/interface/enum/record
- use `PascalCase.java`

### Property
- use `camelCase`
- boolean properties should read naturally: `isActive`, `hasChildren`
- constants use `SCREAMING_SNAKE_CASE`

## Good
```java
package com.leo.sales.order;

public class SalesOrderService {
    private String salesOrderId;
    private boolean isActive;
    private static final int MAX_RETRY_COUNT = 3;
}
```

## Bad
```java
package com.leo.Sales_Order;

public class salesOrderService {
    private String SalesOrderId;
    private boolean is_active;
}
```
