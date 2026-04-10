# SAP UI5 Naming Convention

## Standard

| Target | Convention | Example |
|---|---|---|
| Folder / Namespace | standard `webapp` structure + stable namespace | `webapp/controller/`, `webapp/view/`, `webapp/fragment/`, `com/leo/salesorder/` |
| File Name | artifact-specific suffix | `SalesOrder.controller.js`, `SalesOrder.view.xml`, `ValueHelp.fragment.xml` |
| Property | `camelCase` | `salesOrderId`, `selectedCustomer`, `isEditable` |

## Rules

### Folder / Namespace
Use the standard UI5 app structure:
```text
webapp/
├── controller/
├── view/
├── fragment/
├── model/
├── service/
├── util/
└── i18n/
```

### File Name by artifact
- Controller: `PascalCase.controller.js`
- XML View: `PascalCase.view.xml`
- XML Fragment: `PascalCase.fragment.xml`
- Service / Model / Util: `PascalCase.js`

### Property
- use `camelCase` for controller fields, JSON model properties, JS object properties, and service config values

## Good
```javascript
this.orderModel = new JSONModel();
this.selectedCustomer = null;
this.isEditable = true;
```
