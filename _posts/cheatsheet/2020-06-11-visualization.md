---
layout: post-page
title: Data Visualization
description: Simple plotting of charts using Python
imgsrc: assets/images/tools/data_visualization.png
banner: assets/images/tools/data_visualization_banner.jpg
date: 2020-06-09
category: cheatsheet
tags: [Cheatsheet]
author: Song Jiaming
---
Disclaimer: This is just a notes from coursera course __Data Visualization with Python__

## Before you start
- Import the following to use matplotlib
{% highlight Python %}
%matplotlib inline # allows changes to the figure plotted inline
import matplotlib.pyplot as plt
{% endhighlight %}

## Basic Plotting with Matplotlib using Jupyter Notebook
{% highlight Python %}
plt.plot(5,5,'0') # plot a dot at coordinate (5,5) 
plt.show()

# Alternative plotting using pandas:
df.plot[kind='inline'], # note the x-axis is the index of the dataframe
{% endhighlight %}


### Line Plots
{% highlight Python %}
df.loc[index_name, [column_names]].plot(kind='line') # select the row of index_name and corresponding columns of column_names
plt.title('Title')
plt.ylabel('Y-axis label')
plt.xlabel('X-axis label')
plt.show()
{% endhighlight %}


### Area Plot
{% highlight Python %}
df.sort_values(['Total'], ascending = False, axis=1, inplace=True)
# remember to make your x_axis the index, different line/area in the plot: column, the height/area of the line: values
df.plot(kind='area')
plt.title('Title')
plt.ylabel('Y-axis label')
plt.xlabel('X-axis label')
plt.show
{% endhighlight %}

### Histogram and barchart
{% highlight Python %}
df.plot(kind='hist')

# OR
count, bin_edges = np.histograme[df['target_col']] # set the x axis to each bin of values in df['target_col']
df['target_col'].plot(kind='hist', xticks = bin_edges)

# barchat

df.plot(kind='bar') # vertical barchart
df.plot(kind='barh') # horizontal barchart
{% endhighlight %}


## Specialized Visualization Tools

### Pie Charts
{% highlight Python %}
df.plot(kind='pie')
{% endhighlight %}

### Box Plots
- From top to bottom, each elements represents: outliers, maximum, third quartile, median, first quartile, min, outliers
{% highlight Python %}
df.plot(kind='box')
{% endhighlight %}

### Scatter Plots
- Plot dependent variable against independent variable
{% highlight Python %}
df.plot(kind='box', x = 'independent_var_col', y ='dependent_var_col')
{% endhighlight %}

## Advanced Visualization Tools
### Waffle Charts
- Display progress toward goals
- The easiest way to create waffle chart is to use ```pywaffle```
- To implement our own waffle charts: 
	1. get proportion of each category
	2. define total size of waffle
	3. Map proportion to number of tiles for each category
	4. Creating a matrix to resemble waffle chart
	5. Map waffle matrix to visual and prettify the tiles
	6. Add legends

{% highlight Python %}

def create_waffle_chart(categories, values, height, width, colormap, value_sign=''):

    # compute the proportion of each category with respect to the total
    total_values = sum(values)
    category_proportions = [(float(value) / total_values) for value in values]

    # compute the total number of tiles
    total_num_tiles = width * height # total number of tiles
    print ('Total number of tiles is', total_num_tiles)
    
    # compute the number of tiles for each catagory
    tiles_per_category = [round(proportion * total_num_tiles) for proportion in category_proportions]

    # print out number of tiles per category
    for i, tiles in enumerate(tiles_per_category):
        print (df_dsn.index.values[i] + ': ' + str(tiles))
    
    # initialize the waffle chart as an empty matrix
    waffle_chart = np.zeros((height, width))

    # define indices to loop through waffle chart
    category_index = 0
    tile_index = 0

    # populate the waffle chart
    for col in range(width):
        for row in range(height):
            tile_index += 1

            # if the number of tiles populated for the current category 
            # is equal to its corresponding allocated tiles...
            if tile_index > sum(tiles_per_category[0:category_index]):
                # ...proceed to the next category
                category_index += 1       
            
            # set the class value to an integer, which increases with class
            waffle_chart[row, col] = category_index
    
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
    
    # add dridlines based on minor ticks
    ax.grid(which='minor', color='w', linestyle='-', linewidth=2)

    plt.xticks([])
    plt.yticks([])

    # compute cumulative sum of individual categories to match color schemes between chart and legend
    values_cumsum = np.cumsum(values)
    total_values = values_cumsum[len(values_cumsum) - 1]

    # create legend
    legend_handles = []
    for i, category in enumerate(categories):
        if value_sign == '%':
            label_str = category + ' (' + str(values[i]) + value_sign + ')'
        else:
            label_str = category + ' (' + value_sign + str(values[i]) + ')'
            
        color_val = colormap(float(values_cumsum[i])/total_values)
        legend_handles.append(mpatches.Patch(color=color_val, label=label_str))

    # add legend to chart
    plt.legend(
        handles=legend_handles,
        loc='lower center', 
        ncol=len(categories),
        bbox_to_anchor=(0., -0.2, 0.95, .1)
    )
{% endhighlight %}

## Set parameters for waffle
{% highlight Python %}
width = 40 # width of chart
height = 10 # height of chart

categories = df_dsn.index.values # categories
values = df_dsn['Total'] # correponding values of categories

colormap = plt.cm.coolwarm # color map class

# create waffle
create_waffle_chart(categories, values, height, width, colormap)
{% endhighlight %}

### Word Clouds
- need to install the package ```wordcloud```
{% highlight Python %}
# import package and its set of stopwords
from wordcloud import WordCloud, STOPWORDS

# let's use the stopwords that we imported from `word_cloud`. We use the function *set* to remove any redundant stopwords.
stopwords = set(STOPWORDS) # Stopwords are list of words which are stop words, which has no meanings

# the word 'said' has no meaning
stopwords.add('said')

# Create a word cloud object and generate a word cloud
# instantiate a word cloud object
word_count = WordCloud(
    background_color='white',
    max_words=2000, #use only 2k words first
    stopwords=stopwords
)

# generate the word cloud
word_count.generate(a_txt_file_with_words)

# Visualize:
fig = plt.figure()
fig.set_figwidth(14) # set width
fig.set_figheight(18) # set height

# display the cloud
plt.imshow(word_count, interpolation='bilinear')
plt.axis('off')
plt.show()
{% endhighlight %}

#### Put the word Clouds on a image mask

1. Open the image to a mask
```a_mask = np.array(Image.open('image.png'))```

2. Create wordcloud with the mask
{% highlight Python %}
word_count = WordCloud(
    background_color='white',
    max_words=2000, 
    stopwords=stopwords,
    mask=a_mask
)

word_count.generate(a_txt_file_with_words)

fig = plt.figure()
fig.set_figwidth(14) # set width
fig.set_figheight(18) # set height

plt.imshow(word_count, cmap=plt.cm.gray, interpolation='bilinear')
plt.axis('off')
plt.show()
{% endhighlight %}


### Seaborn and Regression Plots
{% highlight Python %}
import seaborn as sns
ax = sns.regplot(x='year', y='total', data=df, color='red', marker='+')
{% endhighlight %}



## Visualizing Geospatial Data - Folium
- Python library to create several types of leaflet maps
- Binding of data to a map for choropleth visualizations
- Passing visualizations as markers on the map

### Create a Map
{% highlight Python %}
import folium

world_map = folium.Map()

# Map for Canada
canada_map = folium.Map(
	location = [56.130, -106.35],
	zoom_start = 4,
	tiles = 'Stamen Toner' # different map styles
	)
{% endhighlight %}

### Add a marker
{% highlight Python %}
# Map for Canada
canada_map = folium.Map(
	location = [56.130, -106.35],
	zoom_start = 4
	)

# create a feature group
ontario = folium.map.FeatureGroup()
ontario.add_child(
	folium.features.CircleMarker(
			[56.130, -85.32],
			radius = 5,
			color = 'red',
			fill_color = 'red'
		)
	)

canada_map.add_child(ontario)

# label the marker
folium.Marker([56.130, -85.32], popup='Ontario').add_to(canada_map)
{% endhighlight %}

### Choropleth Maps
- Colored map from light to dark depending on the density
- Need a geojson file:
{% highlight json %}
{"type":"FeatureCollection","features":[
    {
        "type":"Feature",
        "properties":{"name":"Afghanistan"},
        "geometry":{"type":"Polygon","coordinates":[[[61.210817,35.650072],[61.210817,35.650072]]]},
        "id":"AFG"
    },
    {
        "type":"Feature",
        "properties":{"name":"Afghanistan"},
        "geometry" :{"type":"Polygon","coordinates":[[[],[]]],"id":"ALB" }
    }]
}
{% endhighlight %}

- Steps to create the map:
{% highlight python %}
# 1 Create a plain world map
world_map = folium.Map(
	zoom_start = 2
	tiles = 'Mapbox Bright' # different map styles
	)

# 2 load the geojson file
world_geo = r'world_countries.json'

world_map.choropleth(
	geo_path = world_geo,
	data = df_canada,
	columns = ['Country', 'Total'],
	key_on = 'feature.properties.name',
	fill_color = 'YlOrRd',
	legend_name = 'Immigration to Canada'

	)
{% endhighlight %}

#### References
1. [Data Visualization with Python](https://www.coursera.org/learn/python-for-data-visualization/home/welcome)