##                                                 Explain methods and considerations for connecting to different types of data sources
##                                                 Describe the circumstances under which different load strategies should be used

##                              Explain the circumstances under which QVD files and/or n-tiered data architectures should be recommended

– Reading from QVD is 10-100 times faster than reading from Data sources.
– Consolidating data from multiple data sources and databases.Create multi layer QVDs to create a robust data model.
– Incremental load can be implemented only by using QVDs



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

##           Given a scenario, determine how to resolve table association issues (e.g., synthetic keys/circular references, data types)

##                                Explain the use of control statements and/or variables
https://community.qlik.com/blogs/qlikviewdesignblog/2013/11/04/the-magic-of-variables

One useful command is the TRACE command. It allows you to write data to the reload window. 
https://mindmajix.com/qlikview/how-debugging-works-in-qlikview-script-debugger

The format is:
TRACE   “string”;


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
