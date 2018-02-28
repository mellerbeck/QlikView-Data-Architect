### Given a set of business objectives, determine KPIs, dimensions, or measures

#### What is a Measure (Expression) - Stolen from https://community.qlik.com/blogs/qlikviewdesignblog/2013/03/25/dimensions-and-measures

When you make a chart, you should start by asking yourself “What do I want to show?” The answer is usually Sales, Quantity or some other number. This is your Measure. In QlikView we have traditionally called this an “Expression”, but "Measure" is really the correct word. (There are expressions that are not measures, e.g. expressions used as labels, or as sort order definitions).

A database or a QlikView app can consist of thousands or millions of records that each contains a small piece of information. A Measure is simply a calculation that can be made over multiple records in this data set. The calculation always returns one single value that summarizes all relevant records. This type of calculation is called an aggregation. There are several aggregation functions: Sum(), Count(), Min(), Max(), etc.

Examples:

Each record contains a sales number. Then Sum(Sales) is a relevant measure that calculates the total sales value.
Each record represents an order and “OrderID” is the key. Then Count(OrderID) is a relevant measure that calculates the number of orders.
 

A Measure can be used almost anywhere in QlikView: In charts, in text boxes, as label for objects, in gauges, etc. Typical measures are all KPI:s, Revenue, Number of orders, Performance, Cost, Quantity, Gross Margin, etc.

__Once again: A Measure is always based on an aggregation. Always!__

#### What is a Dimension
The second question you should ask yourself is “How many times should this be calculated? Per what do I want to show this measure?” The answer could be once per Month, per Customer, per Supplier or something similar. This is your Dimension.

Contrary to Measures, dimensions are descriptive attributes – typically textual fields or discrete numbers. A dimension is always an array of distinct values and the measure will be calculated once per element in the array.

Example:

The field “Customer” is used as dimension. The individual customers will then be listed and the measure will be calculated once per customer.
 

Typical dimensions are Customer, Product, Location, Supplier, Activity, Time, Color, Size, etc.


### Given customer requirements, determine an appropriate solution to meet the customer needs

There are lots of varied ways to deploy QVW applications to users.
  * Publish to Access Point and access using Qlikview Plugin with IE
  * Publish to Access Point and access using AJAX mode
  * Publish to Access Point and access using Qlikview Mobile APP https://help.qlik.com/en-US/qlikview/12.0/pdf/QlikView%20Mobile%20Client.pdf
  * Distribuition task that Emails a QVW to a user
  
 Also, depending on the device you need to tailor the APP appropriately. For example, is your main user on a mobile device? If so, choose a 
 smaller screen resolution. Don't choose sheet objects that are hard to manipulate on a small screen. (Bug buttons work nicely)
 
 Qlikview has a rudimentary built in report function. It sort of works. If you needed to say split it out by a group you can use
 the Banding functionality. https://www.quickintelligence.co.uk/qlikview-reports/
 
 One other common requirement is Handling Multiple Languages
 https://community.qlik.com/blogs/qlikviewdesignblog/2012/11/30/handling-multiple-languages
 You can do it many different ways, using variables or you also can have a language definition table and a selection to choose the language.

If you need to calculate something that is not in the data model if it is a Dimension you would use the Calculated Dimension button. 
 
One other common requirement is handling multiple currencies. One way to do this is to have a table that has a currency multiplier. 
 
