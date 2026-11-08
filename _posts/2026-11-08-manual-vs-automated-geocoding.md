---
layout: post
title: "Assignment 2: Manual vs. Automated Geocoding"
date: 2026-11-08
---

# Manual vs. Automated Geocoding: Mapping *1 the Road*

**Mohamed Alharbi and Ahmed Al Harbi**

## Introduction

Geocoding is the process of connecting geographic references to locations on a map. Although this might seem straightforward, identifying a place mentioned in a text is not always simple. A name can refer to several different locations, some places are difficult to identify, and others might not appear in geographic databases at all.

In this assignment, we explored the differences between manual and automated geocoding using Ross Goodwin's *1 the Road*. Our objective was to examine how humans and computers identify geographic information and how their decisions affect the resulting maps.

*1 the Road*, published by Jean Boîte Éditions in 2018, is an experimental novel created using artificial intelligence. Goodwin equipped a Cadillac with a camera, microphone, GPS system, and computer capable of generating text during a road trip from New York to New Orleans.

The novel is particularly interesting for digital humanities because its text was generated through interactions between technology and physical environments. Geographic information is therefore an important part of both the writing process and the story itself.

For our analysis, we compared three geographic datasets: manually annotated locations from Recogito, automated geocoding using spaCy and geopy, and a third dataset produced through an LLM-assisted workflow.

By comparing these methods, we wanted to understand whether automated systems could identify places as accurately as human annotators and what kinds of geographic information might be lost or misinterpreted.

## 1. Our Manual Annotation Process

We completed this assignment as a pair, working on Section 5 of *1 the Road*.

We divided our responsibilities between reading and annotation. Mohamed focused on reading and examining the assigned section, while Ahmed was responsible for annotating geographic references using Recogito.

Recogito allows users to highlight geographic references in a text and associate them with locations. This involves identifying place names and searching geographic databases for their corresponding coordinates.

One difficulty we encountered was finding reliable latitude and longitude coordinates for certain locations.

Although we used GeoNames and Google Maps to search for geographic information, some places were difficult to identify. In certain cases, we could not find sufficient information to establish their coordinates confidently.

Following Professor Wrisley's instructions in class, Ahmed left these locations without coordinates rather than selecting an uncertain location.

This was an important part of the manual annotation process. It showed us that identifying a geographic reference does not necessarily mean that its location can be determined accurately.

Manual geocoding involves more than simply recognizing a place name. It also requires interpreting the surrounding text and deciding whether the available geographic information is reliable.

![Manual Recogito map]({{ '/assets/assignment2/manual_recogito.png' | relative_url }})

*Figure 1. Geographic locations from the manually annotated Recogito dataset.*

## 2. Downloading and Preparing the Data

After completing the annotations, we exported the Recogito data into CSV format.

The exported dataset contained place names, annotation information, and geographic coordinates when available.

The dataset used for our analysis also included cleaned coordinate columns. These allowed coordinates recorded in different fields, including comments and tags, to be represented consistently.

The final manual dataset contained 246 annotation records, of which 235 had coordinates and 11 did not.

These numbers describe the combined annotation dataset, rather than only the annotations completed by our pair.

The missing coordinates were particularly interesting because they demonstrated a limitation of geographic identification. Even when a place could be recognized in a text, identifying its exact location was sometimes impossible.

For transparency, we have included our Recogito dataset in our GitHub repository.

[View our Assignment 2 data folder]({{ '/assets/assignment2/' | relative_url }})

## 3. Automated Geocoding

The second part of the assignment involved comparing our manual annotations with automated geographic identification.

We worked with two automated datasets provided for the assignment.

The first used spaCy, a Python natural language processing library, to identify geographic entities. Geopy was then used to obtain coordinates for recognized locations.

The second dataset was produced through an LLM-assisted workflow that combined geographic entity identification with coordinate lookup.

Unlike manual geocoding, these approaches automate parts of the process.

Rather than relying on a person to examine each geographic reference individually, the system identifies likely place names and attempts to associate them with locations.

This can make automated geocoding particularly useful when working with large amounts of text. However, it can also introduce errors, especially when a place name is ambiguous.

Our automated datasets contained 341 and 374 annotation records respectively. Of these, 248 and 281 records had coordinates.

These numbers also include repeated geographic references, meaning they should not be interpreted as counts of unique places.

![Automated spaCy map]({{ '/assets/assignment2/automatic_spacy.png' | relative_url }})

*Figure 2. Geographic locations identified through the automated spaCy geocoding process.*

## 4. Comparing Manual and Automated Geocoding

One of the most interesting discoveries came from comparing how different methods identified the same place names.

For example, our manual dataset associated Florence with coordinates in South Carolina, United States. However, the automated datasets associated Florence with coordinates in Italy.

A similar difference appeared with Augusta. Our manual dataset placed Augusta in Georgia, United States, while the automated datasets returned coordinates in Germany.

Another example was La Grange. The manual annotations placed it in Georgia, United States, while the automated datasets returned a location in France.

These examples demonstrate an important limitation of automated geographic identification.

The automated systems were able to recognize these names as geographic references, but the coordinates they selected did not always agree with the manual annotations.

This does not automatically prove that every manually selected coordinate is correct. However, it demonstrates why geographic context matters.

For example, when reading a text about an American road trip, a human annotator might consider the journey's route and surrounding locations before deciding which Florence is being referenced.

An automated system may instead select a prominent matching location from its geographic database.

Consequently, the geographic information produced by automated systems can appear precise even when the underlying interpretation is uncertain.

Our findings suggest that geographic accuracy depends not only on recognizing a place name but also on selecting the appropriate location.

## 5. Visualizing the Three Datasets

We used the provided R notebook in Posit Cloud to create an interactive Leaflet map.

The map combines the three geographic datasets into separate layers, allowing us to compare their spatial patterns.

One advantage of this visualization is that the layers can be displayed together or individually. This makes it easier to observe differences between the manual and automated approaches.

The map also uses different colors to distinguish the datasets.

Additionally, slight changes to point positions, known as jitter, help prevent overlapping markers from hiding one another.

This is useful because several references may share the same coordinates. Without jitter, multiple records could appear as a single point.

### Interactive Three-Layer Map

<iframe
  src="{{ '/assets/assignment2/interactive_map.html' | relative_url }}"
  width="100%"
  height="600"
  style="border: 1px solid #ccc;"
  title="Interactive map comparing manual and automated geocoding">
</iframe>

*Figure 3. Interactive Leaflet map comparing the three geocoding datasets. The layers can be selected individually to examine differences between methods.*

![Three-layer map]({{ '/assets/assignment2/all_three_layers.png' | relative_url }})

*Figure 4. Screenshot showing the three geographic datasets displayed together.*

The visualization demonstrates how the same text can produce different geographic representations depending on the method used.

Although an automated dataset may contain more identified locations, a larger number of points does not necessarily mean that it is more accurate.

Some points may represent incorrectly matched locations, while others may reflect references that were not confidently identified during manual annotation.

This highlights an important distinction between completeness and accuracy.

## 6. Geographic Data and the Role of Interpretation

Kenric McDowell's introduction to *1 the Road* provides an important perspective on the relationship between technology and geographic information.

McDowell explains that the system received information about nearby businesses and locations through the Foursquare API.

This meant that the text was influenced by the geographic information available through a commercial digital platform.

Locations such as gas stations and fast-food restaurants were particularly prominent in the information available to the system.

This raises an interesting question: Does the text represent the actual geographic environment, or does it represent the environment as recorded by a particular technology?

The distinction matters because geographic databases are not necessarily complete or neutral.

Some places are documented extensively, while others may have limited information or may be absent from commonly used databases.

This can affect both the original AI-generated text and the automated methods used to map it.

For instance, a commercial location with extensive online information might be easier to identify than a small or unfamiliar landmark.

Our experience with Recogito demonstrated this problem on a smaller scale. Some geographic references were difficult to locate even after searching multiple resources.

This suggests that access to geographic information plays an important role in determining which locations appear in digital maps.

## 7. Human Judgment Versus Automation

Our comparison revealed advantages and limitations in both approaches.

Manual geocoding allows annotators to consider the surrounding text and investigate ambiguous locations.

Human annotators can also recognize when there is insufficient evidence to assign coordinates.

However, manual annotation requires time and effort. It also depends on the annotator's interpretation and knowledge.

Automated geocoding, by contrast, can process large amounts of information relatively quickly.

This makes it useful for projects involving extensive textual datasets.

Nevertheless, the examples of Florence, Augusta, and La Grange show that automated systems may associate place names with geographically different locations.

The problem is not necessarily that a computer fails to recognize a geographic reference. Instead, it may recognize the name but select an inappropriate match.

Another important observation is that automation does not eliminate human decisions entirely.

Humans still determine which tools to use, what geographic databases to consult, and how the results should be displayed.

Even map design choices, such as marker colors and jitter, influence how users interpret the results.

[**Drucker reading connection to be added after Professor Wrisley confirms the assigned chapter.**]

## Conclusion

This assignment helped us understand that geocoding involves interpretation as well as technology.

Through our work with Recogito, we experienced the challenges of identifying geographic information manually, particularly when reliable coordinates were unavailable.

Comparing the three datasets also demonstrated how automated systems can produce different geographic interpretations of the same text.

The differences involving Florence, Augusta, and La Grange were particularly useful because they showed how geographic ambiguity can affect automated results.

Ultimately, our findings suggest that manual and automated geocoding should not necessarily be viewed as competing methods.

Automated tools can help researchers process large amounts of information, while human interpretation remains important for evaluating uncertain or ambiguous results.

For digital humanities, the challenge is not simply to produce more geographic data, but to understand how that data was created, interpreted, and represented.

Mapping *1 the Road* showed us that even a seemingly straightforward geographic coordinate can involve several layers of human and technological decision-making.

## References

- Goodwin, Ross. *1 the Road*. Jean Boîte Éditions, 2018.
- McDowell, Kenric. Introduction to *1 the Road*, 2018.
- Wrisley, David. *Assignment 2: Manual Geocoding vs. Automated Geocoding*, DHS Fall 2026.
- spaCy. Natural Language Processing Library.
- GeoNames. Geographic Database.
- OpenStreetMap. Open Geographic Data.
- Drucker, Johanna. [Specific assigned chapter to be confirmed.]
