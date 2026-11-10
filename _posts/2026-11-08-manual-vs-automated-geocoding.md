---
layout: post
title: "Assignment 2: Manual vs. Automated Geocoding"
date: 2026-11-08
---

# Manual vs. Automated Geocoding: Mapping *1 the Road*

**Mohamed Alharbi and Ahmed Al Harbi**

## Introduction

Geocoding connects references in a text to locations on a map. The challenge is that a place name can refer to several locations, and some of the places described in a text may be hard to find in a geographic database. We explored these problems using Ross Goodwin’s *1 the Road*, an experimental novel published by Jean Boîte Éditions in 2018. Goodwin equipped a Cadillac with a camera, microphone, GPS system, and computer that generated text during a road trip from New York to New Orleans. Geography shaped the writing process because information gathered along the route helped determine what appeared in the book.

We compared three datasets produced from the text: manual annotations from Recogito, an automated dataset generated with spaCy and geopy, and an LLM-assisted dataset. Mapping these datasets side by side let us ask which references each method captured, where the methods agreed, and what happened when the same name was assigned to different locations. The results show how decisions about context and evidence affect the geography readers see on the map.

## 1. Our Manual Annotation Process

We worked as a pair on Section 5 of *1 the Road*. Mohamed read and examined the assigned section, and Ahmed marked geographic references in Recogito. We used the surrounding text to decide whether a phrase referred to a place, then searched GeoNames and Google Maps for coordinates. The Recogito text came from optical character recognition (OCR), which can split words or misread letters. This added another layer of uncertainty because an odd spelling could reflect a problem in the digital transcription or a name that was genuinely difficult to identify.

Finding a reference and locating it were two separate decisions. Sometimes the passage made it clear that a location was being mentioned, but the information available in the text and in our searches was too limited to identify a reliable match. Following Professor Wrisley’s instructions, we left the coordinates blank in those cases. This kept the reference in the dataset while recording the uncertainty about where it belonged.

## 2. Downloading and Preparing the Data

After annotating the text, we exported the Recogito data as a CSV on 8 November 2026. The export contained place names, annotation information, and coordinates where available. We used cleaned latitude and longitude columns to bring together coordinates that had been recorded in different fields, including comments and tags. The combined class dataset contained 246 annotation records, of which 235 had coordinates and 11 did not. These totals describe the class dataset, which includes our work on Section 5. The [Recogito CSV]({{ '/assets/assignment2/recogito.csv' | relative_url }}) is available in our GitHub repository.

Figure 1 shows the points that could be plotted from the cleaned class annotations. Two gaps stand out, one between Virginia and North Carolina and another between Georgia and Mississippi. A blank stretch of the map and a record with missing coordinates tell us different things. The eleven blank coordinate records document places that were annotated but could not be plotted. A gap on the map could also reflect what the novel mentions or how much of the text the class was able to annotate in the available time. The map alone gives us no way to assign either gap to a particular cause.

<p align="center">
  <img src="{{ '/assets/assignment2/manual_recogito.png' | relative_url }}" alt="Map of the combined Recogito annotations" width="75%">
</p>

*Figure 1. Screenshot of the interactive map showing the cleaned, combined Recogito annotations.*

The distinction matters when interpreting the route. A map marker is evidence of an annotation with coordinates. A record without coordinates can still tell us which reference was difficult to resolve. Looking at the CSV alongside the map helps us separate what was recorded from what can be displayed on the map for readers to compare.

## 3. Automated Geocoding

Professor Wrisley provided the two automated datasets. In the first workflow, spaCy identified likely place names and geopy was used to look up coordinates. The second used an LLM-assisted transcription and tagging workflow that also used spaCy and geopy. Both workflows automate the identification and lookup stages, which makes it possible to process many references quickly. An error can still enter at either stage. A system can interpret a string as a place even when it has another function in the text, or it can recognize a real place name and select coordinates for the wrong location.

The two automated datasets contained 341 and 374 annotation records. These counts include repeated references, so they measure recorded mentions rather than the number of unique places. Figure 2 compares the two automated layers at a world scale. The layers broadly agree along parts of the U.S. route, but both also show points overseas. For a text generated during a U.S. road trip, a cluster of overseas points is a reason to inspect individual matches and check how each place is used in the text. A world view makes those matches visible. A close view of the route helps us see where two matches land near each other, as Wrisley demonstrated with the points labeled St. Paul’s.

<!-- Upload automatic_comparison.png to assets/assignment2. Use a world view with both automated layers on, the manual layer off, and the legend visible. -->

<p align="center">
  <img src="{{ '/assets/assignment2/automatic_comparison.png' | relative_url }}" alt="World map comparing both automated geocoding methods" width="85%">
</p>

*Figure 2. World-view screenshot comparing the spaCy + geopy and LLM-assisted datasets.*

## 4. Comparing Manual and Automated Geocoding

Florence illustrates how the same place name can lead to different coordinates. The manual dataset placed Florence in South Carolina, while the automated results included a match in Italy. Wrisley demonstrated the ambiguity by searching GeoNames for *Florence*. The search returned several possible locations, and Florence, Italy appeared above Florence, South Carolina. This gives one possible explanation for the mismatch. When the lookup uses only the name, the order of the candidates can determine which place is returned. The surrounding passage and the road trip’s route give a reader additional clues for choosing among those candidates. A result can therefore look convincing in the dataset because it has a valid name and coordinates even when it points to the wrong Florence.

The comparison also helps us examine the manual layer more critically. Several manual points sit apart from the apparent route in the southeastern United States. A point off the route could be an annotation error, or it could be a place that the text mentions without the car passing through it. To distinguish those cases, we would need to open the point, find the reference in the text, and compare the passage with the assigned coordinates. This is the same kind of contextual check that makes the Florence example useful.

Agreement across layers can help us decide which references to investigate first. If two methods place a name far apart, the difference gives us a specific passage to revisit. If they agree, that gives us a candidate location to check. Since both automated workflows used some of the same tools, their agreement can also reflect a shared lookup choice.

## 5. Visualizing the Three Datasets

We used the R notebook to create the interactive Leaflet map in Figure 3. The map gives each dataset its own layer and color. Use the checkboxes in the upper-right legend to turn the layers on or off. Start by comparing the two automated layers at a wide zoom to see the overseas matches. Then zoom in on the southeastern United States and turn on the Recogito layer to compare the manual points with the automated ones. The two zoom levels help answer different questions. The world view shows how far a match can fall from the route, while the closer view shows how closely the methods agree in the region the car traveled through.

The notebook also uses jitter, which slightly shifts plotted markers so that overlapping points are easier to see. This helps when several records would otherwise appear as one dot. Small differences in marker positions should therefore be interpreted with care, especially at close zoom. The underlying records are the better place to check whether two methods actually assigned different coordinates.

<iframe
  src="{{ '/assets/assignment2/interactive_map.html' | relative_url }}"
  title="Interactive map comparing the three geocoding methods"
  style="width: 100%; height: 600px; border: 0;">
</iframe>

*Figure 3. Interactive Leaflet map comparing the manual, spaCy + geopy, and LLM-assisted layers.*

## 6. Geographic Data and the Role of Interpretation

In the introduction to *1 the Road*, McDowell explains that the Foursquare API exposed nearby businesses and places to the system generating the text. Examples include gas stations, fast-food restaurants, and the Biloxi Hard Rock Cafe (p. 28). The commercial platform shaped which parts of the landscape were available to the system, and those choices affected which places could later appear in our annotations. A business with a listing was easier for the system to encounter than a nearby place with little or no presence in the platform. Our maps therefore reflect several stages of selection, beginning with the geographic information available to Goodwin’s system and continuing with the way we interpreted the resulting text.

## 7. Human Judgment Versus Automation

Human judgment enters throughout the process. Annotators decide when a reference is specific enough to map. The people who build an automated workflow choose the tools, the databases, and how to handle ambiguous matches. Mapmakers also choose the basemap, colors, and amount of jitter. A satellite basemap can emphasize the landscape, while a street map can make named roads and settlements easier to follow. These design decisions affect which patterns readers notice when they compare the datasets.

## Conclusion

Comparing the three layers showed how easily coverage and accuracy can be confused. The automated datasets contain more annotation records, but the Florence example shows that a successful coordinate lookup can still produce a misleading point. The manual dataset preserves some uncertainty through blank coordinates, and its gaps and isolated points also require interpretation. Bringing the layers together makes those differences visible and gives us a way to return to the text and ask what evidence supports each match.

**READY FOR GRADING**
