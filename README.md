# Coronavirus Twitter Analysis

In this assignment I was tasked with scanning all geotagged tweets sent in 2020. Geotagged tweets are just tweets with a defined location. The goal was to analyze these tweets to monitor the spread of coronavirus on social media.

## The Data
The lambda server has the data set `/data/Twitter dataset` folder which contains all geotagged tweets that were sent in 2020.

The data set is a large data set with around 1.1 billion tweets. The tweets are stored by each day in a zip file `geoTwitterYY-MM-DD.zip` and within the zip file there are 24 text files for each hour of the day. Each text file contains a single tweet per line in JSON format.

I utilized vim to open the compression zip files to get a better sense of the formatting. For example, I ran this command to view the second day of the year:
```
$ vim /data/Twitter\ dataset/geoTwitter20-01-02.zip
```

## Programming Summary

**MapReduce**

I used a [MapReduce](https://en.wikipedia.org/wiki/MapReduce) procedure to examine and analyze this large data set. The `map.py` script processes through each zip file, searching for various coronavirus-related tweets. It counts the occurrences of these tweets, categorizing them by country and language. Then, the results were saved in two reduced files related to either language or country.

**Visualize.py**

I then visualized my data using the matplotlib library to create bar graphs looking at frequency of specific hashtags by either language or country. These graphs output the top 10 values for both hashtags I looked at. To obtain my graphs I ran the following command (replacing necessary files or hashtags):

```
$ python3 visualize.py --input_path=reduced.country --key=#coronavirus
```
This gave me:

<img src=country%5F%23coronavirus.png />

Now by language:

<img src=lang%5F%23coronavirus.png />

I also looked at a second hashtag #코로나바이러스. First by country:

<img src=country%5F%23코로나바이러스.png />

And, by language:

<img src=lang%5F%23코로나바이러스.png />


**alternative_reduce.py**

Finally, I created a script that took the input of various hashtags and output:

1) There is one line per input hashtag.
2) The x-axis is the day of the year.
3) The y-axis is the number of tweets that use that hashtag during the year.

During this I called necessary matplotlib functions to plot these line graphs. This function was helpful in analyzing the changing trends in the language used during the pandemic on social media.

I plotted four differe hashtags. I wanted to look at the change of the name used to refer to the virus, so I plotted #coronavirus and #covid19. I also plotted #doctor and #hospital to see how these words matched up with the overall name of the virus.

My findings: 

<img src=2020%5Fhashtag%5Fgraph.png />

This graph was particularly intersting because we can see how coronavirus was initially the common word used to refer to the virus, with the large spike right around the start of quarentine. Then, over time, covid19 became a more popular name especially into the end of the year. In comparison, words like doctor and hospital were rarely mentioned in relation to coronavirus and covid19.
