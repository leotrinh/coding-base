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

## CLASS Examples

### 1. Controller Class (Standard)
```javascript
// webapp/controller/SalesOrder.controller.js
sap.ui.define(['sap/ui/core/mvc/Controller'], function(Controller) {
  'use strict';
  return Controller.extend('com.leo.salesorder.controller.SalesOrder', {
    onInit: function() {
      this._oRouter = sap.ui.core.UIComponent.getRouterFor(this);
    }
  });
});
```

### 2. Controller with Constructor Pattern
```javascript
sap.ui.define(['sap/ui/core/mvc/Controller'], function(Controller) {
  'use strict';
  return Controller.extend('com.leo.salesorder.controller.SalesOrder', {
    constructor: function() {
      Controller.apply(this, arguments);
      this._bIsEditable = false;
    }
  });
});
```

### 3. Model Property Handling
```javascript
setOrderModel: function(oOrder) {
  this.oOrderModel = oOrder;
  this.getView().setModel(oOrder, 'order');
},
getOrderModel: function() { return this.oOrderModel; }
```

### 4. Static Utility Class (Formatter)
```javascript
sap.ui.define([], function() {
  'use strict';
  return {
    formatStatus: function(sStatus) {
      return sStatus === 'DRAFT' ? 'Draft' : sStatus === 'ACTIVE' ? 'Active' : 'Unknown';
    },
    formatAmount: function(fAmount) { return fAmount ? parseFloat(fAmount).toFixed(2) : '0.00'; }
  };
});
```

### 5. Model Class (JSON / OData)
```javascript
createOrderModel: function() {
  this.oOrderModel = new JSONModel({ salesOrderId: '', customerId: '', items: [], isActive: false });
}
```

### 6. Fragment Class
```javascript
sap.ui.define(['sap/ui/core/Fragment'], function(Fragment) {
  'use strict';
  return {
    openValueHelp: function(oView) {
      if (!this._pValueHelp) {
        this._pValueHelp = Fragment.load({ name: 'com.leo.salesorder.fragment.ValueHelp', controller: this })
          .then(function(oFragment) { oView.addDependent(oFragment); return oFragment; });
      }
      this._pValueHelp.then(function(oFrag) { oFrag.open(); });
    }
  };
});
```

### 7. Enum (Constant Object)
```javascript
sap.ui.define([], function() {
  'use strict';
  return {
    OrderStatus: { DRAFT: 'DRAFT', ACTIVE: 'ACTIVE', COMPLETED: 'COMPLETED' },
    OrderType: { STANDARD: 0, EXPRESS: 1, BULK: 2 }
  };
});
```

### 8. Generic Model Wrapper
```javascript
sap.ui.define(['sap/ui/model/json/JSONModel'], function(JSONModel) {
  'use strict';
  return JSONModel.extend('com.leo.BaseModel', {
    setDataSafe: function(oData) { if (oData) this.setData(oData); },
    getOrDefault: function(sKey, vDefault) { return this.getData()[sKey] ?? vDefault; }
  });
});
```

## FUNCTION / METHOD Examples

### 1. Event Handler (onInit pattern)
```javascript
onInit: function() {
  this._oRouter = sap.ui.core.UIComponent.getRouterFor(this);
  this._loadOrderData();
}
```

### 2. Parameters Naming Convention
```javascript
onCreateOrder: function(salesOrderId, customerId, lineItems) {
  // camelCase params in UI5 controller
}
```

### 3. Async Function (Promise)
```javascript
_loadOrderData: function(sOrderId) {
  return new Promise(function(resolve, reject) {
    OData.read('/sap/opu/odata/sap/SEPMRA_SO_ORDER', resolve, reject);
  });
}
```

### 4. Arrow Function (ES6)
```javascript
this.aItems.map(item => item.salesOrderId);
this.aOrders.filter(order => order.isActive);
```

### 5. Formatter Function
```javascript
formatCurrency: function(fAmount, sCurrency) {
  return (fAmount ? parseFloat(fAmount).toFixed(2) : '0.00') + ' ' + (sCurrency || 'USD');
}
```

### 6. Instance Method
```javascript
getOrderById: function(sOrderId) {
  return this.oOrderModel.getProperty('/' + sOrderId);
}
```

### 7. Static Method
```javascript
sap.ui.define(['sap/ui/core/date/UI5Date'], function(UI5Date) {
  return { parseDate: function(sDate) { return UI5Date.getInstance(sDate); } };
});
```

### 8. Protected/Underscore Method
```javascript
_validateInput: function(oOrderData) { return !!oOrderData.salesOrderId; }
```
