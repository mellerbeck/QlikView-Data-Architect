### Given a data set, identify quality issues
There are many ways to screw up data and data loads.

__REMEMBER__ a LOAD section should close with a semi colon as well as the SQL SELECT section

Stolen from here http://livingqlikview.com/common-pitfalls-qlik-scripting/

#### Forgot to delete comma from what is now the last field.
![ERROR1](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/01Error.jpg)
![ERROR2](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/01ScriptBad.jpg)

#### Failed to open file in write mode
Likely Cause: Reference to a file location that does not exist

#### Why do I have synthetic keys all of a sudden?
Likely Cause: Not Dropping Tables on a resident load

#### I lost the new version of the table
Likely Cause: Automatic Concatenation on resident load. Use noconcatenate to fix

#### Qlikview lockedup
Likely Cause: Joins with no keys. Make double sure when joining that key names match or it will associate every row of one table to every row of the other.

#### Joined table has more records than it started with.
Likely Cause: Left joining with repeating keys. If you left join a table and the right table has repeating values it will join multiple times. __Do not fix with using DISTINCT__   http://www.qlikfix.com/2013/07/30/distinct-can-be-deceiving/

**SPOLIER: When combined with the JOIN or CONCATENATE statement, LOAD DISTINCT will not only remove all duplicates from the input table, but also from the resulting target table.*

Can fix using the lastvalue function with a group by

### Determine the expected effects of data quality issues
Sometimes you have to really look at the data to see what will happen. For example Let's say you had a txt file like this

    Customer,    Item,     Amount
    A,           ItemA,    100, 1      ,XX
    B,           ItemB,    200, 2      ,ZZ 
    C,           ItemC,    300, 3      ,YY

If you loaded in the Customer, Item and Amount Columns you might get confused about what is in the Amount Field. But guess what, you only loaded in Customer, Item and Amount so pay no attention to other (unlabeled) columns of data.

Same as if you had this .txt file

    Customer,     , Amount,    Tax
    D       , 100 , 200   ,    5
    E       , 500 , 300   ,    6
    F       , 600 , 400   ,    7

And you only loaded the Customer and Amount Column, you did not bring in the other columns.

#### Other ways of screwing up data \ Loosely coupled tables (Circular References) \ Synthetic Keys
Stolen from here https://community.qlik.com/blogs/qlikviewdesignblog/2013/06/25/circular-references

Two fictive friends – Albert and Herbert – live in Trollhättan and Gothenburg, respectively. Albert drives a Volvo and Herbert drives a SAAB.

If the above information is stored in a tabular form, you get the following three tables:
![Tables](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/Tables.png)

If you load these tables into QlikView, the circular reference will be identified and you will get the following data model:

![Circular](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/Circular%20reference.png)

To avoid ambiguous results, QlikView marks one of the tables as “loosely coupled”, which means that the logical inference cannot propagate through this table. In the document properties you can decide which table to use as the loosely coupled table. You will get different results from the logical inference depending on which you choose.

If you load the table only once and link to all three foreign keys, you will most likely get a circular reference. You need to break the circular reference and the solution is of course to load the table several times, once for each role.

### Given a data set, determine how the data characteristics at the field level will affect the QlikView data model (e.g., performance, accuracy)

#### Sometimes you are just given crap data. For example a comma delimeted file that the data itself contains commas.

Company, Item, Amount

A Cool Company,  Shoes,   500
A, Bad Company,  Shoes,   400

One fix would be to create the delimeted file using a different dilimiter.

### Interpret an entity relationship (ER) diagram
Stolen From https://community.qlik.com/docs/DOC-16813
![ER](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/ERD1.PNG)
![ER2](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/ERD2.PNG)

### Given a data set, determine the relationships among data

### Given a data set, determine how the relationships among data will affect the QlikView data model (e.g., performance, accuracy)

### LET versus SET
Just remember SET it and forget it. A LET of 1+1 will equal 2
A SET (SET it an forget it) will have the literal string
