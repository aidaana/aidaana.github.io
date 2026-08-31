---
title: "Kyrgyzstan's Phillips curves"
subtitle: ""
layout: post
category: data-analysis
---

<style>
  html {
    scroll-padding-top: 140px !important;
    scroll-behavior: smooth; /* Optional: adds a smooth transition effect */
  }
  /* Automatically add an empty line gap below all paragraphs */
  p { 
    margin-bottom: 25px !important; 
  }
  
  /* Automatically add an empty line gap below all markdown tables */
  table { 
    display: table !important;           /* Overrides theme structural box locks */
    max-width: 75% !important;           /* Adjusts target size layout footprint */
    margin-left: auto !important;        /* Computes centered alignment blocks */
    margin-right: auto !important;       /* Computes centered alignment blocks */
    margin-bottom: 35px !important;      /* Keeps the empty line gap below the table */
    font-size: 0.9em !important;
  }
  
   /* Unbolds the top row headers */
  table th {
    font-weight: normal !important;      /* Changes text from bold to standard weight */
  }
  
  /* Automatically add spacing above and below section headers */
  h3, h4, h5 { 
    margin-top: 40px !important;
    margin-bottom: 20px !important; 
  }
</style>

<script>MathJax = { tex: { tags: 'ams', inlineMath: [['$', '$'], ['\\(', '\\)']] }};</script><script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script><script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

<div style="margin-top: 15px; margin-bottom: 30px;">
  <a href="https://github.com/aidaana/present-value-current-account.git" target="_blank" style="display: inline-flex; align-items: center; gap: 6px; padding: 5px 12px; border: 1px solid light-dark(#ccc, #444); border-radius: 4px; color: light-dark(#333, #ccc); font-size: 0.85em; text-decoration: none; background: transparent; font-weight: 500;">
    📁 Code & Data on GitHub →
  </a>
</div>

In most economics textbooks and news articles, one often hears about the "flattening" or "breaking down" of the Phillips curve. The flattening implies that the low unemployment rate is no longer strongly associated with high inflation. Kyrgyzstan, in contrast, seems to have transitioned from an unusual, upward-slopping Phillips curve to a classical, downward-slopping one.

As the chart below shows, eleven years spanning 2005-2015 are characterized by a positive relationship between inflation and unemployment, in sharp contrast to the traditional trade-off theory. However, from 2016 onward, this relatinship reversed, as illustrated by a traditional Phillips curve. It means, periods of higher unemployment rate are now associated with periods of low inflation, and vice versa. 

<div align="center">
<img src="/assets/images/figures-phillips/fig_main.png" width="700">
<p style="text-align: center !important;"> </p>
</div>
<br>

One peculiar feature of the two scatter plots is that they are not overlapping horizontally. This is because,  the overall range of the unemployment rate shifted between the two periods: 7.4-8.8% in 2005-2015 and 2.9-7.4% in 2016-2025. If we believe the data, annual unemployment rate has been steadily decreasing every year since 2010, except for 2020.

Data availability is one of the obstacles many face when doing research or data exploration concerning small developing countries like Kyrgyzstan. Some weaknesses of the database published by the National Statistical Committee, the country's main data aggregator and publisher, include short time series, delayed and infrequent updates, the lack of a structured, properly maintained database, and a deficient methodology.

For example, monthly and quarterly inflation data is available only from 2003. Inflation expectations data are mostly lacking, making it hard to construct inflation-augmented curves. Meanwhile, data needed to calculate unemployment rate are still published only once a year, while monthly data is available only for the number of officially registered unemployed persons. This has prompted me to mannually construct quarterly unemployment rate series by first calculating, for each year, the ratio of average officially registered unemployed to the annual survey-based unemployed figure. I then apply this ratio to each quarter's average registered count and divide by that year's labor force to obtain a constructed quarterly unemployment rate. 

<div align="center">
<img src="/assets/images/figures-phillips/fig_inflation.png" width="700">
<p style="text-align: center !important;"> </p>
</div>
<br>

After the collapse of the Soviet Union, Kyrgyzstan experienced very high levels of inflation, averaging 24.3% over five years from 1995 through 2000. Increase of prices sharply dropped to 6.9% in 2001 and ranged from 2.1% to 5.6% over the next five years. But prices in 2007-2011 were very volatile, first spiking in 2007 and 2008 as global prices soared, then subsided in 2009 due to sluggish demand following global crisis, only spiking again in 2010 and 2011 following the political unrest in the country. Against the background of more tight monetary policy and relatively stabilized markets, annual inflation ran in single-digit figures, averaging 4%, during nine years from 2012 through 2020. Then for the first time since 2011, the country experienced double-digit inflation: 11.9% in 2021, 13.9% in 2022 and 10.8% in 2023, following post-pandemic inflation and Russia-Ukraine war.

<div align="center">
<img src="/assets/images/figures-phillips/fig_unemployment.png" width="700">
<p style="text-align: center !important;"> </p>
</div>
<br>

In contrast, the chart showing unemployment rate is relatively simpler. The survey-based methodology took start only in 2002. So, it doesn't make much sense to compare data after 2002 to prior low unemployment rate data, which were based on officialy documented records. The data suggests that unemployment rate has been decreasing every year since 2002, when it was 12.5%, down to 3.3% in 2025, except for slightly higher figures in 2008-2010 and 2020. 

Population has clearly become more economically active. However, factors such as low rate of registering one's unemployment status and a lack of monthly or quarterly population surveys make it hard to identify more dynamic business cycle signals. This is why we can only roughly make a guess that Kyrgyzstan's Phillips curve transitioned from an upward-sloping to a downward-sloping relationship. The plausible explanations behind this transition are (1) the shift of inflation drivers from supply-side shocks toward more conventional, demand-driven factors such as dynamics in labor markets or  (2) stronger monetary policy anchoring of inflation expectations.
