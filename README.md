# Launch Common Automation Framework - Python Module Component

This repo holds the component for Python modules within the Launch Common Automation Framework (LCAF).

It contains the following:

* tasks - Makefiles for performing Python operations on your module and running tests and pre-checks
* policy - OPA policy definitions for Python modules.  The contents here apply to **all** LCAF Python modules.
* linkfiles - other files used by Python and LCAF projects

## Policy Customization

To add policies in addition to the policies defined by the LCAF Python module and by Regula, define

```CUSTOM_POLICY_REPO=https://some.git.url/```

in your Makefile.includes.  Only the default branch (`main`) is supported.

This repo should have 2 top-level directories:

* policy
* regula

`policy` will contain your rego policy files (and tests), if any.

`regula` will contain your regula config file which defines your waivers for regula rules (if any).