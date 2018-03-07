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
But if you wanted to ignore selections in say the countryName


## Identify where alternate uses of expressions are appropriate


## Given a scenario, determine the appropriate function or complex expression to use


## Explain how to implement Actions/Triggers in the QlikView interface


## Given a scenario, determine the appropriate object or chart type to use


## Explain the purpose/functionality of common object properties


## Given a scenario, determine the appropriate application performance tuning option to use


## Given a scenario, determine the appropriate reload performance tuning option to use

