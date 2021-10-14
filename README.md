# IBM-Data-Visualization


Why build visuals ?
- for explorator data analysis
- communicate data clearly
- share unbiased representation of data
- use them to support recommendation to different stackholders

When creating a visuals , always remember <a href='https://www.darkhorseanalytics.com/'>Darkhourse analytics</a> approach:
- less is more effictive
- less is more attractive
- less is more impactive

What is a line plot and why use it?
- A line chart or line plot is a type of plot which displays information as a series of data points called 'markers' connected by straight line segments. It is a basic type of chart common in many fields. Use line plot when you have a continuous data set. These are best suited for trend-based visualizations of data over a period of time.
- Line plot is a handy tool to display several dependent variables against one independent variable. However, it is recommended that no more than 5-10 lines on a single graph; any more than that and it becomes difficult to interpret.

### Histograms
- A histogram is a way of representing the frequency distribution of numeric dataset. The way it works is it partitions the x-axis into bins, assigns each data point in our dataset to a bin, and then counts the number of data points that have been assigned to each bin. So the y-axis is the frequency or the number of data points in each bin. Note that we can change the bin size and usually one needs to tweak it so that the distribution is displayed nicely.

```python
count, bin_edges = np.histogram(df_can['2013'])

print(count) # frequency count
print(bin_edges) # bin ranges, default = 10 bins
#By default, the histrogram method breaks up the dataset into 10 bins.
```
the histogram plot divid the xticks in wrong way but with us the xticks as a parameter and assign the bin_edges the x_axis will be good

#### Side Note: We could use df_can['2013'].plot.hist(), instead. In fact, throughout this lesson, using some_data.plot(kind='type_plot', ...) is equivalent to some_data.plot.type_plot(...). That is, passing the type of the plot as argument or method behaves the same


```python
#Tip: For a full listing of colors available in Matplotlib, run the following code in your python shell:

import matplotlib
for name, hex in matplotlib.colors.cnames.items():
    print(name, hex)
```

### Bar Charts (Dataframe) 
- A bar plot is a way of representing data where the length of the bars represents the magnitude/size of the feature/variable. Bar graphs usually represent numerical and categorical variables grouped in intervals.
To create a bar plot, we can pass one of two arguments via kind parameter in plot():
  - kind=bar creates a vertical bar plot
  - kind=barh creates a horizontal bar plot


### Pie Charts 
- A pie chart is a circular graphic that displays numeric proportions by dividing a circle (or pie) into proportional slices. You are most likely already familiar with pie charts as it is widely used in business and media. We can create pie charts in Matplotlib by passing in the kind=pie keyword.


### We will use pandas groupby method to summarize the immigration data by Continent. The general process of groupby involves the following steps:
- Split: Splitting the data into groups based on some criteria.
- Apply: Applying a function to each group independently: .sum() .count() .mean() .std() .aggregate() .apply() .etc..
- Combine: Combining the results into a data structure.
<br><img src='groupby.jpg'><br><br>

### Box Plots 
A box plot is a way of statistically representing the distribution of the data through five main dimensions:
    - Minimum: The smallest number in the dataset excluding the outliers.
    - First quartile: Middle number between the minimum and the median.
    - Second quartile (Median): Middle number of the (sorted) dataset.
    - Third quartile: Middle number between median and maximum.
    - Maximum: The largest number in the dataset excluding the outliers.
<br><br><img src='https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DV0101EN-SkillsNetwork/labs/Module%203/images/boxplot_complete.png'><br><br>


## Subplots
Often times we might want to plot multiple plots within the same figure. For example, we might want to perform a side by side comparison of the box plot with the line plot of China and India's immigration.

To visualize multiple plots together, we can create a figure (overall canvas) and divide it into subplots, each containing a plot. With subplots, we usually work with the artist layer instead of the scripting layer.

Typical syntax is :
```python
    fig = plt.figure() # create figure
    ax = fig.add_subplot(nrows, ncols, plot_number) # create subplots
```
Where:
    - nrows and ncols are used to notionally split the figure into (nrows * ncols) sub-axes,
    - plot_number is used to identify the particular subplot that this function is to create within the notional grid. plot_number starts at 1, increments across rows first and has a maximum of nrows * ncols as shown below.

### Tip regarding subplot convention
In the case when nrows, ncols, and plot_number are all less than 10, a convenience exists such that a 3-digit number can be given instead, where the hundreds represent nrows, the tens represent ncols and the units represent plot_number. For instance,
```python
   subplot(211) == subplot(2, 1, 1) 
```
produces a subaxes in a figure which represents the top plot (i.e. the first) in a 2 rows by 1 column notional grid (no grid actually exists, but conceptually this is how the returned subplot has been positioned).

> The box plot is an advanced visualizaiton tool, and there are many options and customizations that exceed the scope of this lab. Please refer to Matplotlib documentation on box plots for more information.

### Scatter Plots 
A scatter plot (2D) is a useful method of comparing variables against each other. Scatter plots look similar to line plots in that they both map independent and dependent variables on a 2D graph. While the data points are connected together by a line in a line plot, they are not connected in a scatter plot. The data in a scatter plot is considered to express a trend. With further analysis using tools like regression, we can mathematically calculate this relationship and use it to predict trends outside the dataset.


### Bubble Plots 
A bubble plot is a variation of the scatter plot that displays three dimensions of data (x, y, z). The data points are replaced with bubbles, and the size of the bubble is determined by the third variable z, also known as the weight. In maplotlib, we can pass in an array or scalar to the parameter s to plot(), that contains the weight of each point.


### Waffle Charts 
A waffle chart is an interesting visualization that is normally created to display progress toward goals. It is commonly an effective option when you are trying to add interesting visualization features to a visual that consists mainly of cells, such as an Excel dashboard.
Unfortunately, unlike R, waffle charts are not built into any of the Python visualization libraries. Therefore, we will learn how to create them from scratch.
- Step 1. The first step into creating a waffle chart is determing the proportion of each category with respect to the total.
    ```python
        # compute the proportion of each category with respect to the total
        total_values = df_dsn['Total'].sum()
        category_proportions = df_dsn['Total'] / total_values

        # print out proportions
        pd.DataFrame({"Category Proportion": category_proportions})
    ```
- Step 2. The second step is defining the overall size of the waffle chart.
    ```python
    width = 40 # width of chart
    height = 10 # height of chart

    total_num_tiles = width * height # total number of tiles

    print(f'Total number of tiles is {total_num_tiles}.')
    ```
- Step 3. The third step is using the proportion of each category to determe it respective number of tiles.
    ```python
    # compute the number of tiles for each category
    tiles_per_category = (category_proportions * total_num_tiles).round().astype(int)

    # print out number of tiles per category
    pd.DataFrame({"Number of tiles": tiles_per_category})
    ```
- Step 4. The fourth step is creating a matrix that resembles the waffle chart and populating it.
    ```python
    # initialize the waffle chart as an empty matrix
    waffle_chart = np.zeros((height, width), dtype = np.uint)

    # define indices to loop through waffle chart
    category_index = 0
    tile_index = 0

    # populate the waffle chart
    for col in range(width):
        for row in range(height):
            tile_index += 1

            # if the number of tiles populated for the current category is equal to its corresponding allocated tiles...
            if tile_index > sum(tiles_per_category[0:category_index]):
                # ...proceed to the next category
                category_index += 1       

            # set the class value to an integer, which increases with class
            waffle_chart[row, col] = category_index

    print ('Waffle chart populated!')
    ```
- Step 5. Map the waffle chart matrix into a visual.
    ```python
    # instantiate a new figure object
    fig = plt.figure()

    # use matshow to display the waffle chart
    colormap = plt.cm.coolwarm
    plt.matshow(waffle_chart, cmap=colormap)
    plt.colorbar()
    plt.show()
    ```
- Step 6. Prettify the chart.
    ```python
    # instantiate a new figure object
    fig = plt.figure()

    # use matshow to display the waffle chart
    colormap = plt.cm.coolwarm
    plt.matshow(waffle_chart, cmap=colormap)
    plt.colorbar()

    # get the axis
    ax = plt.gca()

    # set minor ticks
    ax.set_xticks(np.arange(-.5, (width), 1), minor=True)
    ax.set_yticks(np.arange(-.5, (height), 1), minor=True)

    # add gridlines based on minor ticks
    ax.grid(which='minor', color='w', linestyle='-', linewidth=2)

    plt.xticks([])
    plt.yticks([])
    plt.show()
    ```
- Step 7. Create a legend and add it to chart.
    ```python
    # instantiate a new figure object
    fig = plt.figure()

    # use matshow to display the waffle chart
    colormap = plt.cm.coolwarm
    plt.matshow(waffle_chart, cmap=colormap)
    plt.colorbar()

    # get the axis
    ax = plt.gca()

    # set minor ticks
    ax.set_xticks(np.arange(-.5, (width), 1), minor=True)
    ax.set_yticks(np.arange(-.5, (height), 1), minor=True)

    # add gridlines based on minor ticks
    ax.grid(which='minor', color='w', linestyle='-', linewidth=2)

    plt.xticks([])
    plt.yticks([])

    # compute cumulative sum of individual categories to match color schemes between chart and legend
    values_cumsum = np.cumsum(df_dsn['Total'])
    total_values = values_cumsum[len(values_cumsum) - 1]

    # create legend
    legend_handles = []
    for i, category in enumerate(df_dsn.index.values):
        label_str = category + ' (' + str(df_dsn['Total'][i]) + ')'
        color_val = colormap(float(values_cumsum[i])/total_values)
        legend_handles.append(mpatches.Patch(color=color_val, label=label_str))

    # add legend to chart
    plt.legend(handles=legend_handles,
               loc='lower center', 
               ncol=len(df_dsn.index.values),
               bbox_to_anchor=(0., -0.2, 0.95, .1)
              )
    plt.show()
    ```
There seems to be a new Python package for generating waffle charts called PyWaffle, but it looks like the repository is still being built. But feel free to check it out and play with it.














