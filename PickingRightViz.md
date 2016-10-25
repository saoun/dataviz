# Picking the right type of visualization

some basic visualization guidelines that can help you decide what type of visualization will work best for different types of data and how to show data relationships. These guidelines are also good general considerations beyond Silk for other visualization tools, particularly if you are building simple visualizations.

Here’s a short version of the Silk Visualization Guidelines:

* Use lists and tables to show simple ranking of data;
* Use maps for location-specific data;
* Use scatter plots to show the relationship between two numbers;
* Use donut and pie charts for showing proportions and distributions;
* Use vertical column charts to compare a few items;
* Use horizontal bar charts to compare many items;
* Use stack charts to show relative components as part of a whole;
* Use grids and mosaics to show images; and
* Use groups to organize items sharing a characteristic or property.
That’s the simple version. Here’s a longer one.

**Lists and tables**: These are particularly good if you want to show multiple data tags from a Silk in a simple format and if you want viewers to be able to sort the data quickly based on any of the tags. For things like salary databases, lists of real estate properties, or a ranking of sports teams by statistics, a table is the best bet.

**Maps**: Obviously locations are best shown on maps. Maps can also be a clear way to show numerical values grouped by location (a number plot). Silk’s mapping does a good job of handling multiple listings in the same location and also for letting users or Silk creators build maps from any number of location data types - street address, zip or postal code, state, country, city and more. Keep in mind that maps with many pins can be extremely confusing, particularly if the pins are grouped together. That’s why we often use inline filters.

**Scatter Plots**: These show one set of numerical values on the X-axis and another on the Y-axis. They are designed to show outliers and relationships between types of data. However, scatter plots are not good at all for ranking factors of comparing more than two data attributes. That’s why you may need to flip through multiple scatter plots to find clear relationships, outliers and data stories.

**Donut and pie charts**: Lots of people in the data visualization world hate pie charts. We don’t feel quite as vehemently, although we do like them better for displaying data about proportion or distribution of a smaller number of data values. Donut charts can handle a few more data values. In general, you never want to show more than 10 slices in one of these charts because the smaller slices quickly become indecipherable.

**Vertical column charts, horizontal bar charts and stack charts**: Flat out, horizontal charts look better on mobile. They also do a much better job showing a larger amount of data. For example, a horizontal column chart showing the 20 most expensive real estate markets in the U.S. would fairly easily handle that load and the horizontal direction of the labels inside or under the columns would scale up and down very nicely. In contrast, a vertical column chart would end up with an overly busy axis (which is why we remove the axis labels in responsive designs) and the columns might feel more tightly packed. Horizontal stack charts display with more data than horizontal column charts because the different colors of the stack elements make it easier to see the different data values in each stack. We’re big fans of colorful stack charts like the one in this article by the San Francisco Chronicle about the resegregation of San Francisco Schools.

**For Photos**: Grids, mosaics and maps. Anything with a picture or photo means you’ll want to pick one of these three visualization display types. Grids are basically photo galleries with data values underneath. Mosaics pack the pictures in more tightly, use smaller images, and have no data values underneath. You can add images to map location points in Silk - something that Bellingcat does very well with its Ukraine Conflict Vehicle Tracking Project. You can also display images in a table or list visualization type, but the images invariably cause the line spaces between table rows or list bullets to be so wide that it doesn’t display well.

**Groups**: Showing Datacards Organized by Like Values The group view is a simple three-column arrangement that shows datacard titles grouped by a data value. For example, in a Silk about the highest paid athletes, a group view might organize the athlete datacards by sport.

-----

Info taken from this [blog post](http://blog.silk.co/post/120086012962/picking-the-right-visualization-for-your-data)
