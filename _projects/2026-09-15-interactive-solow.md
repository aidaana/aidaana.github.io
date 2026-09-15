---
title: "Interactive Solow growth model"
subtitle: ""
layout: post
category: study-aids
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
  <a href="https://github.com/aidaana/kyrgyzstan-phillips-curve.git" target="_blank" style="display: inline-flex; align-items: center; gap: 6px; padding: 5px 12px; border: 1px solid light-dark(#ccc, #444); border-radius: 4px; color: light-dark(#333, #ccc); font-size: 0.85em; text-decoration: none; background: transparent; font-weight: 500;">
    📁 Code & Data on GitHub →
  </a>
</div>
 
### Overview
 
The Solow growth model, a starting point in many macroeconomic modeling courses, was developed by Robert Solow and Trevor Swan in 1956. Its central conclusion is that technological (or productivity) growth, not capital accumulation, is the only driver of long-term economic growth per person.

Althouh the model is simplistic in its setup and assumptions (most notably a fixed savings rate rather than one derived from household optimization), it still remains a foundational framework for analyzing long-term growth or comparing and contrasting with other more realistic models.

Here, I outline the model and its key results, following the derivations and notations presented by Romer (2019, Chapter 1). Following the theoretical part, you can use the interactive model to see the dynamics of capital and output by trying different values of parameters. 
 
### Set-up

Assumptions:
- Population/labor $L_t$ grows at a constant exogenous rate $n$: $\dot{L}_t/L_t = n$.
- Technology $A_t$ grows at a constant exogenous rate $g$ (labor-augmenting): $\dot{A}_t/A_t = g$.
- Output is produced with capital K, labor L, and technology A.
- A constant fraction $s \in (0,1)$ of output is saved and invested every period, while the rest is consumed.
- Capital depreciates at a constant rate $\delta$.
- Closed economy with single good.
- Markets  are perfectly competitive.

Production function is
 
$$Y_t = F(K_t, A_tL_t),$$
 
and the related assumptions are:
 
- Constant returns to scale: $F(\lambda K, \lambda AL) = \lambda F(K,AL)$ for any $\lambda>0$.
- Positive and diminishing marginal products in each argument: $F_K > 0, F_{KK} < 0, \qquad F_{AL} > 0, \quad F_{AL,AL} < 0$
- Inada conditions: $\lim_{K\to 0} F_K = \infty$ and $\lim_{K\to \infty} F_K = 0$

The standard production function is of Cobb-Douglas form:
 
$$Y_t = K_t^{\alpha}(A_tL_t)^{1-\alpha}, \qquad 0<\alpha<1$$
 
Production function can be rewritten in intensive form, which expresses output per unit of effective labor, defining capital per effective worker as $\hat{k}_t \equiv K_t/(A_tL_t)$:
 
$$\hat{y}_t \equiv \frac{Y_t}{A_tL_t} = \frac{K_t^{\alpha}}{(A_tL_t)^{\alpha}} \equiv  f(\hat{k}_t) = \hat{k}_t^{\alpha}$$
 
Capital stock evolves according to the following identity:
 
$$\dot{K}_t = sY_t - \delta K_t$$
 
That is, capital stock grows with investment (a constant share $s$ of output) and gets depleted at a constant rate of depreciation $\delta$.
 
### Dynamics of capital

Differentiating $\hat{k}_t = K_t/(A_tL_t)$ with respect to time using the quotient rule yields:

$$\dot{\hat{k}}_t = \frac{\dot{K}_t}{A_tL_t} - \frac{K_t}{[A_tL_t]^2}\left[A_t\dot{L}_t + L_t\dot{A}_t\right]$$

Split the second term into two separate fractions:

$$\dot{\hat{k}}_t = \frac{\dot{K}_t}{A_tL_t} - \frac{K_t}{A_tL_t}\cdot\frac{\dot{L}_t}{L_t} - \frac{K_t}{A_tL_t}\cdot\frac{\dot{A}_t}{A_t}$$

Now substituting in $K_t/(A_tL_t) = \hat{k}_t$ (by definition), $\dot{L}_t/L_t = n$ (exogenous population growth), $\dot{A}_t/A_t = g$ (exogenous technology growth), and $\dot{K}_t = sY_t - \delta K_t$ (the capital accumulation identity), gives:

$$\dot{\hat{k}}_t = \frac{sY_t-\delta K_t}{A_tL_t} - \hat{k}_t n - \hat{k}_t g$$

Since $Y_t/(A_tL_t) = \hat{y}_t = f(\hat{k}_t)$, the above expression equals to:

$$\dot{\hat{k}}_t = sf(\hat{k}_t) - \delta\hat{k}_t - n\hat{k}_t - g\hat{k}_t$$

Finally, grouping the last three terms together leads to the compact form:
 
$$\boxed{\dot{\hat{k}}_t = s f(\hat{k}_t) - (n+g+\delta)\hat{k}_t}$$
 
This is the fundamental equation of the Solow model,  which demonstrates that capital per effective worker rises when actual investment $sf(\hat{k}_t)$ exceeds the break-even investment $(n+g+\delta)\hat{k}_t$ needed just to keep $\hat{k}_t$ constant (replacing depreciated capital and accounting for increase in effective labor).
 
### Steady State
 
A steady state is a point where $\dot{\hat{k}}_t = 0$, i.e., capital per effective worker is constant:
 
$$sf(\hat{k}^*) = (n+g+\delta)\hat{k}^*$$
 
For the Cobb-Douglas case, it will equal:
 
$$ \hat{k}^* = \left(\frac{s}{n+g+\delta}\right)^{\frac{1}{1-\alpha}}$$
 
Thus, steady-state output and consumption per effective worker are:
 
$$\hat{y}^* = (\hat{k}^*)^{\alpha} = \left(\frac{s}{n+g+\delta}\right)^{\frac{\alpha}{1-\alpha}}, \qquad \hat{c}^* = (1-s)\hat{y}^*$$
 
$\hat{k}^* $ itself is constant, but  output and consumption per worker (not per effective worker) are $y_t = A_t\hat{y}^* $ and $c_t = A_t\hat{c}^* $, which grow forever at rate $g$ once the economy is at steady state. This is the model's central result: long-run growth comes only from technological progress, not from capital accumulation or the savings rate.
 
### Summary of Key Equations
 
| Concept | Equation |
|---|---|
| Production (intensive form) | $\hat{y}_t = \hat{k}_t^\alpha$ |
| Capital accumulation | $\dot{\hat{k}}_t = s\hat{k}_t^\alpha - (n+g+\delta)\hat{k}_t$ |
| Steady-state capital | $\hat{k}^* = \left(\dfrac{s}{n+g+\delta}\right)^{1/(1-\alpha)}$ |
| Steady-state output | $\hat{y}^* = (\hat{k}^*)^\alpha$ |
| Steady-state consumption | $\hat{c}^* = (1-s)\hat{y}^*$ |

### Interactive Model

<div style="max-width: 1150px; margin: 0 auto; font-family: system-ui, sans-serif;">

  <div style="display:grid; grid-template-columns: 3.5fr 2fr; gap: 16px; align-items:start;">

    <div style="display:flex; flex-direction:column;">
      <div style="display:grid; grid-template-columns: 170px 1fr; gap: 8px; align-items:center;">
        <div style="font-size: 14px; line-height: 2.1;">
          <div><span style="display:inline-block; width:14px; height:3px; background:#276fff; vertical-align:middle;"></span> <i>s&middot;</i><span style="position:relative; display:inline-block;"><i>k</i><span style="position:absolute; top:-6px; left:50%; transform:translateX(-50%); font-size:12px;">^</span></span><sup><i>&alpha;</i></sup> <span style="color:#777; margin-left:8px;">(actual investment)</span></div>
          <div><span style="display:inline-block; width:14px; height:3px; background:#ff5b1f; vertical-align:middle;"  ></span> <i>(&delta;+n+g)&middot;</i><span style="position:relative; display:inline-block;"><i>k</i><span style="position:absolute; top:-6px; left:50%; transform:translateX(-50%); font-size:12px;">^</span></span> <span style="color:#777; margin-left:8px;">(break-even)</span></div>
          <div><span style="display:inline-block; width:9px; height:9px; border-radius:50%; background:#14232E; vertical-align:middle;"  ></span> <span style="margin-left:2px;">steady state</span> <span style="position:relative; display:inline-block;"><i>k</i><span style="position:absolute; top:-6px; left:50%; transform:translateX(-50%); font-size:12px;">^</span></span>*</div>
          <div><span style="display:inline-block; width:9px; height:9px; background:#C0392B; vertical-align:middle; transform:rotate(45deg);"  ></span> <span style="margin-left:2px;">current</span> <span style="position:relative; display:inline-block;"><i>k</i><span style="position:absolute; top:-6px; left:50%; transform:translateX(-50%); font-size:12px;">^</span></span></div>
        </div>
        <div id="solow-diagram" style="width:100%; height:320px;"></div>
      </div>

      <div style="display:grid; grid-template-columns: 170px 1fr; gap: 8px; margin-top:8px;">
        <div style="display:flex; flex-direction:column;">
          <div style="flex:1; display:flex; align-items:center; font-size: 14px; line-height: 1.9;">
            <div><span style="display:inline-block; width:14px; height:3px; background:#276fff; vertical-align:middle;"></span> <span style="position:relative; display:inline-block;"><i>k</i><span style="position:absolute; top:-6px; left:50%; transform:translateX(-50%); font-size:12px;">^</span></span><sub><i>t</i></sub> <span style="color:#777; margin-left:8px;">(capital per effective worker)</span></div>
          </div>
          <div style="flex:1; display:flex; align-items:center; font-size: 14px; line-height: 1.9;">
            <div>
              <div><span style="display:inline-block; width:14px; height:3px; background:#14232E; vertical-align:middle;"></span> <i>y<sub>t</sub></i> <span style="color:#777; margin-left:8px;">(output per worker)</span></div>
              <div><span style="display:inline-block; width:14px; height:2px; border-top:2px dotted #ff5b1f; vertical-align:middle;"></span> <i>c<sub>t</sub></i> <span style="color:#777; margin-left:8px;">(consumption per worker)</span></div>
            </div>
          </div>
        </div>
        <div id="time-paths" style="width:100%; height:400px;"></div>
      </div>
    </div>

    <div style="min-width:0;">
      <div id="readout" style="margin-bottom: 16px; font-size: 13px; color:#333; line-height:1.5;"></div>

      <div style="margin-bottom:10px;">
        <label style="font-size:13px;">Savings rate, $s$ = <span id="s-val"></span> <span style="color:#777;">(share of output invested)</span></label>
        <input type="range" id="s" min="0.05" max="0.5" step="0.01" value="0.30" style="width:100%">
      </div>

      <div style="margin-bottom:10px;">
        <label style="font-size:13px;">Capital share, $\alpha$ = <span id="alpha-val"></span> <span style="color:#777;">(output elasticity of capital)</span></label>
        <input type="range" id="alpha" min="0.2" max="0.5" step="0.01" value="0.33" style="width:100%">
      </div>

      <div style="margin-bottom:10px;">
        <label style="font-size:13px;">Depreciation, $\delta$ = <span id="delta-val"></span> <span style="color:#777;">(capital lost per period)</span></label>
        <input type="range" id="delta" min="0.01" max="0.10" step="0.005" value="0.05" style="width:100%">
      </div>

      <div style="margin-bottom:10px;">
        <label style="font-size:13px;">Population growth, $n$ = <span id="n-val"></span> <span style="color:#777;">(labor force growth rate)</span></label>
        <input type="range" id="n" min="0" max="0.05" step="0.002" value="0.01" style="width:100%">
      </div>

      <div style="margin-bottom:10px;">
        <label style="font-size:13px;">Tech growth, $g$ = <span id="g-val"></span> <span style="color:#777;">(labor-augmenting tech growth)</span></label>
        <input type="range" id="g" min="0" max="0.05" step="0.002" value="0.02" style="width:100%">
      </div>
    </div>

  </div>
</div>

<script>
window.MathJax = { tex: { inlineMath: [['$', '$']] }, svg: { fontCache: 'global' } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js" id="MathJax-script" async></script>
<script src="https://cdn.plot.ly/plotly-2.32.0.min.js"></script>
<script>
(function () {
  const N_PERIODS = 100;
  const N_POINTS = 200;
  const K0_FIXED = 1;

  const sliders = ['s', 'alpha', 'delta', 'n', 'g'];
  const els = {};
  sliders.forEach(id => { els[id] = document.getElementById(id); });

  const plotConfig = { displayModeBar: false, scrollZoom: false, doubleClick: false, responsive: true };

  const fixedAxisStyle = {
    fixedrange: true,
    autorange: false,
    showline: true,
    linewidth: 2,
    linecolor: '#222',
    gridcolor: '#e6e6e6',
    tickfont: { size: 12, color: '#222' },
    zeroline: false
  };

  function linearRange(arrays, padFrac = 0.12) {
    let max = -Infinity;
    arrays.forEach(arr => arr.forEach(v => { if (isFinite(v) && v > max) max = v; }));
    if (!isFinite(max) || max <= 0) max = 1;
    return [0, max * (1 + padFrac)];
  }

  function logRange(arrays, padFrac = 0.15) {
    let min = Infinity, max = -Infinity;
    arrays.forEach(arr => arr.forEach(v => {
      if (isFinite(v) && v > 0) { if (v < min) min = v; if (v > max) max = v; }
    }));
    if (!isFinite(min)) min = 0.1;
    if (!isFinite(max)) max = 1;
    const lo = Math.log10(min), hi = Math.log10(max);
    const span = Math.max(hi - lo, 0.3);
    return [lo - span * padFrac, hi + span * padFrac];
  }

  function niceLogTicks(loLog, hiLog) {
    const loDecade = Math.floor(loLog);
    const hiDecade = Math.ceil(hiLog);
    const vals = [];
    for (let d = loDecade; d <= hiDecade; d++) {
      [1, 2, 5].forEach(m => {
        const v = m * Math.pow(10, d);
        const lv = Math.log10(v);
        if (lv >= loLog - 1e-9 && lv <= hiLog + 1e-9) vals.push(v);
      });
    }
    return {
      tickvals: vals,
      ticktext: vals.map(v => (v >= 1 ? v.toFixed(0) : v.toFixed(1)))
    };
  }

  function readParams() {
    return {
      s: parseFloat(els.s.value),
      alpha: parseFloat(els.alpha.value),
      delta: parseFloat(els.delta.value),
      n: parseFloat(els.n.value),
      g: parseFloat(els.g.value),
      k0: K0_FIXED
    };
  }

  function updateLabels(p) {
    document.getElementById('s-val').textContent = p.s.toFixed(2);
    document.getElementById('alpha-val').textContent = p.alpha.toFixed(2);
    document.getElementById('delta-val').textContent = p.delta.toFixed(3);
    document.getElementById('n-val').textContent = p.n.toFixed(3);
    document.getElementById('g-val').textContent = p.g.toFixed(3);
  }

  function buildDiagramTraces(p) {
    const kStar = Math.pow(p.s / (p.delta + p.n + p.g), 1 / (1 - p.alpha));
    const kMax = Math.max(20, kStar * 1.3);

    const kVals = Array.from({length: N_POINTS}, (_, i) => (i + 1) * kMax / N_POINTS);
    const invest = kVals.map(k => p.s * Math.pow(k, p.alpha));
    const breakEven = kVals.map(k => (p.delta + p.n + p.g) * k);
    const yStarInvest = p.s * Math.pow(kStar, p.alpha);
    const kCurrentInvest = p.s * Math.pow(p.k0, p.alpha);

    return {
      traces: [
        { x: kVals, y: invest, mode: 'lines', line: { color: '#276fff', width: 3 }, showlegend: false,
          hovertemplate: 'k = %{x:.2f}<br>investment = %{y:.2f}<extra></extra>' },
        { x: kVals, y: breakEven, mode: 'lines', line: { color: '#ff5b1f', width: 3 }, showlegend: false,
          hovertemplate: 'k = %{x:.2f}<br>investment = %{y:.2f}<extra></extra>' },
        { x: [kStar], y: [yStarInvest], mode: 'markers', marker: { size: 10, color: '#14232E' }, showlegend: false,
          hovertemplate: 'k* = %{x:.2f}<br>investment = %{y:.2f}<extra></extra>' },
        { x: [p.k0], y: [kCurrentInvest], mode: 'markers', marker: { size: 10, color: '#C0392B', symbol: 'diamond' }, showlegend: false,
          hovertemplate: 'k = %{x:.2f}<br>investment = %{y:.2f}<extra></extra>' }
      ],
      investAll: invest.concat(breakEven).concat([yStarInvest, kCurrentInvest]),
      kMax: kMax
    };
  }

  const diagramLayout = {
    margin: { t: 24, r: 15, l: 55, b: 55 },
    xaxis: { title: '', ...fixedAxisStyle },
    yaxis: { title: { text: 'Investment/effective worker' }, ...fixedAxisStyle },
    showlegend: false,
    dragmode: false,
    title: { text: '<b>THE SOLOW DIAGRAM</b>', font: { size: 14 } },
    annotations: [
      {
        text: 'Capital/effective worker',
        xref: 'paper', x: 1, xanchor: 'right',
        yref: 'paper', y: -0.1, yanchor: 'top',
        showarrow: false,
        font: { size: 13, color: '#222' }
      }
    ]
  };

  function simulate(p) {
    const kPath = [p.k0];
    for (let t = 1; t <= N_PERIODS; t++) {
      const kPrev = kPath[t - 1];
      const kNext = kPrev + p.s * Math.pow(kPrev, p.alpha) - (p.delta + p.n + p.g) * kPrev;
      kPath.push(Math.max(kNext, 1e-6));
    }
    const t = Array.from({length: N_PERIODS + 1}, (_, i) => i);
    const A = t.map(tt => Math.pow(1 + p.g, tt));
    const yPath = t.map(i => A[i] * Math.pow(kPath[i], p.alpha));
    const cPath = yPath.map(y => (1 - p.s) * y);
    return { t, kPath, yPath, cPath };
  }

  function buildTimePathTraces(sim) {
    return [
      { x: sim.t, y: sim.kPath, mode: 'lines', line: { color: '#276fff', width: 3 }, xaxis: 'x', yaxis: 'y', showlegend: false,
        hovertemplate: 't = %{x}<br>k = %{y:.2f}<extra></extra>' },
      { x: sim.t, y: sim.yPath, mode: 'lines', line: { color: '#14232E', width: 3 }, xaxis: 'x2', yaxis: 'y2', showlegend: false,
        hovertemplate: 't = %{x}<br>y = %{y:.2f}<extra></extra>' },
      { x: sim.t, y: sim.cPath, mode: 'lines', line: { color: '#ff5b1f', width: 3, dash: 'dot' }, xaxis: 'x2', yaxis: 'y2', showlegend: false,
        hovertemplate: 't = %{x}<br>c = %{y:.2f}<extra></extra>' }
    ];
  }

  const timePathLayout = {
    margin: { t: 24, r: 15, l: 55, b: 45 },
    grid: { rows: 2, columns: 1, pattern: 'independent', roworder: 'top to bottom' },
    xaxis: { title: '', range: [0, N_PERIODS], ...fixedAxisStyle },
    yaxis: { title: { text: 'k<sup>^</sup><sub>t</sub> (log)' }, type: 'log', ...fixedAxisStyle },
    xaxis2: { title: '', range: [0, N_PERIODS], ...fixedAxisStyle },
    yaxis2: { title: { text: 'y<sub>t</sub>, c<sub>t</sub> (log)' }, type: 'log', ...fixedAxisStyle },
    showlegend: false,
    dragmode: false,
    title: { text: '<b>TRANSITION PATHS</b>', font: { size: 14 } },
    annotations: [
      {
        text: 'time',
        xref: 'paper', x: 1, xanchor: 'right',
        yref: 'paper', y: -0.08, yanchor: 'top',
        showarrow: false,
        font: { size: 13, color: '#222' }
      }
    ]
  };

  function updateReadout(p) {
    const kStar = Math.pow(p.s / (p.delta + p.n + p.g), 1 / (1 - p.alpha));
    const yStar = Math.pow(kStar, p.alpha);
    const cStar = (1 - p.s) * yStar;
    document.getElementById('readout').innerHTML =
      `<b>Steady state</b><br>$\\hat{k}^*$ = ${kStar.toFixed(2)} <span style="color:#777;">(long-run capital/eff. worker)</span><br>` +
      `$y^*$ = ${yStar.toFixed(2)} <span style="color:#777;">(long-run output/eff. worker)</span><br>` +
      `$c^*$ = ${cStar.toFixed(2)} <span style="color:#777;">(long-run consumption/eff. worker)</span><br>` +
      `long-run growth of $y_t, c_t$ = $g$ = ${(p.g * 100).toFixed(1)}%/period`;
    if (window.MathJax && window.MathJax.typesetPromise) {
      MathJax.typesetPromise([document.getElementById('readout')]);
    }
  }

  function redraw() {
    const p = readParams();
    updateLabels(p);
    updateReadout(p);

    const diagram = buildDiagramTraces(p);
    diagramLayout.xaxis.range = [0, diagram.kMax];
    diagramLayout.yaxis.range = linearRange([diagram.investAll]);
    Plotly.react('solow-diagram', diagram.traces, diagramLayout, plotConfig);

    const sim = simulate(p);
    const kRange = logRange([sim.kPath]);
    const ycRange = logRange([sim.yPath, sim.cPath]);
    timePathLayout.yaxis.range = kRange;
    timePathLayout.yaxis2.range = ycRange;

    const kTicks = niceLogTicks(kRange[0], kRange[1]);
    timePathLayout.yaxis.tickmode = 'array';
    timePathLayout.yaxis.tickvals = kTicks.tickvals;
    timePathLayout.yaxis.ticktext = kTicks.ticktext;

    const ycTicks = niceLogTicks(ycRange[0], ycRange[1]);
    timePathLayout.yaxis2.tickmode = 'array';
    timePathLayout.yaxis2.tickvals = ycTicks.tickvals;
    timePathLayout.yaxis2.ticktext = ycTicks.ticktext;

    Plotly.react('time-paths', buildTimePathTraces(sim), timePathLayout, plotConfig);
  }

  sliders.forEach(id => els[id].addEventListener('input', redraw));

  redraw();

  window.addEventListener('resize', () => {
    Plotly.Plots.resize('solow-diagram');
    Plotly.Plots.resize('time-paths');
  });

  if (window.MathJax && window.MathJax.typesetPromise) {
    MathJax.typesetPromise();
  } else {
    document.getElementById('MathJax-script').addEventListener('load', () => MathJax.typesetPromise());
  }
})();
</script>

