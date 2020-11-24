# Assignment bootcamp-2020-13-final

In your final assignment notebook, create three figures:
1. Figure 1: Precipitation over time for Boulder, CO and San Francisco, CA.
2. Figure 2: Stream discharge for the 2013 Colorado floods for four sites in Colorado. 
3. Figure 3: An interactive map showing stream gage locations used to create figure 2

NOTE: We follow the USGS spelling of **gage**. :) 

This notebook is less structured than the previous notebooks. There are no 
intermediate steps or checks. 

Requirements for the notebook and for each figure are below. 

## Overall Assignment Requirements 

Remember to follow best practices for code organization, readability 
and reproducibility in your notebook.

* Add cells as you need to above the tested plot cells and below the function cells to process your data

### Notebook Organization:
    * Imports should all be at the top.
    * Followed by function definitions.
    * Followed by setting working directory (as needed).
    * Followed by all other code needed for workflow.

### DRY Code & PEP 8
* Use DRY code and other strategies for readability and reproducibility:
    * Reduce your code wherever possible - use the outputs of selections and functions as the inputs to other functions, plot inputs, etc. Balance combining code with readbility to ensure that the workflow is clear and easy to follow.
    * Use code that is reproducible across different computers (e.g. paths) as needed.
    * Follow PEP 8 guidelines for line lengths, white space, etc, to support readibility.


### Add Markdown Cells to Describe Each Figure

* Throughout the notebook, use Markdown cells to identify different sections of 
the code (e.g. a section for Precipitation Patterns of Boulder, CO and 
San Francisco, CA). 

* Use markdown to describe patterns that you find in each figure and subplot.

### Assignment Tips

* Build your code incrementally: complete the workflow first without functions or loops to ensure that you have the components needed for the workflow. Once your code works, create your function and run it 
on a single file.
* Once your function is working successfully on one city, write loop to run your function for all cities. Sometimes it may be helpful to write your loop  incrementally as well using  print  statements  to ensure it's outputing what you think it is.
* You can use `plt.tight_layout()` (and play with the figsize) in your plot code to have matplotlib automatically space the subplots evenly within a figure. 
* You can use `plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', prop={'size': 11})` to  adjust the location and font size of a legend. This might be especially helpful for Figure 2.

        
*********

# Assignment Requirements

Below each figure that you create  below, add a markdown cell describing 
patterns that you see in the data. The third plot is a map so that markdown
cell can serve as a caption.

## Figure 1: Precipitation Over Time For Boulder, CO and San Francisco, CA 

Create a figure with two subplots.

For the first subplot you should be able to create a single DataFrame containing
the monthly total precipitation for each individual month in each year across both sites.
Use that `DataFrame` the calculate the following:

### Subplot 1: Monthly Max Precipitation Values (inches) for 1989 to 2018 - 12 Values (one value for each month summarized across all years)

* The first subplot should display **Monthly Max Precipitation Values (inches) for 1989 to 2018** for both cities (i.e. both cities on one plot).
    * **NOTE** You should calculate the max month value across all years for each month. Thus you will have a total of 12 values in your plot - one for each month. (for example the max monthly value for jan, the max monthly value for feb, etc)
    
### Subplot 2:  Annual Maximum Monthly Precipitation Value  (inches) for 1989 to 2018 - One Value for Each Year
* One subplot displaying the **Annual Maximum Precipitation Value s(inches) for 1989 to 2018** for both cities (i.e. both cities on one plot). To create this plot you will use the monthly total precipitation
values and calculate the highest precipitation value in a month for each year.
You will thus have a single value representing maximum precipitation for each year.

### General Plot Requirements for Figure 1
* Include a legend for each subplot.
* Use different colors, line styles, etc to highlight each site (i.e. each city should be a unique color/style that is used again across the plots). 
* For each plot, be sure to include appropriate titles and axes labels including units of measurement where appropriate.
* Use a loop to plot your data to avoid *copy pasta* (redundant) code

### Create *Atleast* One Function To Support Processing the Data For Figure 1

Create a function that:

* Imports a `.csv` file into **pandas** DataFrames and 
    * Resamples the data to be a monthly sum instead of a daily sum.
    * The function should parse dates from the "DATE" column and set that column as the index.
    * The function should also add a columns "months" to the `DataFrame`, which is the numeric value of each month.
    * Finally the function should add a site name column and the site x,y location to the dataframe which will allow you to combined both datasets into a single dataframe for plotting.
    * **NOTE:** If you properly read the index in as a datetime object, you can create the months column from the return of `df.index.months`. 


### About the Precipitation Data For Figure 1  

The precipitation data that you will use for figure one can be downloaded 
here: `https://ndownloader.figshare.com/files/25564340`

Files in the download:
* **boulder-daily-precip-1948-2018.csv**
* **san-fran-daily-precip-1948-2018.csv**

The data contained in the download above are total daily precipitation 
(inches) from Boulder, CO and San Francisco, CA. The data were collected 
between 1948 and 2018. The precipitation data values are stored in the `PRCP`.     

You can download the original data from 
<a href="https://www.ncdc.noaa.gov/cdo-web/" target="_blank">U.S. National Oceanic and Atmospheric Administration (NOAA)</a>. Specifics for each can be found in the `README.md` included in the download.

*********


## Figure 2: Stream Discharge Data - 2013 Colorado Floods

Create a figure with two subplots:

### Subplot 1: the **Daily Mean Discharge** (cubic feet per second, CFS) for **Aug - Oct 2013** for all four sites (i.e. all sites on one plot).

* This plot should have four lines, one for each site, covering only the time extent between August 1st, 2013, and October 31st, 2013. 

### Subplot 2:  the **Annual Maximum of Mean Discharge** (cubic feet per second, CFS) for **1990-2018** for all four sites (i.e. all sites on one plot).

* This plot should also only have four lines, one for each site. Each line should be the maximum daily discharge for each year between 1990 and 2018 for each of the four streams. 

### General Plot Requirements for Figure 2

* Include a legend for each subplot and make sure your legend doesn't cover your data.
* Use a different color and or line styles to represent each unique  site location. 
* For each plot, be sure to include appropriate titles and axes labels including units of measurement where appropriate.


### Figure 2 Function 

* Write a function that combines the `hydrofunctions` tasks needed to create a pandas dataframe from the downloaded data for each site.
* in your function, rename the columns in the dataframe to more descriptive names (e.g. discharge and flag)
* Add site name, latitude, and longitude columns to your dataframe.
    * Hint: you can use the `hydrofunctions` function `hydrofunctions.get_nwis_property()`  to get the site name from the site you're working on. Documentation on how to use this function can be found [on the hydrofunctions read the docs page](https://hydrofunctions.readthedocs.io/en/master/hydrofunctions.html#hydrofunctions.hydrofunctions.get_nwis_property). The two properties you will be interested in are `siteName` and `geoLocation`. Look at the return of this function outside of your own function to see how to get the information you want from it!
* Use a loop to apply your function to each of the four sites (i.e. use a loop to create the dataframe for each site).
* Use a loop to plot your data to avoid *copy pasta* (redundant) code


### About the  Stream Discharge Data

For this section of the report, you will use the `hydrofunctions` package in your conda environment to programmatically download stream discharge data for **January 1, 1990 through December 31, 2018 for four U.S. Geological Survey (USGS) stream gages across Colorado**:
1. site `06730500` for the [Boulder Creek Station near Longmont, CO](https://waterdata.usgs.gov/nwis/inventory/?site_no=06730500) in Weld County (Northern Colorado)
2. site `09105000` for the [Plateau Creek Station near Cameo, CO](https://waterdata.usgs.gov/nwis/inventory/?site_no=09105000) in Mesa County (Western Colorado)
3. site `07106300` for the [Fountain Creek Station near Pinon, CO](https://waterdata.usgs.gov/nwis/inventory/?site_no=07106300) in Pueblo County (Central Colorado)
4. site `07126390` for the [Lockwood Canyon Creek Station near Thatcher, CO](https://waterdata.usgs.gov/co/nwis/inventory/?site_no=07126390) in Las Animas County (Southeastern Colorado)

The [documentation for hydrofunctions package](https://hydrofunctions.readthedocs.io/en/master/usage.html) provides instructions and examples for using functions in this package to download data directly from the USGS National Water Information System (NWIS) and create a pandas dataframe. 

The `DataFrame` created by the hydrofunctions functions will include the following:
* Daily mean stream discharge in cubic feet per second (CFS) in column called `USGS:` plus site info (e.g. `USGS:06730500:00060:00003`) 
* An indicator (or flag) of quality of measurement in column called called `USGS:` plus site info and `_qualifiers`(e.g. `USGS:06730500:00060:00003_qualifiers`)
* "No data" values already addressed by hydrofunctions

### Helpful Tips For Figure 2

Review [map of Colorado counties](https://geology.com/county-map/colorado.shtml) as well as the wikipedia entries on the [2013 Colorado Floods](https://en.wikipedia.org/wiki/2013_Colorado_floods) and other events that have occurred at [Fountain Creek](https://en.wikipedia.org/wiki/Fountain_Creek_(Arkansas_River_tributary)) to  help you describe / interpret patterns seen in the stream discharge data plots.

*********


## Figure 3: Interactive Map with Stream Gage Locations

Create an interactive folium map that shows the x,y location of the four  
stream  gages t hat you used to create Figure 2. If you grabbed the x,y location
in your Figure 2 function, you should be able to grab the x,y locations from
that `DataFrame` to create your final plot. 


