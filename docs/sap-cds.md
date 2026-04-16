# SAP CDS Naming Convention

## Standard

| Target | Convention | Example |
|---|---|---|
| Namespace / Technical Object | customer namespace + RAP/VDM prefix where applicable | `/LEO/R_SALES_ORDERTP`, `/LEO/C_SalesOrderUi` |
| File Name | match main CDS artifact / DDL source name | `R_SALES_ORDERTP.ddls.asddls`, `C_SalesOrderUi.ddls.asddls` |
| Property / Element | business-oriented `camelCase` | `salesOrderId`, `grossAmount`, `createdAt` |

## Rules

### Namespace / Technical Object
- use your own namespace
- where RAP / SAP conventions define semantic prefixes, keep them: `R_`, `I_`, `C_`

### File Name
- the file name should match the main DDL source / CDS artifact identity

### Property / Element
- use business-readable names
- prefer `camelCase` for elements exposed in CDS definitions and API-like models

## Good
```cds
define view entity /LEO/R_SALES_ORDERTP
  as select from zsales_order
{
  key SalesOrderUUID as salesOrderId,
      CustomerUUID   as customerId,
      GrossAmount    as grossAmount,
      CreatedAt      as createdAt
}
```

## ENTITY / ARTIFACT Examples

### 1. View Entity
```cds
define view entity /LEO/R_SalesOrderTP
  as select from sales_order
{
  key SalesOrderUUID  as salesOrderId,
      CustomerUUID    as customerId,
      GrossAmount     as grossAmount,
      createdAt       as createdAt
}
```

### 2. Projection Entity
```cds
define projection /LEO/R_SalesOrderTP
  on sales_order {
    key SalesOrderUUID  as salesOrderId,
        CustomerUUID    as customerId,
        GrossAmount     as grossAmount
  }
```

### 3. Abstract Entity (Type)
```cds
@EndUserText.label: 'Base Order Type'
abstract entity /LEO/AT_OrderBase {
  key SalesOrderUUID  : UUID;
      CustomerUUID    : UUID;
      GrossAmount     : Amount;
}
```

### 4. Enum Element
```cds
define view entity /LEO/R_SalesOrderTP
  as select from sales_order
{
  key SalesOrderUUID  as salesOrderId,
      status          as orderStatus,  " enum: DRAFT, ACTIVE, COMPLETED
      case status
        when 'D' then 'Draft'
        when 'A' then 'Active'
        else 'Completed'
      end             as statusText
}
```

### 5. Association
```cds
define view entity /LEO/R_SalesOrderTP
  as select from sales_order
{
  key SalesOrderUUID  as salesOrderId,
      CustomerUUID    as customerId,
      _Customer       as Customer   " to-one association
}
with associations {
  _Customer
}
```

### 6. Composition
```cds
define view entity /LEO/R_SalesOrderTP
  as select from sales_order
{
  key SalesOrderUUID       as salesOrderId,
      _LineItems           as LineItems  " composition to LineItems
}
```

## FUNCTION Examples

### 1. Function (CDS Scalar)
```cds
function /LEO/CalculateTax
  ( @EndUserText.label: 'Amount'
    amount : Amount )
  returns { taxAmount : Amount };
```

### 2. Function with Parameters
```cds
function /LEO/GetOrderStatus
  ( @EndUserText.label: 'Order ID'
    salesOrderId : SalesOrderUUID )
  returns { status : String };
```

### 3. Table Function
```cds
define table function /LEO/TF_OpenOrders
  returns {
    SalesOrderUUID : UUID;
    CustomerId     : UUID;
    GrossAmount    : Amount;
  }
  implemented by method CL_SALES_ORDER=>GET_OPEN_ORDERS;
```

### 4. Action (Bound)
```cds
action /LEO/ActivateOrder( @EndUserText.label: 'Order' order : typeof( SalesOrder ) );
```

### 5. Function Import (OData)
```cds
function import getOrderTotal( orderId : UUID ) returns Integer;
```
