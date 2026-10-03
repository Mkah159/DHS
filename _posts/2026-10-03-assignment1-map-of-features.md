---
title: "Mapping Poland with GeoNames"
date: 2026-10-03
excerpt: "Exploring Poland through five GeoNames feature layers."
tags:
  - Assignments
  - Interactive Map
  - Data and Human Space
---



For this project, I chose **Poland** because it is a country that I already had a personal connection with. I have visited places such as Kraków, Gdańsk, and Zakopane, and those trips stayed with me because of the different tourist attractions and landscapes I experienced in each place. Kraków stood out to me because of its historic center, architecture, and the amount of activity around the city. Gdańsk felt very different because of its northern location, waterfront setting, and unique city atmosphere. Zakopane was probably the clearest example of how different Poland’s geography can be, because the mountain landscape there is very different from the flatter parts of the country. Because I had already visited these places, I was interested to see whether the GeoNames data would show some of the same differences that I remembered from traveling in Poland. I already knew that the north has many lakes and that the south has mountain areas, so I expected the dataset to show clear regional patterns.

The Poland GeoNames file contained **58,566 rows** and 19 variables. Each row represents a geographic feature. GeoNames organizes places using feature codes. The largest category was `PPL`, which represents populated places, with **43,785 records**.

I decided not to use `PPL` because more than 43,000 points would make the map too crowded. Instead, I chose five feature types:

- **Lakes (`LK`)** – 1,063 locations
- **Mountains (`MT`)** – 928 locations
- **Railroad Stations (`RSTN`)** – 516 locations
- **Streams (`STM`)** – 1,095 locations
- **Hotels (`HTL`)** – 1,078 locations

I chose these five because their numbers were more balanced and they gave me a mix of natural and human-made features.

## My Interactive Map

I created an interactive Leaflet map that allows users to turn the five layers on and off. The map also has a legend and clickable markers with information about each location.

<div style="margin: 25px 0;">
  <iframe
    src="{{ '/assets/maps/PL_featuremap.html' | relative_url }}"
    title="Interactive Poland GeoNames map"
    width="100%"
    height="650"
    style="border: 1px solid #ddd;"
    loading="lazy">
  </iframe>
</div>



The image below shows the map with **all five layers turned on**.

<p align="center">
  <img
    src="{{ '/assets/images/poland-map-all-layers.jpg' | relative_url }}"
    alt="Interactive map of Poland showing lakes, mountains, railroad stations, streams, and hotels"
    width="750">
</p>

*Figure 1. The Poland GeoNames map with all five feature layers displayed.*

## Patterns I Found

One of the clearest things I noticed was that the five feature types were not spread evenly across Poland.

The **mountain layer** showed a strong pattern in southern Poland, especially near the borders with Slovakia and the Czech Republic. This matched what I expected because Poland's main mountain areas are in the south.

The **lake layer** showed a different pattern. Many lakes appeared in northern Poland. When I turned off the other layers and looked only at lakes, this became much easier to see. The lakes were not spread equally across the whole country.

The **stream layer** was more spread out across the country, while the **railroad station layer** appeared more connected to developed and populated areas. This showed how different types of features can create very different spatial patterns.

The **hotel layer** was also interesting because I could view it by itself.

<p align="center">
  <img
    src="{{ '/assets/images/poland-map-hotels.jpg' | relative_url }}"
    alt="Interactive Poland map showing only the hotel layer"
    width="750">
</p>

*Figure 2. The interactive map with only the Hotels layer selected.*

Looking at hotels by themselves made the pattern easier to see. This layer was especially interesting to me because I had personally visited tourist places such as **Kraków, Gdańsk, and Zakopane**. When I saw hotel points around major cities and tourist areas, I could connect the data to places I had actually experienced.

For example, Kraków and Gdańsk both felt very active and popular with visitors when I was there, while Zakopane had a very different type of tourism connected to the mountains and outdoor activities. Seeing hotel locations on the map made the data feel more real to me because I could connect some of the points to places I remembered visiting.

At the same time, I had to be careful not to assume that more hotel points automatically means more tourism. A larger number of points could also mean that GeoNames has better coverage in that area. This reminded me that the map shows both real geographic patterns and the limits of the dataset.

## Missing Data and Uneven Coverage

Before this assignment, I often thought of data as something that simply records facts. After working with GeoNames and reading Kitchin and Lauriault, I started to think more carefully about that idea.

Some areas may have more information because they were mapped more carefully, while other areas may have missing or older information. An empty area on a map does not always mean that nothing exists there.

Kitchin and Lauriault explain that data should not automatically be seen as completely neutral or as a perfect copy of reality. Data are shaped by the people, organizations, technologies, standards, and decisions involved in producing them. They also explain that databases are part of larger social and technical systems, not just neutral storage spaces.

This idea is important for my Poland map. GeoNames does not simply copy the real world directly into a database. Someone has to decide what counts as a mountain, lake, stream, hotel, or railroad station. Someone also has to enter the name, coordinates, category, and other information.

Because of this, I should not only ask, **"What does the map show?"** I should also ask, **"How was this information created?"**

## GeoNames as a Data Assemblage

Kitchin and Lauriault use the term **data assemblage** to describe a system made from many different parts that work together to create and manage data.

A data assemblage is not only the final dataset. It can include people, computers, databases, organizations, technical standards, methods, and institutions.

I think GeoNames is a good example of a data assemblage.

When I downloaded `PL.txt`, I received a simple text file, but a lot of work happened before that file reached me. Names and coordinates had to be collected, classified, stored, maintained, and made available online.

The [GeoNames data sources page](https://www.geonames.org/datasources/) shows that GeoNames brings together information from different sources. The [GeoNames Team page](https://www.geonames.org/team.html) also shows that GeoNames uses country ambassadors, including one for Poland, to help with national geographic information and data sources.

This helped me understand that the points on my map are the final result of many different systems and decisions working together.

## Building the Interactive Map

The technical part of this project also taught me a lot.

First, I downloaded the Poland GeoNames file and uploaded it to Posit Cloud. I used R to assign the correct names to all 19 columns, counted the feature codes, and filtered the data to my five selected types. I then created custom popup boxes showing the place name, feature code, population, elevation, and time zone.

I separated the five feature types into different interactive layers:

- Lakes
- Mountains
- Railroad Stations
- Streams
- Hotels

This was useful because showing every point at the same time makes the map crowded. By turning layers off, the user can focus on one type of feature at a time.

I also customized the map with readable layer names, a legend, custom popups, and the **Thunderforest Outdoors** basemap. These changes made the map clearer and easier to use.

## Thinking Critically About the Map

An important part of this assignment was not just creating a working map. It was also thinking about what the map means.

My understanding of Poland changed depending on which feature codes I selected. If I had selected only populated places, the map would mainly show settlement patterns. If I had selected only mountains and lakes, I would see Poland mainly through its natural geography.

This means my map is not a complete picture of Poland. It is one possible picture created from five categories that I chose.

The feature codes also simplify real places into categories. A location becomes a point with a code such as `MT`, `LK`, or `HTL`. This is useful for analysis, but it also removes detail.

This connects to Kitchin and Lauriault's idea that data are not completely "raw." Before the data appears on my map, it has already been collected, selected, categorized, organized, and stored.

The map is useful, but it should not be treated as the complete truth about Poland.

My personal experience also affected how I read the map. Because I had already visited Kraków, Gdańsk, and Zakopane, I naturally paid more attention to those areas. This made me realize that the person using the data also brings their own memories and expectations into the analysis. Two people could look at the same map and focus on very different patterns depending on what they already know about Poland.

## Using This Workflow in the Future

I think this workflow could be useful in other courses or projects. I could use it to map historical sites, environmental information, transportation systems, cultural locations, or population data.

It could also be useful for a capstone project or jobs involving GIS, urban planning, tourism, transportation, or data analysis.

Before this assignment, I mainly thought about whether a map looked correct. Now I also think about where the data came from, who created it, what may be missing, and how the categories affect what I see.

## Conclusion

Overall, this project taught me both technical and critical skills.

On the technical side, I learned how to work with a large GeoNames dataset in R, filter data, create custom popups, build multiple Leaflet layers, add a legend, customize a basemap, and export an interactive HTML map.

I also completed the optional bonus work by including more than three clickable layers, using an API-key basemap, and customizing the Leaflet map further.

More importantly, I learned that data should not automatically be treated as a perfect representation of reality. The Poland GeoNames dataset contains a large amount of useful geographic information, but it still depends on where the information came from, how it was collected, how features were classified, and how complete the coverage is.

This project was more interesting to me because Poland was not just a random country I selected from a list. I had already visited **Kraków, Gdańsk, and Zakopane**, so I was able to connect the digital map to places and landscapes I remembered in real life.

Seeing mountain features in the south reminded me of Zakopane, while looking at hotels and city-related features made me think about my experiences in Kraków and Gdańsk. This helped me understand that mapping is not only about points and codes. It can also connect data to real places, memories, and experiences.

At the same time, the project taught me to separate my personal experience from what the dataset can actually prove. My memories helped me ask questions and notice patterns, but the GeoNames data still has to be studied critically.

My map gives one useful view of Poland, but it is not the only possible view. Changing the feature codes would create a different map and could lead to different observations.

This is what made the project interesting to me. I was not only learning how to create an interactive map. I was also learning how to connect data with real places I had experienced, while still questioning the data behind the map and understanding how digital data shapes the way we see places.

## AI use statement

I used ChatGPT to help me navigate around GitHub and understand what files and codes to put aswell as troubleshooting parts of the R and website workflow.

**READY FOR GRADING**
