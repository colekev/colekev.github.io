---
layout: post
title: Turnstiles, Techies & Teachers: A Data-Based Plan for Successful Promotion
excerpt: How do you combine MTA data with other sources to find 
---

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

**Maximize attendance**

The MTA turnstile data we used is [notoriously difficult](http://chriswhong.com/open-data/visualizing-the-mtas-turnstile-data/) to parse. The data is presented in the form of cumulative counts for entries and exits by turnstile by 4-hour period. Here's a sample entry from the data file: 

`R143,R032,02-00-00,TIMES SQ-42 ST,1237ACENQRS,IRT,01/02/2016,03:00:00,REGULAR,0000754332,0001334774`

What we're really interested in here is the station name (`TIMES SQ-42 ST`), date (`01/02/2016`), entries (the second to last number, `0000754332` here), and the exits (last number or `0001334774`). To find the stations with the most traffic, we calculated the total entries/exits per turnstile per day from the cumulative values and then aggregated these numbers to arrive at total entries/exits per station for the full period.  

And the top stations are...

![top 25 stations chart]({{ site.url }}/assets/top25.png)

The top four stations here made sense--they're all big transfer hubs. But we noticed a few odd top runners such as 86th St and 125th St, which are all more residential areas. Turns out there are a handful of MTA stations that share the same name, but are in totally different areas! We wound up dropping these values, since they were unlikely to be top runners on their own. There are also some stations sharing the same name that are technically separate (such as the Chambers St - 2/3 and Chambers St - A/C) but very close in geography--we decided to keep these values and consider them as one station. 

**Maximize quality**

To determine the likelihood of philanthropic contributions by area, we cross-walked data on median charitable contributions per person to station traffic, using zip code as the common factor, and sized the total potential contribution to compare stations. 

As you can see below, Wall St comes out as a clear front runner with nearly $500 billion in total potential contributions (the median per person contribution to charity in 2012 was almost $95,000!), followed, by Grand Central, Port Authority, Times Square, Chambers St, and Columbus Circle. 

![top contributions chart]({{ site.url }}/assets/top10.png)

We also took a look at some gender ratio by zip code data, but it wasn't very robust or well-documented (a common problem with NYC Open Data...). As a high-level consideration, gender is interesting since the organization is women-focused, but likely has less practical impact when you're on the ground (i.e. if traffic is high enough, the street team could just choose to target women and the actual pre-existing women/men ratio would not matter).

**Optimize recommendations**

Once we had our top six stations, we dug into day by day and time of day traffic patterns to determine the optimal times to deploy street teams. All of our stations had a consistent pattern, so let's look at our front runner, Wall St, as an example. 

![wall st day of week chart]({{ site.url }}/assets/wall-st-days.png)

Not surprisingly, weekdays, specifically Monday through Thursday, have the greatest traffic (all of that summer Friday travel!). The Monday dip you see in the week ending May 30 (green line) is Memorial Day. 

Next, we looked at traffic by time of day in four hour blocks. 

![wall st time of day chart]({{ site.url }}/assets/wall-st-time.png)

As expected, the times of day with the highest traffic are the 8AM - 12PM and 4PM - 8PM windows, both of which capture rush hour. 

## Recommendations and next steps

Based on the data considered and analysis so far, we'd recommend deploying street teams between Monday and Thursday (except Memorial Day!) between 8AM - 12PM and 4PM - 8PM to obtain the greatest number of event signups with the highest potential for quality attendees. 

Of course, these recommendations should be taken with a grain of salt--given the iterative process of data science and the short time frame (one week!) for this exercise, the analysis and findings are definitely the first iteration of findings. With more time, there are a number of additional points I'd love to dig my teeth into: 

**Optimizing station selection** 

  * **Residence vs. station usage:** The philanthropic contribution data we used was based on tax returns, so zip codes are indexed to where people live, not necessarily where they work. Given that our top stations are primarily in office hubs and also that our time of day recommendations are during rush hour, we're likely to capture workers in the area (for whom we cannot estimate philanthropic inclinations). To refine our model, I'd love to find some additional data that describes the relationship between where people live and their commuting patterns (perhaps [Journey to Work](http://www.census.gov/hhes/commuting/) data from the Census?). 

  * **Other demographic/sectoral data:** The particular focus of a non-profit organization will likely define its supporters. Given that our non-profit was a tech organization, I would have loved to have considered areas with high concentrations of tech companies and affilitated orgs. The easiest way to do this would probably be to use [NAICS codes](http://www.census.gov/eos/www/naics/) and [Bureau of Labor Statistics](http://www.bls.gov/) data, but finding the right level and type of classification for tech companies is difficult, since codes are based on industry (i.e. the type of product) as opposed to the type of company. 

    For example, Uber would probably be classified under code `48-49 - Transit and Ground Passenger Transporation` instead of what most of us would assume tech comapnies are under, either `51 - Information` or `54 - Professional, Scientific, and Technical Services`. There are ways to dig in deeper down to the six-digit code level, but these problems continue to persist. This is actually an issue that my old firm, HR&A Advisors, tackled in our study of the [NYC tech ecosystem](http://www.hraadvisors.com/nyctechstudy/)--we hand-picked a set of NAICS codes to try and capture the tech industry. The best strategy here might just to be to pull the old domain knowledge card--Flatiron, the Meatpacking District, DUMBO, and Long Island City are probably good bets for tech. 

    There are also many other factors I'd like to consider outside of industry: what about race and age? What about general foot traffic (e.g. areas with a lot of pedestrian activity, such as Broadway in SoHo)? 

**User interface** 

One of the reasons I decided to leave economic development/policy consulting and transition into tech was the desire to do something more with data than just produce charts and powerpoints. I'd love to build a tool here that empowers the client to use the data for their needs in the future, since the availability of their street team resources will likely fluctate. Perhaps a dashboard where the input would be street team capacity and the time/day availability, and the output would be a recommendation of the top three areas to deploy and/or a route for the time frame? 

## Code and presentation

The top stations analysis scripts are available at [my GitHub repo](https://github.com/dianalam/streetteam-mta-analysis) and our findings presentation can be viewed [here](https://github.com/dianalam/streetteam-mta-analysis/blob/master/presentation/mta-turnstile-pres.pdf).










