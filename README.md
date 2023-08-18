# Test class for domain constant classes 

This repository provides class `ZCL_FOSS_DOMAIN_CONSTANTS_TEST` as a parent class for your domain constant class unit tests.

It has test methods to verify the integrity of your constant class, e.g. if it contains a constant for each domain fix values.

# What's a domain constant class?

A domain constant class contains constants for each value of a domain. 

Please refer to the approriate section in the [Clean ABAP styleguide](https://github.com/SAP/styleguides/blob/93499d0/clean-abap/sub-sections/Enumerations.md) for more details on the subject.

A constant class for the domain `DDISGN` might look like this:

````abap
CLASS zcl_ddsign_constant_class DEFINITION
  PUBLIC
  FINAL
  ABSTRACT
  CREATE PUBLIC.

  PUBLIC SECTION.
    CONSTANTS included TYPE ddsign VALUE 'I'.
    CONSTANTS excluded TYPE ddsign VALUE 'E'.
ENDCLASS.
````

# How to use 

Simply inherit your test class from this class and implement method `GET_CLASS_NAME`.
You can use method `DETERMINE_CLASS_NAME_FROM_TYPE` to do this dynamically without hard-coding the name of the class:

````abap
CLASS ltc_example_inheritor DEFINITION CREATE PUBLIC
 FOR TESTING
 RISK LEVEL HARMLESS
 DURATION SHORT
 INHERITING FROM zcl_foss_domain_constants_test.

  PROTECTED SECTION.
    METHODS get_class_name REDEFINITION.
ENDCLASS.


CLASS ltc_example_inheritor IMPLEMENTATION.
  METHOD get_class_name.
    DATA lo_constant_class TYPE REF TO lcl_example_constant_class.
    rv_result = determine_class_name_from_type( lo_constant_class ).
  ENDMETHOD.
ENDCLASS.
````

# Contributing

If you want to contribute to this repository, please use [my recommended ABAP Cleaner Profile](https://github.com/ConjuringCoffee/abap-cleaner-recommendation).
Pull requests are welcome.

# What is `FOSS`?

A dedicated application namespace wouldn't make much sense for a repository this small, so a more generic namespace made more sense.
FOSS is an acronym for [free and open-source software](https://en.wikipedia.org/wiki/Free_and_open-source_software).

# Miscellaneous

The class was inspired by an example from the [Clean ABAP styleguide](https://github.com/SAP/styleguides/blob/93499d0/clean-abap/sub-sections/Enumerations.md#prefer-classes-to-interfaces).