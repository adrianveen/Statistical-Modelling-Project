# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
The goal of the projects is to demonstrate out knowledge in handling multiple APIs, combing datasets of different sources, creating a database, and performing EDA and regression analysis on the data. 

The above goals also include data cleaning, data visualization, and running and fine tuning regression models. 

## Process
### Step 1 - Planning/Strategizing
This step consisted of reviewing the project outline, and mapping out an approach prior to starting the work. This allowed for given steps to be followed to ensure that project requirements were not missed, and that time management was done effectively. 

This was done as part of a lesson learned from the last project that took a more unstructured and explorative approach. 

Despite planning, the merging of the POI data and the number of free bikes was initially missed. However, completing this step and simply rerunning the data visualization scripts was successful, avoiding much backtracking. 
### Step 2 - Experimenting/Testing
At the start of each of the parts outlined in assignment.md, the data was explored and manipulated in order to better understand it's structure, and also identify any issues. 

This consisted of scanning through the API outputs in their JSON format, and attempting some brute force methods to see how data could be obtained. Before the api calls, single longitude/latitude pairs were sent with the API calls in order to ensure that the GET request functions were working as intended. 

Once a good understanding of the data was established, the process of data cleaning began. This included a number of standard practices such as removing NULL/NaN values and duplicates, as well as recasting values as the correct data types. 

As the data was from two different sources, the values of the same data was often formatted differently. One example of this is the price column. Foursquare used a 1-4 integer scale, while Yelp used a $-$$$$ symbolic scale. The Yelp data was then reformatted into an integer value to match the Foursquare data. 

### Step 3 - Analyzing
Analyzing the data consisted of 2 separate parts: EDA, which involved investigating the descriptive statistics of the data as well as data visualization, and the next part was the regression modelling. 

One challenged faces here is that there were not many numeric values in the data set. If more time was available for the project, different fields or parameters may have been called from the APIs with a focus on numeric data. 

As a result, some fields like categories were not investigated that deeply and were soley investigated as a standalone value (ie. see the distribution of categories). 

The regression model chosen was a multivariate linear regression model. As there were no obvious patterns in the data when viewing scatterplots, it was not justifiable to use a more complicated model. 

### Step 4 - Interpreting
The final step is interpreting the regression model and EDA performed on the data. 

The regression model produced an R-squared value of only 0.08, implying that the model was not a very good fit. With the number of free bikes as the dependent variable, the most noteworthy independent variable was the latitude. As the latitude is always positive north of the equator, the negative coefficient of the latitude implied that the further north you go, you will see a larger number of free bikes. 

Thinking about the layout of Toronto, this intuitively makes sense: major entertainment, restaurant, and bar areas are focused around east-west corridors, such as bloor, dundas, college, queen and king. As they are running east-west, they would have a similar latitude. 

As a result, more bike stations are focused around these corridors, and less so along north south streets. This can be seen in the map with the coordinates plotted. From the heatmap, a weak correlation was seen between the price and the latitude as well, implying that more expensive areas for entertainment and eating tend to be further south in the city. 

## Results
(fill in what you found about the comparative quality of API coverage in your chosen area and the results of your model.)
Due to API call limits, only 200 bike station locations were chosen to call the Yelp and Foursquare APIs. Also in order to keep the data size manageable, the limit of POIs around each bike station was limited to 10 for each API. This also ensure that the results were of similar sizes.

As for the quality of the APIs, it initially seemed that Yelp had an advantage due to the price and rating fields. But after diving deeper into the documentation for Foursquare, it became apparent that Fourquare had many more *potential* data points. Whether or not these were all available in Toronto is unclear. It was also discovered that Fourquare also had rating and price information available, negating Yelp's advantage. 

The major issue noticed in the API results was that Yelp seemed to have data for locations that had permanently closed. The ratings also differed greatly from some locations when compared to google, which arguable has more traffic, and likely more accurate ratings. Although this last point was not confirmed on a larger scale, it was not seen in the Foursquare data to the same degree. 

In order to further compare the two, a more focused data set would need to be pulled, such as the maximum number of results returned for a single location. From there, one could discern if there were any discrepancies between the data provided by either API, and then confirm with a third source to attempt to confirm the accuracy. 


## Challenges 
There were many challenges faced during the time of this project, however, due to lessons learned from the SQL data cleaning project, they were handled more efficiently, or ignored as it was clear they would have little impact on the project. 

The different challenges are outlined below:
- Learning new APIs
    - Working with a new API and trying to combine it with another data set proved difficult. - Not all of the data aligned, and the new API required investigative work to determine how it was structured before any analysis could be started. 
- Some values were left un formatted, or unorganized
    - one example is the timestamp. Whether or not this value has any value is also unclear. 
        - It is a live timestamp, which means it will change each time you run the API call. 
        - It was only formatted into a usable value, but could still be cleaned up some more by rounding the seconds value for example
    - Another value that could have been further formatted was the distance. These values currently have up to 6 decimal places, for a measurement of metres.
        - These could have been rounded to 2 or 1 decimal places for a slightly neater database, but this was skipped over for the sake of saving time.
- Category names have many duplicates, or similar values
    - Each POI had multiple categories associated with it and both databases seemed to have main categories and subcategories
    - This resulted in the categories been excluded from the analysis to sum degree as there was not enough time to work on converting them into separate columns and numeric values
- Some categories requested did not show up as anticipated in the end results
    - Parks and Libraries were included as category parameters in the API calls, however, they did not seem to get pulled into the end data set. 
    - It is unclear why this happened, and with more time it would be nice to look into this issue
- API Limits
    - Yelp had a 24 hour limit of 500 API calls.
         - Since there were over 700 bike stations, the number of stations was reduced to 200. This would allow for a second call to be completed for all 200 if something went wrong with the first. 
         - As a result, the data was fairly limited.
         - One potential work around was to call the API twice over two days, and combine the responses, however, this would have slowed down the project timeline. 

## Future Goals
With more time, a number of changes would be made that would a) improve the data quality and size, and b) improve the quality of the analysis. 

- Due to API limitations the number of data points was limited. 
    - With more time (and money), ideally all bike stations would have been included, or all bike stations within a ploygon surrounding Toronto (eg. just the downtown core) would be included. 
    - The API's for foursquare and were limited to 10 POIs per API call.
        - With more time, these limits would be removed, in order to create a much larger data set. 
        - Instead of 10 POIs near a bike station, we may have been able to work with 500, which could have given our model many more data points to work with. 
- Another ambitious improvement on this process would be to expand the analysis to different cities, or compare one city to another and see what sort of patterns arise
    - from there you may be able to make inferences about bike stations or POIs based on a city's location or population for example. 
- I would have also included much more information in my API calls
    - With additional time, a deeper dive into the API documentation could have been done to create a much larger database
- In general, there could have also been more data cleaning done.
    - Checking for outliers could have been expanded to more columns or the categorical data as well.
- The categories was a large gap in the final product. 
    - the categories were separated into indivudal items, however, there still exists terms with overlap, or plural and singular versions of the same category. 
    - The categories in the SQL database were given a primary key, however, that primary key was not linked to the POIs
