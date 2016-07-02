
This past week I began a more intense journey as part of the [Metis Data Science](http://www.thisismetis.com/data-science) summer cohort, culminating in our first project: **How can we use various data sources to find the ideal subway stations to promote the annual summer gala for WomenTechWomenYes (WTWY), a fictional non-profit focused on increasing the participation of women in technology?**

## Goals

WTWY, like many non-profit organizations, funds itself through the generousity of others who share its mission. Therefore, the focus of any effort to find the right people to attend its gala, be its advocate, and contribute to the cause must incorporate data from disparate sources to find the right demographic.

## Assumptions

We made a couple assumptions about the timing of the gala and WTWY's capacity to support the marketing teams:
1. The gala date will be in August 2016.
2. WTWY has a limited budget that can only support 2-7 promotional street teams at any given time.

## Our Approach

The [MTA turnstile data source](http://web.mta.info/developers/turnstile.html) was specifically mentioned by WTWY, and any analysis to maximize promotion efforts at subway stations should focus on rider traffic. But we also had to consider the demographics of those riders.

Our approach focused on finding th subway stations located at the nexus of three factors:

1. **Neighborhoods with tech employers and tech student/professors**. To find subway riders with the highest likelihood of being supportive of a tech-related cause, we decided to filter for neighborhoods with strong tech employment or major universities with computer science programs. We found data on the location employers in the technology industry in New York State Comptroller Thomas P. DiNapoli's report on [New York City’s Growing High-Tech Industry](https://www.osc.state.ny.us/osdc/rpt2-2015.pdf).
2. **Higher income neighborhoods**. While the wealthiest Americans [don't give a higher percentage of their incomes](https://philanthropy.com/article/As-Wealthy-Give-Smaller-Share/152481) to charitable causes, the simple fact that they have more income to give makes them a preferred target of any fundraising effort. We used data from the [American Community Survey 2006-2010](https://www.census.gov/programs-surveys/acs/data.html) to find New York City zip codes with median incomes greater than $70,000, then found how many of these wealthier zip code where located near each subway station.
3. **Subway stations with the highest foot traffic**. We used the tech employer and wealth data to filter our list of 384 subway stations down to the 31 with a preseance of either, then we used the July 2015 [MTA turnstile data](http://web.mta.info/developers/turnstile.html) as a proxy for the traffic patterns you could expect this July, the ideal time period for promoting the August gala.

## Cleaning the Data

Once we had all the turnstile data for July 2015 loaded into Python, there was still quite a bit of cleaning and calculation needed to provide meaningful numbers on which to base our analysis. 

1. The turnsile data only provided the cumulative number of entries and exits, not the net amount for any particular time period. We used a [Python loop](http://www.tutorialspoint.com/python/python_loops.htm) function to go through the data and calculate the net entries and exits for each period, then created a new column for total traffic (entries plus exits).
2. The MTA collected most of its turnstile data at regular, four-hour intervals of midnight, 4am, 8am, etc. However, there were many instances where the data was an hour off of the regular schedule, and some observation times were seemingly random. To help with our time analysis, we rounded all time periods to the nearest hour, and eliminated the small proportion of data that far removed from the regular schedule.
3. The "STATION" names in the data set often included what were actually multiple stations, e.g. "86 ST" included the distinct staions for the 1, 456, BC, N and R trains. We decided to group all of our data by not only station, but also "LINENAME".

![subwayData]({{ site.url }}/images/subway_data_july_2015.png)

After cleaning the data, we were able to further narrow our station

