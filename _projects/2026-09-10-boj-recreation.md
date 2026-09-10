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
<td width="45%" valign="top" style="border: none; padding-right: 20px;">

Recreation of Chart 33 in BOJ's [Outlook for Economic Activity and Prices (July 2026).](https://www.boj.or.jp/en/mopo/outlook/index.htm)

Data source: [BOJ Time-Series Data Search](https://www.stat-search.boj.or.jp/index_en.html)
Time-series: Corporate Goods Price Index (2020 base), Producer Price Index

**Notes:**

Product groups were combined as follows:

<div style="font-size: 0.85em;">

**Petroleum and coal products, nonferrous metals**: <span style="background-color:#4A7EBB; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Petroleum and coal products</span>, <span style="background-color:#D9822B; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Nonferrous metals</span>

**Materials (chemicals, plastic products, metals, etc.)**: <span style="background-color:#4A7EBB; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Chemicals and related products</span>, <span style="background-color:#D9822B; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Plastic products</span>, <span style="background-color:#5B9E5B; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Ceramic, stone and clay products</span>, <span style="background-color:#B34D6E; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Iron and steel</span>, <span style="background-color:#8B5FA3; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Metal products</span>, <span style="background-color:#4A7EBB; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Pulp, paper and related products</span>, <span style="background-color:#D9822B; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Lumber and wood products</span>

**Machinery**: <span style="background-color:#4A7EBB; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">General purpose machinery</span>, <span style="background-color:#D9822B; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Production machinery</span>, <span style="background-color:#5B9E5B; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Business oriented machinery</span>, <span style="background-color:#B34D6E; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Electrical machinery and equipment</span>, <span style="background-color:#8B5FA3; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Transportation equipment</span>, <span style="background-color:#4A7EBB; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Information and communications equipment</span>

**Beverages and foods, etc.**: <span style="background-color:#4A7EBB; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Beverages and foods</span>, <span style="background-color:#D9822B; color:white; padding:1px 8px; border-radius:6px; font-weight:600;">Agriculture, forestry and fishery products</span>

**Other**: everything else

</div>

</td>
<td width="55%" valign="top" style="border: none;">

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
<td width="45%" valign="top" style="border: none; padding-right: 20px;">

Recreation of Chart 45 in BOJ's [Outlook for Economic Activity and Prices (July 2026).](https://www.boj.or.jp/en/mopo/outlook/index.htm)

Data source: [BOJ Time-Series Data Search](https://www.stat-search.boj.or.jp/index_en.html)
Time-series: Corporate Goods Price Index (2020 base), Import price index, Yen basis and Contract currency basis

**Notes:**
The change driven by commodity prices is calculated as the year-on-year change in import price index on a contract currency, while the change driven by exchange rates is calculated as the difference between the year-on-year changes in the import price index on a yen basis and on a contract currency basis.

</div>

</td>
<td width="55%" valign="top" style="border: none;">

<div align="center">
<img src="/assets/images/figures-recreation/fig_import_prices.png" width="600">
<p style="text-align: center !important;"> </p>
</div>
<br>

</td>
</tr>
</table>
