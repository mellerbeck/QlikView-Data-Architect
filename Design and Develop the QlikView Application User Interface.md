## Determine the result of a given function or complex expression

SET ANALYSIS duh duh duh

https://community.qlik.com/servlet/JiveServlet/download/1223362-268012/QlikLearn-Set-Analysis%20-Vikas.pdf

It all starts with an aggregation

For example 

    sum( Sales )

Set analysis is really just a selection! ( A fancy one of course)

Broken into 3 categories. 

### Identifiers
0 - empty set
1 - full set
$ - Current selection
$1 - Previous selection
$_1 - Next Selection

Example
sum({1} Sales) - Disregards selections
sum({$} Sales) - Current Selection

Sometimes you want to ignore selections in fields. To do that you set the field to nothing. So for example lets say you had the country 
codes

    codes     countryName
    AF        Afghanistan
    AX        Aland Islands
    AL        Albania
    DZ        Algeria

You wanted your set to be AF and AX so Code={AF,AX}
But if you wanted to ignore selections in say the countryName you would do 

    <Code={AF,AX},countryName=>


## Identify where alternate uses of expressions are appropriate


## Given a scenario, determine the appropriate function or complex expression to use


## Explain how to implement Actions/Triggers in the QlikView interface


## Given a scenario, determine the appropriate object or chart type to use

https://help.qlik.com/en-US/sense/September2017/Subsystems/Hub/Content/Visualizations/when-to-use-what-type-of-visualization.htm

    Side by side -                  - Bar chart
    Absolute and relative values    - Combo chart
    Selections to reduce data set   - 
    Indicate ratio                  - Gauge
    Trends over time                - Line chart
    Point and area data             - Map
    Ratio to total                  - Pie
    Cross table view and summarize  - Pivot
    Display correlation             - Scatter plot
    Display numbers and values      - Table
    


## Explain the purpose/functionality of common object properties


## Given a scenario, determine the appropriate application performance tuning option to use




## Given a scenario, determine the appropriate reload performance tuning option to use
http://qlikviewcookbook.com/2014/02/speed-up-script-development-with-buffer/

One trick that works well for LOG files is the Buffer load.

A BUFFER statement just by itself will load the data and the store it to a QVD in the background. Next time you run the load statement it will load it from the QVD.

If you use

    BUFFER (incremental) LOAD
    
Case 1: Append Only
The simplest case is the one of log files; files in which records are only appended and never deleted. The following conditions apply:

The database must be a log file (or some other file in which records are appended and not inserted or deleted) which is contained in a text file (no ODBC/OLE DB). 
QlikView keeps track of the number of records that have been previously read and loads only records added at the end of the file.


Script Example:

Buffer (Incremental) Load * From LogFile.txt (ansi, txt, delimiter is '\t', embedded labels);

 

Buffer Load:

 

The syntax is:

buffer[ (option [ , option] ) ] ( loadstatement | selectstatement )

where:

option ::= incremental | expiry

expiry::= stale [after]amount[ (days | hours)]

amount is a number specifying the time period. Decimals may be used. The unit is assumed to be days if omitted.

The incremental option enables the ability to read only part of an underlying file. Previous size of the file is stored in the XML header in the QVD file. This is particularly useful with log files. All records loaded at a previous occasion are read from the QVD file whereas the following new records are read from the original source and finally an updated QVD-file is created. Note that the incremental option can only be used with load statements and text files and that incremental load cannot be used where old data is changed or deleted!
    

