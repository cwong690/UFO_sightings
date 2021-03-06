# NLP Unsupervised Learning Case Study

![badge](https://img.shields.io/badge/last%20modified-may%20%202020-success)
![badge](https://img.shields.io/badge/status-in%20progress-yellow)

<a href="https://github.com/cwong690">Cindy Wong</a> | <a href="https://github.com/oro13">Feli Gentle</a> | <a href="https://github.com/mkpetterson">Maureen Petterson</a>

## Table of Contents

- <a href="https://github.com/mkpetterson/UFO_sightings#Introduction">Introduction</a> 
- <a href="https://github.com/mkpetterson/UFO_sightings#data-preparation-exploratory-data-analysis">Exploratory Data Analysis and Data Preparation</a> 

- <a href="https://github.com/mkpetterson/UFO_sightings#natural-language-processing">Natural Language Processing</a> 
- <a href="https://github.com/mkpetterson/UFO_sightings#summary-and-key-findings">Summary and Key Findings</a>


## Introduction

UFO sightings occur with relative frequency all across the United States. The sighted UFOs have various shapes and the sightings last for varying amounts of time. Using the UFO sighting database, we evaluated several characteristics of the sightings and used Natural Language Processing (NLP) to analyze the descriptions and see what commonalities all the descriptions had. 

The data was pulled from the [The National UFO Reporting Center Online Database](http://www.nuforc.org/webreports.html).  


## Data Preparation and Exploratory Data Analysis

### Data Preparation

The raw data was 2.5GB and required a decent amount of preparation prior to analysis. We downloaded a zipped json file that included the raw HTML for each individual sighting.

Cleaning and preparation methods included:

- Extracting the unique observation ID, date, time, location, shape and text description of the sightings
    - First we used Beautiful Soup's html parser to extract data contained within specific HTML tags
    - Limited data to about 15,000 in order for it to not run forever
    - Regular expressions were utilized to extract the exact terms we needed to run analyis on the different features
- Separating the text description from the follow-up notes
- Putting the information into a pandas datafram for easier analysis

<details>
    <summary>Raw JSON data</summary>
    <img alt="Data" src='images/json_data.png'>
</details>
    
<details>
    <summary>Raw Extracted Sample Report</summary>
    <img alt="Data" src='images/sample_report.png'>
</details>    
    
<br>    
    
The cleaned up pandas dataframe is shown below
    
  <img src='images/initial_df.png'>


### Exploratory Data Analysis

The sightings described the UFOs as various different shapes, including circles, chevrons, lights, or fireballs. The duration of the sightings lasted from a few seconds to many minutes. 


**Shapes and Duration**
<img alt="shapes" src='images/shape_duration.png' style='width: 600px;'>


The time of day for the observations were also interesting. Sightings tended to be higher in the early morning or evening hours, which makes sense as UFO lights will not be as visible during daylight hours. It's also possible many people mistake planets, satellites, or planes as UFOs.  

<img alt="timeofday" src='images/time_of_day.png'>

**State**

We got a count of the states and sightings. It seems California is number one for UFO sightings.

<img alt="state_count" src='images/state_counts.png'>


## Natural Language Processing
The data was analyzed using a combination of nltk packages and sklearns CountVectorizer/TFIDFVectorizer to analysis the most common words within the observations. We also used topic modeling to extract latent features of the text. The pipeline used on each observation was:

### Baseline Model using SkLearn

Fitting the Model:
<img alt="vanilla topics" src='images/vanilla_model.png'>

Top 10 Topics:
<img alt="vanilla topics" src='images/vanilla_topics.png'>

Custom Language Processing with NLTK

1. Tokenization of text observations, Stop Words removal (standard English)

<img alt="cleaning words" src='images/cleaning.png'>

3. Lemmitization using nltk WordNetLemmatizer

<img alt="lemmatizing" src='images/lemma.png'>

4. TFIDFVectorizer to get the relative word strength

<img alt="Vectorizing with additional features" src='images/vectorize2.png'>

5. Topic Modeling using Non-negative Matrix Factorization (NMF)

<img alt='fitting model 2' src='images/cluster2.png'>

Using this pipeline allowed us to visualize the most common words for the observations. 

<b>UFO Sightings</b>
<img alt="ufowords" src='images/UFO_words.png'>

<b>Notes on the UFO Sightings</b>
<img alt="ufonoteswords" src='images/UFO_notes_words.png'>

<b>Bigfoot Sightings</b>
<img alt="bigfootwords" src='images/bigfoot_words.png'>

## Summary and Key Findings


<img alt="Data" src='images/ufo.jpeg'>
