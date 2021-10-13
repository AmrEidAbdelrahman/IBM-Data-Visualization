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
