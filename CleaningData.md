# Cleaning Data

## Excel tricks

Google Sheets is used in these examples, but Excel usually uses the same formula names.

The [Find & Replace](https://support.google.com/docs/answer/62754?co=GENIE.Platform%3DDesktop&hl=en) command is very helpful when cleaning data. Use it to change anything that doesn’t look right and follows a predictable pattern. Examples are weird notation symbols, an extra space at the end of each value, etc.

Use the <a href="https://support.google.com/docs/answer/3094133?hl=en">PROPER formula</a> to capitalize each word in a string if needed. Example usage: ``=PROPER(A2)``.

Use the <a href="https://support.google.com/docs/answer/3094123?hl=en">CONCATENATE formula</a> to combine the values of 2 columns into one column. Example usage: ``=CONCATENATE(A2," ",A3)``

<a href="https://productforums.google.com/forum/#!topic/docs/V-mVXdxshmM">Convert AM/PM times to HH:MM</a> easily by using ``=TEXT(A2,"HH:MM")``.

Use the <a href="https://support.google.com/docs/answer/3094136?hl=en">SPLIT formula</a> to split the contents of a cell into separate columns, based on a common symbol (a comma, for instance). Example usage: ``=split(A2,", ",false)``

Use <a href="https://support.google.com/docs/answer/56470?hl=en">Format -> Number</a> to make sure your cells with numbers are formatted appropriately. Here you can check things like thousand separators, the way dates are formatted, currencies notations, and more.

Taking care of multiple values: depending on your data visualization tool of choice, you might be able to visualize more than one value per data entry. For this to work, you need to separate the values with a character. A comma usually does the trick, but use another symbol if your values contain commas. 

## OpenRefine: hardcore cleaning time

<a href="http://openrefine.org/">OpenRefine</a> is a Java powered data cleaning tool that you can run locally and that works within your web browser. When using spreadsheet formulas to clean data doesn’t cut it, OpenRefine is your new best friend.<br>

Let's check out this example: One column in the dataset looked like this, showing the yearly salary and equity together:

| Job Compensation |
| ---------------- |
| ₹1200k - ₹2200k · 0.0 - 0.25% |
| $3k - $30k · 0.0 - 2.0% |
| $50k - $75k · 0.0 - 1.0% |
| $70k - $90k · No equity |
| 5.0 - 10.0% |

OpenRefine lets you use formulas to split the values into 2 columns, like this:

| Job Compensation | Equity |
| ---------------- | ------ |
| ₹1200k - ₹2200k | 0.0 - 0.25% |
| ¥20k - ¥100k | 0.0 - 2.0% |
| £1k - £2k | 0.0 - 1.0% |
| ₹600k - ₹1000k | No equity | 
|  | 5.0 - 10.0% |

Here were the steps to follow:

Pick Edit Column -> Add Column Based on This Column. Name the column “Equity”.
Use the following expression: ``value.split(‘ · ‘)[-1]``. This takes all values that occur before the ‘·’ character in the ‘Job Compensation’ column, and places them in a new column.
Then on the ‘Job Compensation’ column, pick Edit Cells -> Transform. As the expression, use ``value.split(‘ · ‘)[0]``. This removes everything before the ‘·’ character.
To clean up values without a currency symbol, pick Facet -> Text Facet. Select all cells with no currency symbol. Then pick Edit Cells -> Transform Use the expression: leave empty.

## Read more

<a href="https://github.com/wireservice/csvkit">csvkit</a> is a suite of command line utilities for converting to and working with CSV files. Not for the faint of heart, but very useful for manipulating large datasets, examining datasets, performing SQL like queries, joining multiple csv files, and much more.
There are tons of other great resources on data cleaning and data journalism in general: check out <a href="https://support.office.com/en-us/article/Top-ten-ways-to-clean-your-data-2844b620-677c-47a7-ac3e-c2e157d1db19">Microsoft’s cleaning guide</a>, <a href="http://schoolofdata.org/handbook/recipes/cleaning-data-with-spreadsheets/">The School of Data</a>, and <a href="https://infoactive.co/data-design/ch08.html">Data + Design</a>, to name a few.

---------

Info taken from this <a href="http://blog.silk.co/post/143527419532/tools-for-data-visualization-part-2-cleaning-data">blog post</a>.
















