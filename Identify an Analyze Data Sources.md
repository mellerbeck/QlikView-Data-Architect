###                                                           Given a data set, identify quality issues
There are many ways to screw up data and data loads.

#### An easy and typical error with hand typed data is inconsistency accross fields. For example
U.S.
US
USA

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

###                                                          Determine the expected effects of data quality issues

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

###                                                      Given a data set, determine how the data characteristics at the field level will affect the QlikView data model (e.g., performance, accuracy)

#### Remember Qlikview magic only happens (i.e. fields only associate if they are aliased to the same name!)

#### Sometimes you are just given crap data. For example a comma delimeted file that the data itself contains commas.

Company, Item, Amount

A Cool Company,  Shoes,   500
A, Bad Company,  Shoes,   400

One fix would be to create the delimeted file using a different dilimiter.

### Interpret an entity relationship (ER) diagram

OK, this post finally made me see the light
https://docs.microsoft.com/en-us/common-data-service/entity-reference/relationships


Stolen From https://community.qlik.com/docs/DOC-16813
![ER](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/ERD1.PNG)
![ER2](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/ERD2.PNG)

More http://www.vertabelo.com/blog/technical-articles/crow-s-foot-notation

And More

https://www.slideshare.net/IngePowell/erd-cardinality


###                              Given a data set, determine the relationships among data

#### Performancing enhancements
How can you reduce memory and optimize applications? http://bi-review.blogspot.com/2013/08/few-tips-for-dealing-with-large.html

_One of ways to reduce calculation times is denormalization of the data model. Although, there should be a reasonable balance since denormalization usually increases memory consumption._

Another way is by splitting fields to more efficiently store values.
https://community.qlik.com/docs/DOC-5462

Fat is sometimes better
http://livingqlikview.com/sometimes-fat-is-better/

#### Some info of Schema's stolen from here https://mindmajix.com/snowflake-and-star-schema-in-qlikview

#### Star schema 
Star Schema has a single fact table connected to dimension tables and it visualize as a star. In a star schema only one link establishes the relationship between the fact table and any of the dimension tables. It  is a relational database schema for representing multidimensional data. It is the simplest form of the data warehouse schema that contains one or more dimensions and fact tables

![STAR](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/star.png)

#### Snowflake schema
A snowflake schema is an extension of the star schema. In the snowflake schema, the data model may have one or more fact tables, with connected dimension tables, but will also have secondary dimension tables radiating from one or more primary dimension tables. Pure star schemas in large systems or companies are somewhat rare; snowflake schemas are, the more commonly encountered scenarios due to multiple fact tables and more complex and multiple underlying data sources.

![snowflake](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/snowflake.png)

QlikView Data Model best practices dictate that, a star schema is desirable whenever possible. If not a star schema, the smallest possible snowflake schema is fine, especially in limiting the fact tables to one. A scenario may exist, however, where there is only one large fact table containing many dimensions.

Similarly, if you have a data model with a snowflake schema, working to consolidate the data and build a star schema is usually not going to cause increased performance/ decreased time of query in most cases. This does change with very large data sets, and in those cases, it is worthwhile to spend the time to consolidate and collapse as much as you can, to confirm the star schema.

One of the key considerations is limiting the number of connections required for QlikView to access data, so when working with large data sets, consolidate your data and limit the number of dimension tables, as well as consolidate/concatenate multiple fact tables.

#### Normalize versus Denormalize

Normalize - Normalize means to remove redundancy. 
Denormalize - Put the redundancy back in!

There was a guy named Norm. When you removed all the Norm and there was just one Norm left. Norm was normalized.

Norm was lonely, and so they went and sewed on some other heads and arms and feet and so on until he was denormalized again.

https://blog.codinghorror.com/maybe-normalizing-isnt-normal/


### Given a data set, determine how the relationships among data will affect the QlikView data model (e.g., performance, accuracy)

Let's say you had some interesting dates... maybe coming from an AS400 or something

I have a date in an AS400 table in format YYYYMMDD (numeric) https://www.experts-exchange.com/questions/28265035/AS400-date-is-YYYMMDD-in-table-need-MM-DD-YYYY-from-SQL.html

How do you handle them? https://community.qlik.com/docs/DOC-3102

If the date isn’t automatically recognized, you may need to use an interpretation function to
interpret it: 

```ruby
Date#( DateField, 'M/D/YY') as Date    
```

Or for example the date 20180101

```cpp
Date( Date#( DateField, 'YYYYMMDD'), 'M/D/YYYY') as Date 
```


__Make sure you really use an interpretation function and not a formatting function – it should have a
hash sign “#” in it.__
 
*Also, you should check that QlikView really has interpreted the dates as numbers: Either implicitly
by checking that the dates are right-aligned in the list box, or explicitly by formatting the dates as
numbers (Properties – Numbers) and verifying that the numbers displayed have values around
40000 (for dates in present time).*

Let's say you had a file with just months like this

    MONTH
    JAN
    FEB
    MAR
    APR

You can convert the month names to dual months using
```ruby
Month( Date#( Month,'MMM') ) as Month
```

### What if you have multiple date types in a file
You can use the Alt() function

The alt function returns the first of the parameters that has a valid number representation. If no such match is found, the last parameter will be returned. Any number of parameters can be used. https://help.qlik.com/en-US/qlikview/November2017/Subsystems/Client/Content/Scripting/ConditionalFunctions/alt.htm

Syntax:  

alt(case1[ , case2 , case3 , ...] , else)
 
*The alt function is often used with number or date interpretation functions. This way, QlikView can test different date formats in a prioritized order. It can also be used to handle NULL values in numerical expressions.*

So if you had some crazy dates like

    31.03.1900
    1956-02-28
    20111201
    
This function would take care of it
```ruby

Alt( Timestamp#(MixDate,'M/D/YYYY h:mm tt'),
 Date#(MixDate,'M/D/YYYY'),
 Date#(MixDate,'D/M/YYYY'),
 Date#(MixDate,'YYYYMMDD'),
 Date#(MixDate,'DD.MM.YYYY'),
 Date#(MixDate,'YYYY-MM-DD')
 ) as MixDate
 
```

#### Concatenating and adding fields is a good way of optimizing performance 
http://www.qliktips.com/2013/10/flags-and-dual-values-in-set-analysis.html



###                                                              LET versus SET
Just remember SET it and forget it. A LET of 1+1 will equal 2
A SET (SET it an forget it) will have the literal string

###                                                              Joins
Because you know I'm all about that Joins
'bout that joins, more data

Yeah, it's pretty clear the first is an INNER JOIN
It returns the records that are matching in both tables

Yeah, my momma she told me don't worry about your joins
She says, a LEFT JOIN returns all the records that are on the LEFT
You know and the matched records from the right table.

If you want the opposite then use a RIGHT JOIN
Returns all the records on the RIGHT and matched records from the LEFT

To get every inch of perfect data use a FULL OUTER JOIN



