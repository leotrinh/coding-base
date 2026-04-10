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
