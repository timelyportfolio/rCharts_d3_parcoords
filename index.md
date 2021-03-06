---
title       : GARCH and MA Outperformance using rCharts & d3 Parallel Coordinates
subtitle    : Applied to French Industry Data Set
author      : TimelyPortfolio
framework   : minimal       # {io2012, html5slides, shower, dzslides, ...}
github: {user: timelyportfolio, repo: rCharts_d3_parcoords, branch: "gh-pages"}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [parcoords]      # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
assets:
  css: 
    - "http://fonts.googleapis.com/css?family=Open+Sans"
    - "http://fonts.googleapis.com/css?family=Open+Sans+Condensed:700"
---


---
# GARCH and MA Outperformance
## Now Using d3 Parallel Coordinates with rCharts

Parallel coordinates become much more useful when they are interactive, so I will recreate one of my favorite blog posts ["Trend is Not Your Friend" Applied to 48 Industries](http://timelyportfolio.blogspot.com/2012/08/trend-is-not-your-friend-applied-to-48.html) and convert the chart to a living breathing d3 parallel coordinates chart courtesy of [Ramnath Vaidyanathan's rCharts](http://ramnathv.github.io/rCharts/) and [Kai Chang's d3.parcoords](http://syntagmatic.github.io/parallel-coordinates/). I will convert the scatter and horizon plots in a later post.  Note see 

<!--old post; left in html to demonstrate combination-->
# "Trend is Not Your Friend" Applied to 48 Industries
<p><em><font size="1">Please see previous post <a href="http://timelyportfolio.blogspot.com/2012/06/crazy-rut-in-academic-context.html">Crazy RUT in Academic Context Why Trend is Not Your Friend</a>.</font></em></p>
  <p>I'll repeat the intro to the post mentioned above, so we can all get caught back up.</p>
  <p>In response to <a href="http://timelyportfolio.blogspot.com/2012/06/where-are-fat-tails.html">Where are the Fat Tails?</a>, reader vonjd very helpfully referred me to this paper <a href="http://www.frankfurt-school.de/clicnetclm/fileDownload.do?goid=000000311260AB4" target="_blank">The Trend is Not Your Friend! Why Empirical Timing Success is Determined by the Underlying's Price Characteristics and Market Efficiency is Irrelevant</a> by Peter Scholz and Ursula Walther. The authors conclude</p>
  <blockquote>
  <p>"Our study on the basis of real data clearly confirms the hypothesis that the asset price characteristics of the underlying price process have a crucial impact on timing results. This allows us to forecast the timing success depending on the market's parameters. An OLS regression analysis supports our predictions and verifies our assumption that the drift has the<br>strongest influence on timing success. By contrast, the higher moments (skewness, kurtosis) seem not to have any significant impact on the timing result in the empirical sample. As we presumed, the level of market development, and hence the degree of efficiency, does not play any role. Trading worked coincidentally rather well in the developed world and quite poorly in the emerging markets. The driving factor for the timing success is the parametric environment the trading system stumbles on.</p>
<p>Our study contributes to the discussion by providing a structured analysis of the relevance of the most important price process parameters. As a result, the traditional explanations for timing success can be abandoned: we find that it is very likely for the SMA trading rule to generate excess returns over its benchmark if the underlying price path exhibits negative drifts, high serial autocorrelation, low volatilities of returns, and highly clustered volatilities. Drift and autocorrelation of the underlying asset seem to have the largest impact, though."</p></blockquote>
<p>One of my initial ideas for extending the research was to incorporate a much larger set of indexes over a longer period of time.&nbsp; As I was working on <a href="http://timelyportfolio.blogspot.com/2012/08/48-industries-since-1963.html">48 Industries Since 1963</a>, I decided 50 years of data on 48 different indexes would be a great dataset to apply the ideas and methods presented in the paper.</p>
<p>Using R and all its wonderful packages, it is surprisingly easy to accomplish.&nbsp; Let's see if we can test "drift and autocorrelation.have the largest impact" on excess returns with industries also.&nbsp; I'll try not to get too statistical.</p>
<p>In terms of drift or annualized return, we can see a linear inverse relationship between return and out(under)performance of the 200 day moving average system, so the better the performance of the industry, the less likely a moving average system is to outperform.</p>
<table style="width: auto">
<tbody>
<tr>
<td><a href="https://picasaweb.google.com/lh/photo/DYGUjcUGkmrHlaVDDQCZj9MTjNZETYmyPJy0liipFm0?feat=embedwebsite"><img src="https://lh3.googleusercontent.com/-9blyMbBqm0I/UCKl39NZYhI/AAAAAAACrPw/vZiS_PZc2dA/s800/Rplot.png" width="640" height="500"></a></td></tr>
<tr>
<td style="text-align: right; font-family: arial,sans-serif; font-size: 11px">From <a href="https://picasaweb.google.com/115099029813395778077/TimelyPortfolio02?authuser=0&amp;feat=embedwebsite">TimelyPortfolio</a></td></tr></tbody></table>
<p>In terms of the GARCH model effects on excess returns, a parallel coordinate chart will best start our exploration.&nbsp; Lines are colored by the excess return of a moving average system on each industry.</p>

<h3>d3 Parallel Coordinates (go ahead and play with it)</h3><div style="height:600px">
<div id='chart' class='rChart nvd3Plot parcoords'></div>
<script id="brushing">
var params = {
 "dom": "chart",
"width":    800,
"height": "600",
"padding": {
 "top":     24,
"left":    100,
"bottom":     12,
"right":    200 
},
"data": [
 {
 "industry": "Gold",
"mu": 0.00051723,
"ar1": -0.066903,
"ma1": 0.11785,
"omega": 3.453e-06,
"alpha1": 0.049596,
"beta1": 0.94495,
"PerfDiff": -0.059927 
},
{
 "industry": "Coal",
"mu": 0.0005384,
"ar1": -0.06297,
"ma1": 0.14288,
"omega": 1.7469e-06,
"alpha1": 0.050263,
"beta1": 0.94688,
"PerfDiff": -0.034628 
},
{
 "industry": "Soda",
"mu": 0.00080222,
"ar1": -0.2382,
"ma1": 0.28996,
"omega": 2.1252e-06,
"alpha1": 0.059029,
"beta1": 0.93302,
"PerfDiff": -0.042998 
},
{
 "industry": "Smoke",
"mu": 0.00080997,
"ar1": -0.050889,
"ma1": 0.13298,
"omega": 1.7361e-06,
"alpha1": 0.049855,
"beta1": 0.94256,
"PerfDiff": -0.049229 
},
{
 "industry": "Fun",
"mu": 0.00096938,
"ar1": -0.16513,
"ma1": 0.2673,
"omega": 2.9771e-06,
"alpha1": 0.080934,
"beta1": 0.9095,
"PerfDiff": -0.011502 
},
{
 "industry": "Comps",
"mu": 0.00064905,
"ar1": -0.38513,
"ma1": 0.4266,
"omega": 2.7603e-06,
"alpha1": 0.069932,
"beta1": 0.92024,
"PerfDiff": -0.0097761 
},
{
 "industry": "Chips",
"mu": 0.00071427,
"ar1": -0.020925,
"ma1": 0.15026,
"omega": 1.7868e-06,
"alpha1": 0.065012,
"beta1": 0.92725,
"PerfDiff": 0.0040667 
},
{
 "industry": "LabEq",
"mu": 0.00069595,
"ar1": 0.0073988,
"ma1": 0.12948,
"omega": 1.5918e-06,
"alpha1": 0.071271,
"beta1": 0.92204,
"PerfDiff": 0.0057089 
},
{
 "industry": "Mach",
"mu": 0.00069674,
"ar1": 0.092925,
"ma1": 0.095038,
"omega": 1.5872e-06,
"alpha1": 0.087746,
"beta1": 0.90299,
"PerfDiff": -0.019804 
},
{
 "industry": "BusSv",
"mu": 0.00072134,
"ar1": 0.14294,
"ma1": 0.03119,
"omega": 2.2322e-06,
"alpha1": 0.093144,
"beta1": 0.8935,
"PerfDiff": 0.0092167 
},
{
 "industry": "Agric",
"mu": 0.00065552,
"ar1": -0.055045,
"ma1": 0.12979,
"omega": 2.249e-06,
"alpha1": 0.053208,
"beta1": 0.93491,
"PerfDiff": -0.042768 
},
{
 "industry": "Oil",
"mu": 0.0006369,
"ar1": -0.11267,
"ma1": 0.2285,
"omega": 1.0987e-06,
"alpha1": 0.062543,
"beta1": 0.9321,
"PerfDiff": -0.031646 
},
{
 "industry": "Steel",
"mu": 0.00051605,
"ar1": 0.17463,
"ma1": 0.010466,
"omega": 2.459e-06,
"alpha1": 0.098097,
"beta1": 0.89274,
"PerfDiff": 0.0056015 
},
{
 "industry": "Mines",
"mu": 0.00057527,
"ar1": 0.20137,
"ma1": -0.059233,
"omega": 1.0872e-06,
"alpha1": 0.068662,
"beta1": 0.92782,
"PerfDiff": -0.016345 
},
{
 "industry": "FabPr",
"mu": 0.00057019,
"ar1": 0.20344,
"ma1": -0.089662,
"omega": 1.3837e-06,
"alpha1": 0.063448,
"beta1": 0.93181,
"PerfDiff": -0.01305 
},
{
 "industry": "RlEst",
"mu": 0.00050816,
"ar1": 0.60107,
"ma1": -0.49852,
"omega": 1.5931e-06,
"alpha1": 0.090047,
"beta1": 0.90349,
"PerfDiff": 0.072937 
},
{
 "industry": "Cnstr",
"mu": 0.00061497,
"ar1": 0.11484,
"ma1": 0.036917,
"omega": 2.4302e-06,
"alpha1": 0.080454,
"beta1": 0.90965,
"PerfDiff": 0.014257 
},
{
 "industry": "Txtls",
"mu": 0.00060474,
"ar1": 0.36387,
"ma1": -0.20407,
"omega": 2.0682e-06,
"alpha1": 0.10623,
"beta1": 0.88414,
"PerfDiff": 0.01296 
},
{
 "industry": "Autos",
"mu": 0.0006076,
"ar1": 0.051829,
"ma1": 0.03423,
"omega": 2.2425e-06,
"alpha1": 0.068008,
"beta1": 0.92177,
"PerfDiff": 0.015763 
},
{
 "industry": "Banks",
"mu": 0.00069627,
"ar1": 0.22728,
"ma1": -0.042497,
"omega": 1.4634e-06,
"alpha1": 0.092584,
"beta1": 0.89977,
"PerfDiff": 0.0015836 
},
{
 "industry": "Fin",
"mu": 0.00076966,
"ar1": 0.24119,
"ma1": -0.055791,
"omega": 7.8789e-07,
"alpha1": 0.079339,
"beta1": 0.91752,
"PerfDiff": 0.013268 
},
{
 "industry": "Ships",
"mu": 0.00068131,
"ar1": 0.23604,
"ma1": -0.15731,
"omega": 3.2745e-06,
"alpha1": 0.071621,
"beta1": 0.91561,
"PerfDiff": -0.018317 
},
{
 "industry": "Guns",
"mu": 0.0007699,
"ar1": 0.28278,
"ma1": -0.25595,
"omega": 2.6928e-06,
"alpha1": 0.063811,
"beta1": 0.92402,
"PerfDiff": -0.019821 
},
{
 "industry": "Hlth",
"mu": 0.00083388,
"ar1": 0.080228,
"ma1": 0.099658,
"omega": 4.24e-06,
"alpha1": 0.098798,
"beta1": 0.88471,
"PerfDiff": 0.050353 
},
{
 "industry": "Other",
"mu": 0.00053762,
"ar1": 0.09262,
"ma1": 0.047702,
"omega": 9.5592e-07,
"alpha1": 0.074327,
"beta1": 0.92467,
"PerfDiff": 0.051239 
},
{
 "industry": "Toys",
"mu": 0.00060552,
"ar1": -0.054008,
"ma1": 0.16669,
"omega": 5.517e-06,
"alpha1": 0.085645,
"beta1": 0.89044,
"PerfDiff": 0.0085864 
},
{
 "industry": "Beer",
"mu": 0.0006587,
"ar1": -0.085863,
"ma1": 0.16657,
"omega": 1.1769e-06,
"alpha1": 0.06611,
"beta1": 0.9269,
"PerfDiff": -0.038015 
},
{
 "industry": "PerSv",
"mu": 0.00066837,
"ar1": 0.18288,
"ma1": -0.051095,
"omega": 2.8105e-06,
"alpha1": 0.067704,
"beta1": 0.91603,
"PerfDiff": 0.032219 
},
{
 "industry": "Telcm",
"mu": 0.00057124,
"ar1": 0.11171,
"ma1": -0.053296,
"omega": 9.0842e-07,
"alpha1": 0.06748,
"beta1": 0.92569,
"PerfDiff": -0.0092719 
},
{
 "industry": "Food",
"mu": 0.0006007,
"ar1": 0.085065,
"ma1": 0.02578,
"omega": 9.4036e-07,
"alpha1": 0.0769,
"beta1": 0.91369,
"PerfDiff": -0.01369 
},
{
 "industry": "Util",
"mu": 0.00054677,
"ar1": 0.39545,
"ma1": -0.17877,
"omega": 6.0287e-07,
"alpha1": 0.10766,
"beta1": 0.88742,
"PerfDiff": 0.0052839 
},
{
 "industry": "Hshld",
"mu": 0.00059481,
"ar1": -0.55771,
"ma1": 0.61081,
"omega": 1.694e-06,
"alpha1": 0.068606,
"beta1": 0.91775,
"PerfDiff": -0.018602 
},
{
 "industry": "MedEq",
"mu": 0.00069352,
"ar1": -0.13436,
"ma1": 0.26073,
"omega": 3.5653e-06,
"alpha1": 0.08621,
"beta1": 0.88835,
"PerfDiff": -0.024207 
},
{
 "industry": "Drugs",
"mu": 0.00065794,
"ar1": 0.045303,
"ma1": 0.086984,
"omega": 1.6612e-06,
"alpha1": 0.076462,
"beta1": 0.91185,
"PerfDiff": -0.02621 
},
{
 "industry": "Boxes",
"mu": 0.00059984,
"ar1": 0.03458,
"ma1": 0.058175,
"omega": 2.3432e-06,
"alpha1": 0.068785,
"beta1": 0.91765,
"PerfDiff": -0.025843 
},
{
 "industry": "ElcEq",
"mu": 0.00082749,
"ar1": -0.03257,
"ma1": 0.1323,
"omega": 1.8082e-06,
"alpha1": 0.06029,
"beta1": 0.92992,
"PerfDiff": -0.009298 
},
{
 "industry": "Insur",
"mu": 0.00068614,
"ar1": 0.30038,
"ma1": -0.11229,
"omega": 1.7619e-06,
"alpha1": 0.097045,
"beta1": 0.88889,
"PerfDiff": 0.00085511 
},
{
 "industry": "BldMt",
"mu": 0.00069379,
"ar1": 0.11024,
"ma1": 0.061819,
"omega": 1.7352e-06,
"alpha1": 0.085693,
"beta1": 0.90222,
"PerfDiff": 0.012211 
},
{
 "industry": "Whlsl",
"mu": 0.00062375,
"ar1": 0.12258,
"ma1": 0.03803,
"omega": 1.4843e-06,
"alpha1": 0.085669,
"beta1": 0.90165,
"PerfDiff": 0.0070484 
},
{
 "industry": "Trans",
"mu": 0.00071638,
"ar1": 0.0051034,
"ma1": 0.14008,
"omega": 3.0119e-06,
"alpha1": 0.086898,
"beta1": 0.89442,
"PerfDiff": -0.013633 
},
{
 "industry": "Chems",
"mu": 0.00068721,
"ar1": 0.04813,
"ma1": 0.085836,
"omega": 1.1762e-06,
"alpha1": 0.066251,
"beta1": 0.92631,
"PerfDiff": -0.023074 
},
{
 "industry": "Paper",
"mu": 0.00059879,
"ar1": 0.24658,
"ma1": -0.091574,
"omega": 1.4883e-06,
"alpha1": 0.070845,
"beta1": 0.91714,
"PerfDiff": -0.0021218 
},
{
 "industry": "Clths",
"mu": 0.0005906,
"ar1": 0.27765,
"ma1": -0.11111,
"omega": 1.3827e-06,
"alpha1": 0.078087,
"beta1": 0.91457,
"PerfDiff": 0.0025725 
},
{
 "industry": "Rtail",
"mu": 0.00063599,
"ar1": 0.032357,
"ma1": 0.12331,
"omega": 1.5871e-06,
"alpha1": 0.072278,
"beta1": 0.91579,
"PerfDiff": -0.025513 
},
{
 "industry": "Books",
"mu": 0.00061775,
"ar1": 0.2149,
"ma1": -0.063248,
"omega": 1.2367e-06,
"alpha1": 0.083894,
"beta1": 0.9091,
"PerfDiff": 0.017285 
},
{
 "industry": "Rubbr",
"mu": 0.00064807,
"ar1": 0.31369,
"ma1": -0.19846,
"omega": 2.1678e-06,
"alpha1": 0.08058,
"beta1": 0.90219,
"PerfDiff": -0.0057624 
},
{
 "industry": "Aero",
"mu": 0.0008032,
"ar1": 0.038222,
"ma1": 0.089369,
"omega": 2.0719e-06,
"alpha1": 0.066346,
"beta1": 0.92351,
"PerfDiff": 0.0088872 
},
{
 "industry": "Meals",
"mu": 0.00079041,
"ar1": 0.024206,
"ma1": 0.083147,
"omega": 2.4058e-06,
"alpha1": 0.077861,
"beta1": 0.90796,
"PerfDiff": 0.0030607 
} 
],
"colorby": "PerfDiff",
"range": [ -0.072937,      0, 0.072937 ],
"colors": [ "#C11A34", "gray", "#0571B0" ],
"id": "chart" 
}
var getColors = d3.scale.linear()
  .domain(params.range)
  .range(params.colors)
  .interpolate(d3.interpolateLab);

var color = function(d) { return getColors(d[params.colorby]); };

  d3.parcoords()("#" + params.dom)
    .width(params.width)
    .height(params.height)
    .margin(params.padding)
    .data(params.data)
    .color(color)
    .alpha(0.4)
    .render()
    .shadows()
    .brushable()  // enable brushing
    .reorderable(); // enable moving axes
</script>
</div><h3>Old Static R Parallel Coordinates (not as helpful)</h3>![plot of chunk unnamed-chunk-1](assets/fig/unnamed-chunk-11.png) <p>Mu and alpha1 seem to most heavily influence the ability of a moving average system to outperform.&nbsp; Let us isolate our chart to mu and alpha1 and add ar1 based on the findings of the authors.&nbsp; I am very tempted to try to explain GARCH here, but for the sake of brevity, I will refrain.&nbsp; This <a href="http://scholar.google.com/scholar?cluster=1570505569310094643&amp;hl=en&amp;as_sdt=0,1" target="_blank">paper</a> and this <a href="http://www.portfolioprobe.com/2012/07/06/a-practical-introduction-to-garch-modeling/" target="_blank">Portfolio Probe post</a> offer a good introduction to GARCH.</p>
![plot of chunk unnamed-chunk-1](assets/fig/unnamed-chunk-12.png) <p>In conclusion, it seems the same effects observed by the authors also apply to US industry indexes.&nbsp; In future posts, I will add a little more statistical rigor to the analysis and apply to other indexes.</p>
<p>Now, I just cannot resist using a horizon plot to evaluate the rolling 250 day excess returns of a moving average system over buy and hold.&nbsp; As you can see, a bull market favors buy and hold.&nbsp; The 70s and 2008-2009 were very kind to a moving average approach.</p>
<h3>Old Static R Horizon Plot</h3>![plot of chunk unnamed-chunk-1](assets/fig/unnamed-chunk-13.png) 


