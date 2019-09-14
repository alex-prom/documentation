# Currency

## Settings & rates

Administrator can configure currency related parameters and rates at Administration > Currency.

You can specify which currencies will be available in the system in *Currency List* parameter.

*Default Currency* -- which currency will be set be default when creating a new record. A currency to which all currency fields will be converted to when filtering, sorting, reporting.


*Base Currency* -- which currency to use as a base to specify rates.

### Default currency for specific field

It's possible to specify an exclusive default currency for a specific field.

Example for *amount* field of *Opportunity*. Set *Default* value at Administration > Entity Manager > Opportunity > fields > amountCurrency.

## Currency converion

### Currency Converted field

All fields of *Currency* type are paired with a special read-only field of *Currency Converted* type. When you create a new Currency field, Converted field is created automatically. This field represents a value converted to *Default Currency* based on current currency rates. This field is used for sorting by currency field, filtering, comparison, reporting.

Note, that when currency rates are changed, the value of Currency Converted field is also changed. Technically the value is not stored, but calculated on-fly. This can cause an issue that your reports gets changed every time currency rates are changed.

To store a converted value based on current rates you can:

1. Convert currency manually. With mass action from the list view or action on the detail view.
2. Convert currency automatically with Workflows tool. Convert Currency service action is available for Opportunities, Quotes, Sales Orders, Invoices. E.g. you can setup a workflow that will update currencies for all closed opportunities each week.
3. Utilize formula to store a current convered value in a separate read-only field. You can use either a regular Before Save Script or Workflow tool.

### Storing current conveted value (locked)

Lets assume that you have a currency field named *amount*, and default currency is *USD*.

Create a new field of *Currency* type, name it *amountConvertedLocked*, make it read-only, 

Add a formula script to Before Save Script at Entity Manager. You can also use this formula in Workflow rule.

```
amountConvertedLocked = amountConverted;
amountConvertedLockedCurruncy = 'USD';
```

You can re-calculate formula for all existing records with mass action on the list view.

### Convert currency manually

It's possible to convert manually all currency fields of a record.

1. Mass action on the list view. Select which records you want to update (you can selech all results). In *Actions* dropdown click *Convery Currency*.
2. Action on the detail view. Available in the dropdown next to *Edit* button.

### Convert currency with Workflow

*Convert Currency* service action is available for Opportunity, Quote, Sales Order, Invoice. E.g. you can setup a workflow that will update currencies for all closed opportunities each week.
