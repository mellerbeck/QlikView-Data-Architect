##                                                 Explain methods and considerations for connecting to different types of data sources

Sometimes you want to do a wildcard load. https://community.qlik.com/blogs/qlikviewdesignblog/2013/01/10/wildcard-data-loading-blah

My quick test was 

    LOAD @1
    FROM
    [C:\files\*.txt]
    (txt, codepage is 1252, no labels, delimiter is '\t', msq);
    
Of a fancier method

```ruby
For each vFile in FileList('C:\Users\aby\Desktop\*wildcard.xlsx')

Load Col2+Col3 as Total,
     *;
Load *,
     Filebasename() as Source
from [$(vFile)]
(ooxml, embedded labels, table is Sheet1);

Next vFile
```

##                                                 Describe the circumstances under which different load strategies should be used

##                              Explain the circumstances under which QVD files and/or n-tiered data architectures should be recommended

– Reading from QVD is 10-100 times faster than reading from Data sources.
– Consolidating data from multiple data sources and databases.Create multi layer QVDs to create a robust data model.
– Incremental load can be implemented only by using QVDs

This is an amazing white paper on proper QVD usage!!!! 
http://qlikview.oxs.ru/install/Goods/QVDocumentation/Enterprise%20Framework/Scalability/Data%20Management/QlikView%20Enterprise%20QVD%20Layer.pdf




##                                Describe the use and properties of fact tables and dimension tables
##                                Explain load techniques relevant to data transformation
##                                Explain the use of QlikView functions to transform data
##                                Explain how to resolve complex calendar scenarios

### Generating data is a frequent task. This paper by HIC is excellent
https://community.qlik.com/docs/DOC-3786



##                                Explain the use and effects of different types of joins
https://community.qlik.com/docs/DOC-7520

    INNER
    LEFT
    RIGHT
    OUTER
    
![twotables](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/Two%20Tables.png)

After different joins this is what it looks like

![different](https://github.com/mellerbeck/QlikView-Data-Architect/blob/master/Images/Different%20Joins.png)

http://www.qlikfix.com/2010/12/09/merging-tables-concatenation/



##                                Given business requirements, determine appropriate section access configuration
Quote myself why not https://michaelellerbeck.com/2017/07/13/learning-some-qlikview-section-access/
__SECTION ACCESS LIKES EVERYTHING IN UPPERCASE__

Simple mode is
ACCESS USERID PASSWORD
ACCESS, USERID, PASSWORD, OMIT



##           Given a scenario, determine how to resolve table association issues (e.g., synthetic keys/circular references, data types)

##                                Explain the use of control statements and/or variables
https://community.qlik.com/blogs/qlikviewdesignblog/2013/11/04/the-magic-of-variables

One useful command is the TRACE command. It allows you to write data to the reload window. 
http://www.johndaniel.com/index.php/how-to-use-the-trace-function-to-track-down-problems-in-qlikview/

    The format is:
    TRACE   “string”;

https://help.qlik.com/en-US/qlikview/November2017/Subsystems/Client/Content/Scripting/ScriptRegularStatements/Trace.htm
    
    Let MyMessage = NoOfRows('MainTable') & ' rows in Main Table';
    Trace $(MyMessage);

### Sometimes you need to load limited amounts of data. Two ways to accomplish this.
https://community.qlik.com/blogs/qlikviewdesignblog/2014/12/26/limited-load-and-the-first-prefix
You can use limited load. Or you can use the FIRST prefix



##                                Explain the purpose and functionality of the Table Viewer/System Fields
https://help.qlik.com/en-US/qlikview/November2017/Subsystems/Client/Content/Table_Viewer.htm
(Control-T)
This dialog is used to display the data table structure of the current QlikView document. Tables are shown as boxes with a list of the fields they contain. Connector lines between the boxes show the associations. Where more than two lines meet there are connector points in the form of small dots.

__Information density__ is the number of records that have values (i.e. not NULL) in this field as compared to the total number of records in the table.

__Subset ratio__ is the number of distinct values of this field found in this table as compared to the total number of distinct values of this field (that is other tables as well).

* $numeric	  All (non-NULL) values in the field are numeric	
* $integer	  All (non-NULL) values in the field are integers.	
* $text	      No values in the field are numeric.	Yes
* $ascii	    Field values contain only standard ASCII characters.	Yes
* $date	      All (non-NULL) values in the field can be interpreted as dates (integers).	
* $timestamp	All (non-NULL) values in the field can be interpreted as time stamps.



##                                Determine the root cause for discrepancies between values in legacy reports and QlikView values
##                                Explain the purpose and functionality of QlikView troubleshooting tools or functions
##                                Given a script, determine the cause and/or solution for a script error
