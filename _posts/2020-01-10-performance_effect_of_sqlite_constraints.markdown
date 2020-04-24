---
layout: post
title:      "Performance effect of SQLite constraints"
date:       2020-01-10 00:38:55 -0500
permalink:  performance_effect_of_sqlite_constraints
---




> Note: This is not related to Active record or ruby sqlite3 gem.

SQLite, unlike other databases, does not [strictly check](https://www.sqlite.org/datatype3.html) data being inserted.  It is possible to enter a string into a field designated for an integer.  As its name suggests, SQLite focuses on providing strong compatibility with other SQL DB offering, while being as lightweight as possible.  Thus much of the data validation is left to the connecting application.  However, SQLite is not without some constant and data validation features.  While constraints do not directly solve the lack of type checking, it will allow us to provide some constraints to the data entered.

Constraints available:
-    `PRIMARY Key` − can only be used once in a table, the field is UNIQUE, not null and auto Increments.

-    `NOT NULL` − The field cannot contain a NULL value.

-    `DEFAULT <VALUE>`− value use of not value iS provided.

-   `UNIQUE` − All values in the field must not be repeated in the table.

-  `CHECK` − Allow for custom constraints based on an expression. (e.g: `CHECK(active == 1 || active == 0)`)

-  `FOREIGN KEY` – see below.

The foreign key allows you to reference rows in other tables by their primary key. However, by default, the foreign key is also not validated, you can create a key connection to a primary key or table that does not exist.  Foreign key validation can enable with a [special syntax](https://www.sqlite.org/foreignkeys.html)

- `FOREIGN KEY(field_name) REFERENCES other_table_name(primary_key_field)`


Since SQLite above all else is designed to be lightweight, it is possible to remove constraint functionality at compile time or via pragmas.  Thus, you should make sure the version being used in your project has it enabled. However, in my testing, the SQLite installed via homebrew (Mac) and DNF (Fedora) did have it enabled at compilation and can be toggled via pragma.

By adding constant to a test SQL project, I saw a very small increase in the computation of transactions and do not believe they would hurt performance in most situations. [Results](https://github.com/Anthonyntilelli/sqlite3-constraint-test/blob/master/tests.md)

Should you use SQLite constants in your ruby application?

If you are using  SQLite in your application, constants can greatly increase the validity of your data with a very small cost on performance.  During my time testing for this blog, the constrained version was able to catch small mistakes made and help greatly reduce debugging.

If your application is using an Abstracted ORM solution such as Active Record, you should prefer the constrain and validations option offered by that solution.  Under the hood, that solution may be making use of the constraints in part. However direct SQLite manipulation should be done with care to ensure the correct functioning of your chosen ORM solution.

