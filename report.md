# Applied Data Science Capstone Project

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