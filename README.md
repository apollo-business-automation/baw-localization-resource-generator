# BAW Localization Resource generator

This generator is here to help you Working with Localization Resources in BAW.

## Description

This XLSM file with macros enables you to maintain and generate localization resource bundle for BAW (BPMN) in multiple languages.

## Usage

1. Review and edit sheets as needed based on the description below.
2. Provide at least one translation column. Prepopulated with sample content. Make sure you provide column which matches default locale specified on *config* sheet.
3. Customize resource bundle name if desired.
4. Click Export button on *config* sheet and resource bundle will be generated into folder where the XLSM is located.
	
Bare in mind the note from https://www.ibm.com/docs/en/baw/20.x?topic=applications-creating-localization-resources which instructs you to unicode escape non-ascii characters. This can be done using e.g. https://native2ascii.net online tool

## Sheet description

- Sheet *config* - Choose default locale and name of the resource bundle.
- Sheet *context types* - Serves for *where* is the localization used. Add new entries if needed.
  - Column *name* is used to lookup the *value* when used on *contexts* sheet.
  - Column *value* is used in the resulting entry on *contexts* sheet and is short not to make the result localization key too long.
- Sheet *key types* - Serves for *for what* is the localization used. Add new entries if needed.
  - Column *name* is used to lookup the *value* when used on *translations* sheet.
  - Column *value* is used in the resulting entry on *translations* sheet.
- Sheet *contexts* - Computes a context key to be used on *translations* sheet.
  - Column *name* contains actual name of BAW artifact or abstract names for e.g. global translations or enums that are used on different places.
  - Column *value* is short representation of the *name*. Typically it can be first letters of name of artifact.
  - Column *type* is a reference to sheet *context types* column *name*
  - Column *computed context key* is used in the resulting entry on *translations* sheet.
- Sheet *translations* - Contains the actual translations.
  - Column *context key* is a reference to sheet *contexts* column *computed context key*.
  - Column *key type* is a reference to sheet *key types* column *name*.
  - Column *key name* is short english representation of the translation.
  - Column *computed localization key* is computed from the previous columns to its final for of ```<context types/value><contexts/value>.<key types/value>.<translations/key name>```.
  - Additional columns represent two letter codes of languages you want to provide localization for.
