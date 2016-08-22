---
layout: post
title: 3 Late-Round Quarterbacks to Win 2016 Drafts 
---

This is an update to my [previous post](https://colekev.github.io/opportunity-scores-rookie-wr-2016/) on finding over/undervalued receivers based on the realtionship between signal-callers and their receivers. A higher drafted quarterback, presumably, will throw for more yards and touchdowns than one drafted lower. Receivers are the ones catching the ball and accumulating those yards, touchdowns and fantasy points. By analyzing the relationship between our assessments of a team’s quarterback and receivers, we can see which part of the equation is undervalued versus the other.

Last offseason, we used this relationship to identify that the Colts’ receivers were vastly overvalued based on the [Andrew Luck halo effect](http://rotoviz.com/2015/04/andrew-luck-fantasy-halo-effect/), that you [should likely pass](http://rotoviz.com/2015/04/trestman-effect-joe-flacco-actually-undervalued/) on Joe Flacco, and that Blake Bortles [had breakout potential](http://rotoviz.com/2015/04/four-quarterbackreceiver-adp-arbitrage-opportunities/) with such a strong receiving corps.

For more background on the analysis, you can also see my post from earlier this offseason on [five undervalued quarterbacks](http://rotoviz.com/2016/05/undervalued-quarterbacks-fantasy-2016/?hvid=2JrtbF) using this relationship. 

That was three months ago, and ADPs have changed greatly based upon news and shifts in drafters' perceptions. Here is the updated chart showing the relationship between quarterback and receiver ADPs using the [RotoViz Best Ball ADP App](http://rotoviz.com/best-ball-adp/).

![qb_rec_adp_2016]({{ site.url }}/images/qb_rec_adp_22_08_2016.png)

This graph can be a little difficult to assess, but there are clearly certain teams where the relationship between quarterback and receivers ADPs vary from the norm. 

There are a few adjustments that make this formula work:

1) The receiver value calculation is the inverse of ADP: the last pick in a 20-round, 12-team draft (240) minus ADP. You then add up all the values for wide receivers and tight ends to come up with the combined score.

2) The weighting of tight end ADP on the total receiver value calculation is cut down to one third of that of wide receivers. This gives a negative affect on opportunity for teams with an elite tight end, but recognizes that tight end and wide receiver production are not completely fungible.

3) The receiving stats accumulated by running backs in an offense are accounted for by discounting the receiver value calculation by the percentage of receiving fantasy points to running backs.

4) Quarterback rushing production is also accounted for by discounting the receiver value calculation by the percentage of quarterback fantasy points from rushing, not throwing.

An easier way to digest the information is a bar chart showing the exact distance from the regression line for every team.

![qb_value_adp_2016]({{ site.url }}/images/qb_value_22_08_2016.png)

If you're a late-round quarterback enthusiast, you have a few great choices this year. Robert Griffin III is surrounded by receiving talent (at least in the minds of fantasy footballers), yet is the 28th quarterback of the board in recent MFL10s. When you add in Griffin's rushing ability, he could be a steal in this year's drafts.

Matthews Stafford and Jay Cutler don't stir confidence in the hearts of many, but both have mutiple receiving weapons with farily high ADPs this season. Stafford lost Calvin Johnson, but the prospects for Golden Tate and Marvin Jones to replace that production are viewed as favorable. 

Jay Culter could have a healthy Alshon Jeffery for all of 2016, plus the addition of 2015 top-10 pick Kevin White to the receiving corps. Stafford and Cutler aren't without risks, but their respective ADPs make them huge bargains in comparison to their highly valued receivers.

Always keep in mind that the flip side of these quarterbacks being undervalued is that their receivers could be overvalued. Griffin, Stafford and Culter might not produce the hoped for performances if their respective receivers are being overdrafted on the hope that all will have breakout seasons.

You can find my [R code](https://github.com/colekev/Opportunity-Scores-for-Rookie-WRs/blob/master/OS_2016.R) for calculating these scores at my [GitHub repo](https://github.com/colekev/Opportunity-Scores-for-Rookie-WRs).
