---
title: "Recreation of charts in BOJ reports"
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

#### Year-on-year rate of increase in the producer price index (PPI) by product groups

<table width="100%" style="border: none; border-collapse: collapse;">
<tr style="border: none;">
<td width="45%" valign="top" style="border: none; padding-right: 20px;" markdown="1">

Recreation of Chart 33 in BOJ's [Outlook for Economic Activity and Prices (July 2026).](https://www.boj.or.jp/en/mopo/outlook/index.htm)

Data source: [BOJ Time-Series Data Search](https://www.stat-search.boj.or.jp/index_en.html)
Time-series: Corporate Goods Price Index (2020 base), Producer Price Index

**Notes:**

Product groups were combined as follows:

<div style="font-size: 0.85em;" markdown="1">

**Petroleum and coal products, nonferrous metals**: Petroleum and coal products, Nonferrous metals

**Materials (chemicals, plastic products, metals, etc.)**: Chemicals and related products, Plastic products, Ceramic, stone and clay products, Iron and steel, Metal products, Pulp, paper and related products, Lumber and wood products

**Machinery**: General purpose machinery, Production machinery, Business oriented machinery, Electrical machinery and equipment, Transportation equipment, Information and communications equipment

**Beverages and foods, etc.**: Beverages and foods, Agriculture, forestry and fishery products

**Other**: everything else

</div>

</td>
<td width="55%" valign="top" style="border: none;" markdown="1">

<div align="center">
<img src="/assets/images/figures-recreation/fig_ppi.png" width="600">
<p style="text-align: center !important;"> </p>
</div>
<br>

</td>
</tr>
</table>

#### Year-on-year rate of increase in import price index by source of change

<table width="100%" style="border: none; border-collapse: collapse;">
<tr style="border: none;">
<td width="45%" valign="top" style="border: none; padding-right: 20px;" markdown="1">

Recreation of Chart 45 in BOJ's [Outlook for Economic Activity and Prices (July 2026).](https://www.boj.or.jp/en/mopo/outlook/index.htm)

Data source: [BOJ Time-Series Data Search](https://www.stat-search.boj.or.jp/index_en.html)
Time-series: Corporate Goods Price Index (2020 base), Import price index, Yen basis and Contract currency basis

**Notes:**
The change driven by commodity prices is calculated as the year-on-year change in import price index on a contract currency, while the change driven by exchange rates is calculated as the difference between the year-on-year changes in the import price index on a yen basis and on a contract currency basis.

</td>
<td width="55%" valign="top" style="border: none;" markdown="1">

<div align="center">
<img src="/assets/images/figures-recreation/fig_import_prices.png" width="600">
<p style="text-align: center !important;"> </p>
</div>
<br>

</td>
</tr>
</table>
