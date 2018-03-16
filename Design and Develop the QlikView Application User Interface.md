## Determine the result of a given function or complex expression

SET ANALYSIS duh duh duh

https://community.qlik.com/servlet/JiveServlet/download/1223362-268012/QlikLearn-Set-Analysis%20-Vikas.pdf

It all starts with an aggregation

For example 

    sum( Sales )

Set analysis is really just a selection! ( A fancy one of course)

Broken into 3 categories. 

### Identifiers
```
0 - empty set
1 - full set
$ - Current selection
$1 - Previous selection
$_1 - Next Selection
```

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

Buckets, buckets, buckets. https://community.qlik.com/blogs/qlikviewdesignblog/2014/07/14/buckets

Simple way is nested if statements.

```ruby

   If( ShippedDate - RequiredDate <= -5, 'Too early',
   If( ShippedDate - RequiredDate <= 0, 'Just in time',
   If( ShippedDate - RequiredDate <= 5, 'Small delay',
      'Large delay' ))) as Delay,
```

Second option Round or Class

```ruby
Round( ShippedDate - RequiredDate , 5 ) as Delay,
Class( ShippedDate - RequiredDate , 5 ) as Delay,
```

Third option is IntervalMatch

```ruby
DelayClasses:
Load Lower, Upper, Delay Inline
[Lower, Upper, Delay
-E99,-5,Too early
-4,0,Just in time
1,5,Small delay
6,E99,Large delay];
IntervalMatch (DelayInDays)
Load Lower, Upper Resident DelayClasses;
```

## Explain how to implement Actions/Triggers in the QlikView interface

https://help.qlik.com/en-US/qlikview/November2017/Subsystems/Client/Content/Document_Properties_Triggers.htm

Triggers are a complex subject, you can do a lot with them. A simple example,

an OnOpen trigger

You can use this to set a variable, select in field etc...

OnAnySelect - anything selection in any field

__Cascading actions are not supported__


## Given a scenario, determine the appropriate object or chart type to use

One advanced way of adding your own visualizations is through extensions and mashups.
https://help.qlik.com/en-US/qlikview-developer/November2017/Subsystems/Mashups/Content/mashups-start.htm



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
    Containers                      - Can hold all other objects

There are ways to make one chart work like multiple charts! You can enable the fast type change setting and choose the charts you want to allow it to be able to change to.


    
### A common qlikview requirement is doing some whatif Analysis. 
Sliders are useful for this because they can change variables.
Also, input boxes are useful because you can type values and update things in accordance.

A trick you can use to have a custom sort on an object is to the use the Dual
http://qlikfornewbies.blogspot.com/2015/12/qvnewbie5-dual-function-in-qlikview_18.html

Qlikview will sort based on the number, but you can still see the textual display.
http://www.qlikfix.com/2010/12/27/creating-a-custom-sort-order-load-order-dual/

## Explain the purpose/functionality of common object properties

Within say a straight table there are also many sub options. For example, under the Dispaly options you can choose
```
Text
Image
Circular Gauge
Linear Gauge
Traffic Light Gauge
LED Gauge
Mini Chart
Link
```
Within the Mini Chart Settings you have yet more options!
```
Sparkline
Line with dots
Dots
Bars
Whiskers
```

A useful way of adding additional information about a chart to help your users is the Help Text property.
You can type this in on the Caption tab of an object.



Sometimes in charts you want the colors to persist. http://www.qlikfix.com/2010/12/17/consistent-dimension-colors/

There are a couple of ways to do this. You can script the values into the load script.
You can also check the check box called Persistent Colors.

Sometimes in charts you don't want the data to display until a selection has been made. This is done using the Calculate Condition property.

The Current Selections box is a quick and easy way to show the selections (although I like to use a more minimalized version)
Sometimes you might want to show the selections within a caption. In this case you can use the

    GetCurrentSelections()

### One very useful thing to do is add help text to your objects. To do this go to properties, Caption, Help Text. Once you populate the field a ? mark will show up that if they click will show the help text.




## Given a scenario, determine the appropriate application performance tuning option to use

Not really tuning, but if you need to change the screen size of your design window you can go to view, resize window, and then
change the resolution. 


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
    
## Other random topics

### how to calculate subset ratio. Subset ratio is the number of distinct values of this field found in this table as compared to the total number of distinct values of this field (that is other tables as well).

https://help.qlik.com/en-US/qlikview/November2017/Subsystems/Client/Content/Table_Viewer.htm
https://community.qlik.com/thread/80776

See the example below there are five unique occurences in the field F1 (numbers 1-5). The subset ratio in table A is 60% (3/5, ie 3 unique occurences as compared to 4 rows in the table). In table B the subset ratio will be 80% (numbers 1, 2, 4 and 5 as compared to the total the numbers 1-5, ie 4/5).

```ruby
A:
LOAD * INLINE [
    F1, F2
    1, A
    2, B
    3, C
    3, Cbis
];

B:
LOAD * INLINE [
    F1, F3
    1, I
    2, II
    4,  IV
    5, V
];
```





