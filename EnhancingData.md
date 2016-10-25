# Enhancing Data

When you have extracted and cleaned your data, you might find that you are still missing a few things before you can get a story out of it. In this post, we’ll share some of our tricks on how to use the data points in your dataset to extract, calculate and lookup additional information. We’ll use Google Sheets in these examples, but Excel works the same, unless we say otherwise.

<br>

Let’s say you have a dataset you want to analyze, and it looks like this:

| Job Title | Job Offer | Link | Job Compensation Scrape | Tags Scrape | Job Compensation | Equity |
| --------- | --------- | ---- | ----------------------- | ----------- | ---------------- | ------ |
| Marketing/Growth Hacker | https://angel.co/liveongo/jobs/130607-marketing-growth-hacker | ₹300k - ₹500k · 0.0 - 0.05% | Full Time · Bangalore · Growth Hacker · Branding · Business Development · Business Strategy | ₹300k - ₹500k | 0.0 - 0.05% |

This is part of a list of job postings - scraped from a jobs database at angel.co - that include the keyword “Growth Hacker”. There’s a couple of columns with information for each job posting, including the URL, a salary indication, and a column with tags describing the job. On closer inspection you will notice there’s actually a lot more data hidden in those cells:<br>

* For one, the cells with descriptive tags contain multiple terms that are only useful as distinct values.
* The dataset has some abbreviated terms (the salary specification) that make them difficult to use.
* Also, that column with salary info actually only shows a range, not exact numbers, and they’re listed in various currencies.
* Finally, there is no separate column with the name of the company that posted the job opening, but that name is hidden in the URL of the job posting. So you want to distill that company name and put it in a separate column: the scrape actually included another dataset with background info on a lot of these companies, and so we want to add this information to our dataset. 

Now, how do you even begin to enhance your original dataset with all this hidden information? Let’s run by this step by step and see how using simple formulas in Excel or Google Sheets can solve all of the above

## Multiple values in one cell

When dealing with multiple values in one cell, you can split ranges with the <a href="https://support.google.com/docs/table/25273?hl=en">SPLIT formula</a>.

Example usage: You can use the SPLIT formula to split up all the different descriptive tags that are smooshed together in a single cell. In this case, the contents of one of the cells in column D looked like this: ‘Full Time · Remote OK · Marketing’. We can easily split this up on the · symbol. The formula would look like this: ``=SPLIT(D2,” · “,false)``.

Similarly, that column with salary information contains a range of numbers and looks like this: ‘$50k - $58k’. We can use the SPLIT formula again to get the ‘minimum salary’ and ‘maximum salary’ out of the salary range given in cell C2, using ``=SPLIT(C2," - ",false)``.

In Excel, use the <a href="https://support.office.com/en-us/article/Split-text-into-different-columns-with-the-Convert-Text-to-Columns-Wizard-30b14928-5550-41f5-97ca-7a3e9c363ed7?ui=en-US&rs=en-US&ad=US">Text to Columns</a> command.

## Working with ranges of numbers

You can convert abbreviated values with the <a href="https://support.google.com/docs/answer/3094215?hl=en">SUBSTITUTE formula</a>.

Example usage: As you could note, the salary ranges were expressed in an abbreviated way, such as ‘$50k’. Since we want to do some calculations with these numbers, we need the full salary amounts. One of the options then is using ``=SUBSTITUTE(C2,"k","000")``. Apply this formula, and ‘$50k’ will become ‘$50,000’.

You can calculate the median of numbers with the <a href="https://support.google.com/docs/answer/3094025?hl=en">MEDIAN formula</a>.

Example usage: We already have the minimum and maximum of the salary range that is offered, split up in cells G2 and H2. So let’s add the median salary that can be calculated from this range, using ``=MEDIAN(G2:H2)``.

## Normalizing multiple currencies

The <a href="https://support.google.com/docs/answer/3093281?hl=en">GOOGLEFINANCE formula</a> is great for working with multiple currencies.

Example usage: Unfortunately, different job postings from our dataset give salary ranges in different currencies. If we want to quickly compare our potential future income, we need to convert them into a single currency. Let’s say the dataset contained salaries specified in Euros and in US Dollars, and we want to normalize them and have a column with all salaries specified in US Dollars.

The GOOGLEFINANCE formula is normally used to fetch current securities information from Google Finance, but it also lets you look up the current conversion rate of two currencies. So we can create a formula that fetches the conversion rate of Euros to Dollars and then multiplies this figure with the salaries that are given in Euros. If cell I2 contains the ‘median salary’ that we calculated in Euros, we add the following formula to cell J2 ``=GOOGLEFINANCE(“EURUSD”)*I2`` to get that same median in Dollars.

Unfortunately Excel doesn’t have a comparable formula.

## Comparing and matching data from separate spreadsheets

Look up and match associated data from separate sheets or columns with the <a href="https://support.google.com/docs/answer/3093318?hl=en">VLOOKUP formula</a>.

The last thing missing from our wish list is getting additional company information. We don’t have the company name yet but we do have the URL of the job posting that contains the company name. So let’s get that name first, by splitting cell B2 containing the URL that looks like https://angel.co/tryfynd/jobs/132608-marketing-lead-growth-hacker. First, we execute ``=SPLIT(B2,”/jobs”,false)`` to get to the URL with more general info on the company (‘tryfynd’ in this case). Then we use this result in cell K2 and execute ``=SPLIT(K2,”angel.co/”,false)`` to distill just the company name in cell L2.

As mentioned before, we can combine this company name with additional information in another spreadsheet that might be relevant to us. Let’s say we’ve been working so far in ‘Sheet 1’ and we have a large dataset with data on hundreds of companies in ‘Sheet 2’. We know the companies looking for growth hackers are somewhere in ‘Sheet 2.’ In order to match them and add more data to our ‘Sheet 1’, we will need to use the following formula ``=VLOOKUP(L2,’Sheet 2’!A:E,2,false)``. This formula consists of 4 elements so let’s break it down:

* The first part L2 specifies what needs to be looked up - the company name in cell L2 of Sheet 1 in our case.
* The second part Sheet 2’!A:E specifies the range of columns where the formula needs to search for that company name - in our case that range contains columns A through E of Sheet 2.
* The third part, 2, specifies from which column within the range you want the formula to give you a result. This means that if column A of Sheet 2 contains the company name and column B its year of founding, the VLOOKUP formula we used will give us the matching year of founding from Sheet 2 for every company we have in Sheet 1.
* The last part of the formula is a true or false specifier. This element is part of several formulas (including the SPLIT formula). In the case of VLOOKUP it relates to how exact your match will be. By default, the formula will look for the first thing in the range that more or less matches what you are looking for. Often times you just want an exact match so you have to specify this by ending your formula with false.
You can add as many additional columns of data to ‘Sheet 1’ as you want by changing the third element of the ``VLOOKUP`` formula (changing the number will give you results from different columns within the range).

After applying all of the above formulas, the end result should be a spreadsheet ready for analysis. No need to stop there though: the options described in this post are far from exhaustive. If you want to explore more options see <a href="https://docs.google.com/spreadsheets/d/1LO-6VYHswRZVWYzZQQRffrQNuiaFKa7lbEZUiKSXi2M/edit#gid=2100432997">this spreadsheet</a> with the demo dataset of growth hacker job postings. Also make sure to check out <a href="https://support.google.com/docs/table/25273?hl=en">Google’s Spreadsheets function list</a>.

----

Info taken from this <a href="http://blog.silk.co/post/144293633212/tools-for-data-visualization-part-3-enhancing">blog post</a>.




































