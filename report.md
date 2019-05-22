# Applied Data Science Capstone Project

- [Applied Data Science Capstone Project](#applied-data-science-capstone-project)
  - [Introduction](#introduction)
  - [Data](#data)
  - [Methodology](#methodology)
  - [Results](#results)
    - [Cluster Analysis](#cluster-analysis)
      - [Cluster 0 (Red)](#cluster-0-red)
      - [Cluster 1 (Purple)](#cluster-1-purple)
      - [Cluster 2 (Blue)](#cluster-2-blue)
      - [Cluster 3 (Teal)](#cluster-3-teal)
      - [Cluster 4 (Light green)](#cluster-4-light-green)
      - [Cluster 5 (Orange)](#cluster-5-orange)
  - [Discussion](#discussion)
  - [Conclusion](#conclusion)

## Introduction

This is the final project for the IBM Data Science Professional Specialization course on Coursera. I will be using what I have learned about using location data and machine learning algorithms.

Tokyo and Osaka are two of Japan's largest cities.
Tokyo is located in the Kanto (East) region of Japan, while Osaka is located in the Kansai (West) region of Japan.

As two of the largest cities in Japan, it makes me wonder whether how the two cities are similar or differ from each other based on the nearby venues.

This project will use machine learning techniques to try and figure that out.

## Data

I will be obtaining my data from the web by scraping websites for data of the various wards in each cities, and their coordinates.

The data will be loaded onto a dataframe with columns for city, ward, latitude and longitude.

I will then use Foursquare's API to grab data of nearby venues for each ward.

The data will then be cleaned and formatted for use with a machine learning clustering algorithm.

After cluster labels have been assigned for each row of data, I will merged it with the original dataframe to show the names of the city and ward.

The clusters will then be visualised on a map using the folium library.

We should then be able to compare the clusters in the two cities for similarities or differences.

## Methodology

The first step is to gather the data required to do the analysis.
To do this, I used the Beautiful Soup library to scrape relevant wikipedia pages for the list of wards for Tokyo and Osaka.

Then, using the geocoder library and passing in the names of the ward, I was able to obtain coordinates for each ward. This is then visualised on a map using the folium library.

![map of tokyo](screenshots/tokyo_map.png)
*Map of Tokyo*

![map of osaka](screenshots/osaka_map.png)
*Map of Osaka*

Once that is done, I will need to gather information on the top venue categories in each ward using the Foursquare API.

The Foursquare API's explore endpoint takes in parameters for the radius from a coordinate to look for venues.
In order to determine the radius to use, I once again scrape wikipedia for the list of area size of each ward, then calculate the median area size for each city and finally, assuming that the area is a circle (which it is not) I calculate the radius using the formula to find the area of a circle.

Using the Foursquare API, I find up to 100 venues near each ward which is within the radius specified. The data is then grouped by wards and have the frequency of the venue categories converted to decimals so that it can be used with a clustering algorithm.

K-means is used as the clustering algorithm for this problem. K-means is an unsupervised clustering algorithm that allows a specific number of clusters to be specified for the outcome.

Judging by the number of wards in total, I have decided on a cluster size of 6. The clustering algorithm is applied on the data, and the resulting cluster labels is merged with the ward and city names which is then used to visualise the clusters on a map.

## Results

The results of the clustering algorithm is visualised in the screenshots below.

![Map of Osaka and Tokyo with Clustering](screenshots/tokyo_osaka_clustered.png)
*Map of Osaka and Tokyo with Clustering*

The screenshot above shows the two cities side by side and right away we can see that the colours are quite different for each city.
The screenshots below shows a close-up of each city.

![Map of Tokyo with Clustering](screenshots/tokyo_clustered.png)
*Map of Tokyo with Clustering*

![Map of Osaka with Clustering](screenshots/osaka_clustered.png)
*Map of Osaka with Clustering*

In addition to the visualisation of the clusters, we can also look at the wards and top venues for each cluster.

### Cluster Analysis

#### Cluster 0 (Red)

This cluster is the cluster coloured in red which contains 3 locations which are all in Tokyo. The most common venues in these areas are hotels and Japanese restaurants.

#### Cluster 1 (Purple)

Venues in this cluster are all located in Osaka with the number 1 most common venue being convenience stores for all of the wards in this list. This makes sense as looking at the cluster on the map, these wards are all on the outer area of the city. Other common venues are Ramen restaurants, Chinese restaurants, Donburi restaurants, etc.

#### Cluster 2 (Blue)

This cluster contains 5 wards in Osaka and 2 wards in Tokyo. The number 1 most common venue for all of the wards in this clusters are once again convenience stores. Other common venues in this cluster are intersections, supermarkets, parks, gyms, golf driving ranges, etc. So this seems to be clusters of wards which is good for recreational activities. I would say that these areas are good places to live in.

####  Cluster 3 (Teal)

This cluster has a few wards from Osaka. Looking at the map, this seems to be the cluster that most of Tokyo is in. It is also the cluster that the wards in the centre of Osaka is in. So we should be able to say that most of the areas in Tokyo that are similar to the city centre of Osaka. This makes sense as Osaka is less dense in population compared to Tokyo so in the areas of Tokyo which is less dense might be similar to central Osaka.

#### Cluster 4 (Light green)

The top venues in this cluster are Ramen restaurants with other common venues being parks, cafes, dessert shops, etc. It seems to be a more relaxing part of the cities. Looking at the map, wards in this cluster are on the outskirt of Tokyo and on the west of Osaka.

#### Cluster 5 (Orange)

This last cluster only has 1 ward which seems to be an outlier and is located in Osaka. The most common venue? Theme park rides. That's right, it's where Universal Studio Japan is located. Therefore, all the top venues in this area are rides, attractions, gift shop, hotels, etc. So understandably, this ward is different from most other wards in the data set.

Check the [Python Notebook](./Tokyo_vs_Osaka.ipynb) for the full results.

## Discussion

From the visualisation of the clusters on the map, we can tell that Osaka and Tokyo are both very unique despite that both of the are large cities in Japan.

One of the surprising thing from the result is how so many wards in Osaka has convenience stores as the number 1 most common venue compared to only 2 wards in Tokyo with convenience store as number 1.

It also appears that Osaka has a much higher frequency of Japanese style restaurants such as Ramen and Sushi restaurants. This seems to be the city to live in if you love exploring food.

It also seems that Ramen restaurants are very common in almost all of the wards. I guess there is no escaping from Ramen while in Japan.

Using the median area size of a ward for each city as the radius is not the most accurate way to gather venue data. This method assumes that each ward has a circular area, and all wards has similar sizes. The outcome is that if a ward is smaller than the median size then the Foursquare API would return data outside the specific ward. Likewise, for a ward that is larger, venue data outside that radius would not be included in the statistic.

## Conclusion

In conclusion, although these 2 large cities are both in Japan, based on the venue categories of places in each city, we can see that the 2 cities are quite different.

We were able to visualise the results on a map and analyse the clusters to determine why the clustering algorithms has clustered them in this way and make observations and discussions on the data.