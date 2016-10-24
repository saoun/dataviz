# Cleaning Data

## Excel tricks

We’ll use Google Sheets in these examples, but Excel usually uses the same formula names (if you are using the English version).

The Find & Replace command is very helpful when cleaning data. Use it to change anything that doesn’t look right and follows a predictable pattern. Examples are weird notation symbols, an extra space at the end of each value, etc.

Use the <a href="https://support.google.com/docs/answer/3094133?hl=en">PROPER formula</a> to capitalize each word in a string if needed. Example usage: ``=PROPER(A2)``.

Use the <a href="https://support.google.com/docs/answer/3094123?hl=en">CONCATENATE formula</a> to combine the values of 2 columns into one column. Example usage: ``=CONCATENATE(A2," ",A3)``

<a href="https://productforums.google.com/forum/#!topic/docs/V-mVXdxshmM">Convert AM/PM times to HH:MM</a> easily by using ``=TEXT(A2,"HH:MM")``.

Use the <a href="https://support.google.com/docs/answer/3094136?hl=en">SPLIT formula</a> to split the contents of a cell into separate columns, based on a common symbol (a comma, for instance). Example usage: ``=split(A2,", ",false)``

Use <a href="https://support.google.com/docs/answer/56470?hl=en">Format -> Number</a> to make sure your cells with numbers are formatted appropriately. Here you can check things like thousand separators, the way dates are formatted, currencies notations, and more.

Taking care of multiple values: depending on your data visualization tool of choice, you might be able to visualize more than one value per data entry. For this to work, you need to separate the values with a character. A comma usually does the trick, but use another symbol if your values contain commas. 

## OpenRefine: hardcore cleaning time

<a href="http://openrefine.org/">OpenRefine</a> is a Java powered data cleaning tool that you can run locally and that works within your web browser. When using spreadsheet formulas to clean data doesn’t cut it, OpenRefine is your new best friend.

