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

## CLASS Examples

### 1. Plain Class Declaration
```abap
CLASS lcl_sales_order DEFINITION.
  PUBLIC SECTION.
    METHODS: get_id RETURNING VALUE(r_id) TYPE vbeln.
ENDCLASS.
```

### 2. Class with Constructor
```abap
CLASS lcl_sales_order DEFINITION.
  PUBLIC SECTION.
    METHODS: constructor
      IMPORTING sales_order_id TYPE vbeln
                status TYPE string.
    METHODS: get_id RETURNING VALUE(r_id) TYPE vbeln.
  PRIVATE SECTION.
    DATA: sales_order_id TYPE vbeln, status TYPE string.
ENDCLASS.

CLASS lcl_sales_order IMPLEMENTATION.
  METHOD constructor.
    me->sales_order_id = sales_order_id.
    me->status = status.
  ENDMETHOD.
  METHOD get_id.
    r_id = me->sales_order_id.
  ENDMETHOD.
ENDCLASS.
```

### 3. Class Properties (public, private)
```abap
CLASS lcl_sales_order DEFINITION.
  PUBLIC SECTION.
    DATA: sales_order_id TYPE vbeln.  " public
  PRIVATE SECTION.
    DATA: internal_state TYPE string.  " private
  PROTECTED SECTION.
    DATA: description TYPE string.    " protected
ENDCLASS.
```

### 4. Static Fields / Methods
```abap
CLASS lcl_sales_order DEFINITION.
  PRIVATE SECTION.
    CLASS-DATA: count TYPE i.
  PUBLIC SECTION.
    CLASS-METHODS: get_next_id RETURNING VALUE(r_id) TYPE vbeln.
ENDCLASS.

CLASS lcl_sales_order IMPLEMENTATION.
  METHOD get_next_id.
    count = count + 1.
    r_id = count.
  ENDMETHOD.
ENDCLASS.
```

### 5. Abstract Class
```abap
CLASS lcl_base_service DEFINITION ABSTRACT.
  PUBLIC SECTION.
    METHODS: process ABSTRACT IMPORTING order TYPE REF TO lcl_sales_order.
ENDCLASS.
```

### 6. Interface
```abap
INTERFACE lif_order_processor.
  METHODS: process IMPORTING order TYPE REF TO lcl_sales_order.
  METHODS: can_handle IMPORTING order_type TYPE string
             RETURNING VALUE(r_result) TYPE abap_bool.
ENDINTERFACE.
```

### 7. Enum
```abap
" ABAP 7.5+ enum support
ENUM lty_order_status.
  ADD: 'DRAFT'   AS draft,
       'ACTIVE'  AS active,
       'COMPLETED' AS completed.
ENDENUM.
```

### 8. Generic Class
```abap
CLASS lcl_box DEFINITION.
  PUBLIC SECTION.
    METHODS: constructor IMPORTING value TYPE any.
    METHODS: get RETURNING VALUE(r_value) TYPE any.
  PRIVATE SECTION.
    DATA: value TYPE any.
ENDCLASS.
```

## FUNCTION / METHOD Examples

### 1. Function Module Declaration
```abap
FUNCTION lf_create_order.
  IMPORTING
    sales_order_id TYPE vbeln
    customer_id TYPE kunag
  EXPORTING
    order TYPE REF TO lcl_sales_order
  RAISING
    cx_sales_error.
ENDFUNCTION.
```

### 2. Parameters Naming Convention
```abap
METHODS: create_order
  IMPORTING sales_order_id TYPE vbeln customer_id TYPE kunag
           line_items TYPE Standard Table of ty_line_item
  RETURNING VALUE(r_order) TYPE REF TO lcl_sales_order.
```

### 3. Return Type
```abap
METHODS: get_order_by_id
  IMPORTING sales_order_id TYPE vbeln
  RETURNING VALUE(r_order) TYPE REF TO lcl_sales_order.
```

### 4. Static Method
```abap
CLASS lcl_sales_order IMPLEMENTATION.
  METHOD lif_order_factory~create_from_data.
    r_order = NEW lcl_sales_order( sales_order_id = data-sales_order_id status = data-status ).
  ENDMETHOD.
ENDCLASS.
```

### 5. Instance Method
```abap
METHOD get_id.
  r_id = me->sales_order_id.
ENDMETHOD.
```

### 6. Exception Handling
```abap
METHODS: process_order
  IMPORTING order TYPE REF TO lcl_sales_order
  RAISING cx_sales_error cx_validation_error.
```
