# Manipulating tables

## Creating a table

​	To create a table in HBase, we need only to define the groups of columns, not the columns itself.

​	Syntax:

```bash
create '<tbname>', {NAME=>'<familyname>'}, {NAME=>'<familyname>'}
```

​	Example:

```bash
create 'commerce', {NAME=>'customer', VERSIONS=>3}, {NAME=>'product'}
# or
create 'commerce', {NAME=>'customer', VERSIONS=>3}, 'product'
```

## Table options

​	To scan a table (read its data):

```bash
scan 'commerce'
```

​	Disabling a table:

```bash
disable 'commerce'
```

​	To delete a table (can only be done after the table is disabled):

```bash
drop 'commerce'
scan 'commerce' # error
```

​	To truncate a table (disable it and recreate its structure):

```bash
truncate 'commerce'
```

