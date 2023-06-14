# Microsoft Dynamics 365 Business Central connector
Repository for the Microsoft Dynamics 365 Business Central connector

The current connector is using the API as part of the wider Microsoft Graph API, this is still in beta, but seems to work. When doing `sesam upload/authentication` using sesam-py, first time you use the authorization screen to send a request for approval the Azure AD admin (Henrik/support), and then after it's approved, you have to do `upload/authenticate` again. The second time, all the secrets should be picked up and uploaded to your node successfully. 

A note/caveat on the API
------------------------

Currently, this connector uses several undocumented MS Graph APIs (and the documented ones are in "beta" and has been since 2019).
This means that it could stop working, and there's no support from MS if they do.

How to obtain an "account_id"
-----------------------------

Most of the pipes in this connector need an "account_id" which is really a "CompanyID" from the "companies" pipe.
To get it, do a `sesam upload` (possibly twice) and then run the "xxxxxx-companies-collect" pipe and copy the "id" 
from the only entity  it produces. Enter this as "account_id" in .authconfig.


# Datatypes
## Currencies
Minimal object:
```
{
  "code": "NOK"
}
```

## Customers
Note that ``displayName`` is not actually required by the API, but without a ``displayName`` it will not show up in the UI.

Minimal object:
```
{
  "displayName": "Some customer"
}
```

## Employee
Minimal object:
```
{
  "givenName": "Ante",
  "surname": "Testson"
}
```

## Paymentterms
Minimal object:
```
{
   "code": "3 DAGER"
}
```

## Paymentmethods
Minimal object:
```
{
  "code": "ACCOUNT",
  "displayName": "Betaling",
}
```

## Vendors
Insert:

Minimal object:
```
{
  "displayName": "Leverandør 2"
}
```

Update:
```
    "$based_on_properties": [
      "balance",
      "blocked",
      "currencyCode",
      "currencyCode",
      "currencyId",
      "displayName",
      "id",
      "lastModifiedDateTime",
      "number",
      "paymentMethodId",
      "paymentTermsId",
      "taxLiable"
    ]
```


## Salesorders
Insert:

Minimal object:
```
  {
    "customerNumber": "50000"
  }
```

Update:
```
  "$based_on_properties": [
    "billToCustomerId",
    "billToCustomerNumber",
    "billToName",
    "currencyCode",
    "currencyId",
    "id",
    "customerName",
    "customerNumber",
    "customerId",
    "discountAmount",
    "discountAppliedBeforeTax",
    "email",
    "externalDocumentNumber",
    "fullyShipped",
    "number",
    "orderDate",
    "partialShipping",
    "paymentTermsId",
    "pricesIncludeTax",
    "requestedDeliveryDate",
    "salesperson",
    "shipToContact",
    "shipToName",
    "status",
    "totalAmountExcludingTax",
    "totalAmountIncludingTax",
    "totalTaxAmount"
  ]
```

## Salesorderitems
Minimal object:
```
  {
    "itemId": "d66eb5d3-55e9-ed11-8850-6045bdc8c1cc",
    "lineType": "Item"  
  }
```

## Items
Minial object:
```
  {
    "displayName": "Test",
    "itemCategoryId": "c46eb5d3-55e9-ed11-8850-6045bdc8c1cc",
    "type": "Inventory"
  }
```

## Itemcategories
Minimal object:
```
  {
    "code": "TEST",
    "displayName": "Test"
  }
```

