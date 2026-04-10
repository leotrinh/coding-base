# SAP ABAP Naming Convention

## Standard

| Target | Convention | Example |
|---|---|---|
| Package / Repository Object | customer namespace + SAP object convention | `ZSD_ORDER`, `/LEO/CL_SALES_ORDER` |
| File Name | mirror repository object / abapGit export naming | `zcl_sales_order.clas.abap`, `zif_order_api.intf.abap` |
| Property | descriptive names first; avoid technical encoding for local names | `sales_order_id`, `is_released`, `line_items` |

> This guide uses a hybrid ABAP rule:
> - keep SAP namespace and repository naming rules
> - prefer Clean ABAP descriptive local names
> - keep technical prefixes only where SAP object types or framework-generated artifacts require them

## Rules

### Package / Repository Object
- always use customer namespace (`Z*`, `Y*`, or `/LEO/`)
- repository object names must stay compatible with SAP naming constraints
- for global classes/interfaces, SAP conventions such as `CL_`, `IF_`, `CX_` remain acceptable

### File Name
- if code is exported with abapGit, file names should mirror repository object identity
- do not invent a second naming scheme in Git

### Property
- for local variables, parameters, and attributes inside clean code, prefer descriptive names without Hungarian-style encoding
- keep prefixes where framework/object type/team constraints require them

## Good
```abap
DATA sales_order_id TYPE vbeln.
DATA line_items     TYPE STANDARD TABLE OF ty_line_item.
DATA is_released    TYPE abap_bool.
```

## Legacy-acceptable
```abap
DATA lv_sales_order_id TYPE vbeln.
DATA lt_line_items     TYPE STANDARD TABLE OF ty_line_item.
```
