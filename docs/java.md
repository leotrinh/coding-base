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

## CLASS Examples

### 1. Plain Class Declaration
```java
public class SalesOrder {
    // body
}
```

### 2. Class with Constructor
```java
public class SalesOrder {
    private String salesOrderId;
    private String status;

    public SalesOrder(String salesOrderId, String status) {
        this.salesOrderId = salesOrderId;
        this.status = status;
    }
}
```

### 3. Class Properties (public, private)
```java
public class SalesOrder {
    public String salesOrderId;     // public
    private String internalState;  // private
    protected String description;   // protected
}
```

### 4. Static Fields / Methods
```java
public class SalesOrder {
    private static int count = 0;

    public static int getNextId() {
        return ++count;
    }
}
```

### 5. Abstract Class
```java
public abstract class OrderService {
    public abstract void process(SalesOrder order);
    public void log(String message) {
        // common behavior
    }
}
```

### 6. Interface
```java
public interface OrderProcessor {
    void process(SalesOrder order);
    boolean canHandle(String orderType);
}
```

### 7. Enum
```java
public enum OrderStatus {
    DRAFT, ACTIVE, COMPLETED
}

public enum OrderType {
    STANDARD(0), EXPRESS(1), BULK(2);
    private final int value;
    OrderType(int value) { this.value = value; }
    public int getValue() { return value; }
}
```

### 8. Generic Class
```java
public class Box<T> {
    private T value;
    public Box(T value) { this.value = value; }
    public T get() { return value; }
}
```

## FUNCTION / METHOD Examples

### 1. Method Declaration
```java
public BigDecimal calculateTotal(List<LineItem> items) {
    return items.stream()
        .map(LineItem::getPrice)
        .reduce(BigDecimal.ZERO, BigDecimal::add);
}
```

### 2. Parameters Naming Convention
```java
public SalesOrder createOrder(String salesOrderId, String customerId, List<LineItem> lineItems) {
    return new SalesOrder(salesOrderId, customerId, lineItems);
}
```

### 3. Return Type
```java
public String getOrderId(SalesOrder order) {
    return order.getSalesOrderId();
}
```

### 4. Static Method
```java
public static SalesOrder fromJson(String json) {
    // parse and return
    return new SalesOrder();
}
```

### 5. Instance Method
```java
public class SalesOrder {
    public String getId() { return this.salesOrderId; }
    public void setStatus(String status) { this.status = status; }
}
```

### 6. Override Method
```java
@Override
public String toString() {
    return "SalesOrder{id='" + salesOrderId + "'}";
}
```

### 7. Generic Method
```java
public <T> T convert(Object source, Class<T> targetType) {
    // conversion logic
    return targetType.cast(source);
}
```

### 8. Builder Pattern Method
```java
public static class Builder {
    private String salesOrderId;
    public Builder salesOrderId(String id) { this.salesOrderId = id; return this; }
    public SalesOrder build() { return new SalesOrder(salesOrderId); }
}
```
