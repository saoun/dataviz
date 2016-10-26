# Extracting and Scraping Data

Some sites already have their data organized in a table, allowing you to easily copy and paste it into a spreadsheet. Wikipedia is a good example of this. Others offer their data for download in a spreadsheet format. <br>

Sometimes, if you come across a website with structured information that isn’t downloadable or organized in a table, you might have to turn to specialized tools to extract your data.

## Import.io

<a hreh="https://www.import.io/">Import.io</a> is an easy tool that lets you extract data from any relatively structured website. Enter a URL on their homepage, and you will be quickly greeted by a structured data table. You can then export the data to a spreadsheet for further cleaning and enhancing.<br>

<img src="https://silk-blog.s3.amazonaws.com/blogpost-images/magick.png">

## Your Browser’s Developer Tools

Sometimes, you can actually copy data from the HTML source. The HTML source is available from your browser’s developer tools.<br>

The ‘Source’ tab shows you the page’s source. This can help you monitor which scripts pull the data and from where. Once you have this information, you could actually find the URL that directs you to a clean structured data. Here’s an <a href="http://apps.frontline.org/concussion-watch/#players_2014">example</a>. This interactive visualization on NFL concussion counts looks hard to scrape.<br>

<img src="https://silk-blog.s3.amazonaws.com/blogpost-images/datapostpart1-1.png">

But if you click in ‘Sources’ and analyze the code, you’ll find this:<br>

<img src="https://silk-blog.s3.amazonaws.com/blogpost-images/datapostpart1-2.png">

We end up with <a href="http://www.pbs.org/wgbh/pages/frontline/js/data/concussions/automated_newer.json">this link</a>, which contains a structured JSON file, ready to be converted to a spreadsheet file with a tool like OpenRefine.<br>

JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate.<br>

Sometimes, parts of a web page, such as interactive maps, are populated with data retrieved through API calls. A good alternative to scrape this data is to capture information by clicking on the ‘Network’ tab of your developer tools. Here, you’ll be able to monitor the network operations executed by the script used to run the web page. Sorting for bigger sizes and specific types of operation usually helps finding the script which returns the data you need. Then, you copy and paste the results previewed in the ‘response’ tab on the right into a text editor, and end up with a file containing the results of the API call used to retrieve the data you wanted.

## The Google Chrome Table Capture Extension

<a href="https://chrome.google.com/webstore/detail/table-capture/iebpjdmgckacbodjpijphcplhebcmeop">Table Capture</a> is a Google Chrome extension that converts data from a webpage into a spreadsheet.<br>

Install the extension, then navigate to a page you want to scrape. Clik on the extension, which will appear red if a table is automatically recognized. Select the table you want to scrape, and select Copy to Clipboard, or to Google Docs.

## The Google Chrome Scraper Extension

<a href="https://mnmldave.github.io/scraper/">Scraper</a> is a Google Chrome extension that converts data from a webpage into a spreadsheet.<br>

After you install the extension, visit the URL you want to scrape. Highlight an instance of the text you would like to convert to a table, right-click and choose ‘Scrape similar…’. You can directly export the results to a Google Sheet, or tweak the <a href="http://www.w3schools.com/xml/xpath_intro.asp">Xpath</a> values until you are satisfied with the result. Here is a <a href="https://www.youtube.com/watch?v=oCp9IcdSpZI&feature=youtu.be">video tutorial</a>.

<img src="https://silk-blog.s3.amazonaws.com/blogpost-images/datapostpart1-3.png">

## Google Sheets’ ImportXML Function

One of the most useful things when it comes to harvesting data from the web is learning how to use XPath expressions. XPath is “<a href="https://en.wikipedia.org/wiki/XPath">a query language for selecting nodes from an XML</a>”. Knowing how to use XPath to parse web pages will allow endless scraping possibilities, and help you build a spreadsheet from scratch. You can read more <a href="http://archive.oreilly.com/pub/a/perl/excerpts/system-admin-with-perl/ten-minute-xpath-utorial.html">here</a>.

For less complex scrapers, you’ll find that you don’t really need a deep knowledge of XPath to use it. For example, you can easily use XPath to construct web crawlers that turn thousands of pages into a structured spreadsheet.<br>

Let’s say I have a list of cities, and I want to pull in information about each from Wikipedia. This is how I would start:

<img src="https://silk-blog.s3.amazonaws.com/blogpost-images/datapostpart1-4.png">

To fill the image column, in cell C2, type:

``=importXML(B2,"//td/a/img/@src")``

The drag it down for all the other cities.

``//td/a/img/@src``
This is the XPath expression to query the url (stored in B1) and return the results contained in that specified path. To understand the exact path of what you need, you can view the source of a webpage and figure it out yourself. Or you can find the object you want (in this case the image), by right clicking on it and selecting ‘Inspect Element’. You will then view the page source. Find the url of the image you want, right click and select ‘Copy XPath’. You will now have saved on your clipboard the XPath needed to retrieve the image.<br>

<img src="https://silk-blog.s3.amazonaws.com/blogpost-images/datapostpart1-5.png">

You can repeat this to fill out all the other columns. For example, the first paragraph describing a city is accessible through:

``=JOIN(" ",importXML(B2, "//div[4]/p[1]"))``

--------

Info taken from this <a href="http://blog.silk.co/post/142737643047/data-journalism-tools-part-1-extracting-and">blog post</a>.


