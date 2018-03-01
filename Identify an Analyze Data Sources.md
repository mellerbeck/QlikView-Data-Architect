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

### Given a data set, determine how the data characteristics at the field level will affect the QlikView data model (e.g., performance, accuracy)

### Interpret an entity relationship (ER) diagram
Stolen From https://community.qlik.com/docs/DOC-16813
![ER](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/ERD1.PNG)
![ER2](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/ERD2.PNG)

### Given a data set, determine the relationships among data

### Given a data set, determine how the relationships among data will affect the QlikView data model (e.g., performance, accuracy)

### LET versus SET
Just remember SET it and forget it. A LET of 1+1 will equal 2
A SET (SET it an forget it) will have the literal string
