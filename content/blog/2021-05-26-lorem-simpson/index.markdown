---
title: "Testing flair in Hugo Apero"
subtitle: "Testing change in rmarkdown"
excerpt: "Testing out some r packages"
date: 2021-05-26
author: "JauntyJJS"
draft: true
images:
series:
tags:
categories:
layout: single
---

<script src="{{< blogdown/postref >}}index_files/clipboard/clipboard.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/xaringanExtra-clipboard/xaringanExtra-clipboard.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/xaringanExtra-clipboard/xaringanExtra-clipboard.js"></script>
<script>window.xaringanExtraClipboard(null, {"button":"<i class=\"fa fa-clipboard\"><\/i> Copy Code","success":"<i class=\"fa fa-check\" style=\"color: #90BE6D\"><\/i> Copied!","error":"Press Ctrl+C to Copy"})</script>
<link href="{{< blogdown/postref >}}index_files/font-awesome/css/all.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index_files/font-awesome/css/v4-shims.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>

## Some code to <mark class="black_red">start</mark>

Some test `text09`

hi <i class="fas fa-hands-helping"></i>

<p class="blue">
This is a paragraph
</p>

``` r
library(flair)
library(dplyr)
library(ggplot2)
library(plotly)
```

## Introduction

### plotly

<pre><code class='language-r'><code>p <- <span style="color:Coral;text-decoration:underline">ggplot</span>(<span style="background-color:Aquamarine">iris</span>, <span style="color:Coral;text-decoration:underline">aes</span>(<span style="color:CornflowerBlue">x</span> = <span style="background-color:Aquamarine"><span style="background-color:pink">Sepal.Length</span></span>, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;y = <span style="background-color:Aquamarine"><span style="background-color:pink">Petal.Length</span></span>, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color = <span style="background-color:Aquamarine">Species</span>)) +<br>&nbsp;&nbsp;<span style="color:Coral;text-decoration:underline">geom_point</span>()<br><br>plotly::<span style="color:Coral;text-decoration:underline">ggplotly</span>(<span style="background-color:Aquamarine">p</span>)</code></code></pre>
<div id="htmlwidget-1" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"data":[{"x":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5],"y":[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4],"text":["Sepal.Length: 5.1<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 4.9<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 4.7<br />Petal.Length: 1.3<br />Species: setosa","Sepal.Length: 4.6<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.0<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 5.4<br />Petal.Length: 1.7<br />Species: setosa","Sepal.Length: 4.6<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 5.0<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 4.4<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 4.9<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.4<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 4.8<br />Petal.Length: 1.6<br />Species: setosa","Sepal.Length: 4.8<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 4.3<br />Petal.Length: 1.1<br />Species: setosa","Sepal.Length: 5.8<br />Petal.Length: 1.2<br />Species: setosa","Sepal.Length: 5.7<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.4<br />Petal.Length: 1.3<br />Species: setosa","Sepal.Length: 5.1<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 5.7<br />Petal.Length: 1.7<br />Species: setosa","Sepal.Length: 5.1<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.4<br />Petal.Length: 1.7<br />Species: setosa","Sepal.Length: 5.1<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 4.6<br />Petal.Length: 1.0<br />Species: setosa","Sepal.Length: 5.1<br />Petal.Length: 1.7<br />Species: setosa","Sepal.Length: 4.8<br />Petal.Length: 1.9<br />Species: setosa","Sepal.Length: 5.0<br />Petal.Length: 1.6<br />Species: setosa","Sepal.Length: 5.0<br />Petal.Length: 1.6<br />Species: setosa","Sepal.Length: 5.2<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.2<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 4.7<br />Petal.Length: 1.6<br />Species: setosa","Sepal.Length: 4.8<br />Petal.Length: 1.6<br />Species: setosa","Sepal.Length: 5.4<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.2<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.5<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 4.9<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.0<br />Petal.Length: 1.2<br />Species: setosa","Sepal.Length: 5.5<br />Petal.Length: 1.3<br />Species: setosa","Sepal.Length: 4.9<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 4.4<br />Petal.Length: 1.3<br />Species: setosa","Sepal.Length: 5.1<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.0<br />Petal.Length: 1.3<br />Species: setosa","Sepal.Length: 4.5<br />Petal.Length: 1.3<br />Species: setosa","Sepal.Length: 4.4<br />Petal.Length: 1.3<br />Species: setosa","Sepal.Length: 5.0<br />Petal.Length: 1.6<br />Species: setosa","Sepal.Length: 5.1<br />Petal.Length: 1.9<br />Species: setosa","Sepal.Length: 4.8<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 5.1<br />Petal.Length: 1.6<br />Species: setosa","Sepal.Length: 4.6<br />Petal.Length: 1.4<br />Species: setosa","Sepal.Length: 5.3<br />Petal.Length: 1.5<br />Species: setosa","Sepal.Length: 5.0<br />Petal.Length: 1.4<br />Species: setosa"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(248,118,109,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)"}},"hoveron":"points","name":"setosa","legendgroup":"setosa","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7],"y":[4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1],"text":["Sepal.Length: 7.0<br />Petal.Length: 4.7<br />Species: versicolor","Sepal.Length: 6.4<br />Petal.Length: 4.5<br />Species: versicolor","Sepal.Length: 6.9<br />Petal.Length: 4.9<br />Species: versicolor","Sepal.Length: 5.5<br />Petal.Length: 4.0<br />Species: versicolor","Sepal.Length: 6.5<br />Petal.Length: 4.6<br />Species: versicolor","Sepal.Length: 5.7<br />Petal.Length: 4.5<br />Species: versicolor","Sepal.Length: 6.3<br />Petal.Length: 4.7<br />Species: versicolor","Sepal.Length: 4.9<br />Petal.Length: 3.3<br />Species: versicolor","Sepal.Length: 6.6<br />Petal.Length: 4.6<br />Species: versicolor","Sepal.Length: 5.2<br />Petal.Length: 3.9<br />Species: versicolor","Sepal.Length: 5.0<br />Petal.Length: 3.5<br />Species: versicolor","Sepal.Length: 5.9<br />Petal.Length: 4.2<br />Species: versicolor","Sepal.Length: 6.0<br />Petal.Length: 4.0<br />Species: versicolor","Sepal.Length: 6.1<br />Petal.Length: 4.7<br />Species: versicolor","Sepal.Length: 5.6<br />Petal.Length: 3.6<br />Species: versicolor","Sepal.Length: 6.7<br />Petal.Length: 4.4<br />Species: versicolor","Sepal.Length: 5.6<br />Petal.Length: 4.5<br />Species: versicolor","Sepal.Length: 5.8<br />Petal.Length: 4.1<br />Species: versicolor","Sepal.Length: 6.2<br />Petal.Length: 4.5<br />Species: versicolor","Sepal.Length: 5.6<br />Petal.Length: 3.9<br />Species: versicolor","Sepal.Length: 5.9<br />Petal.Length: 4.8<br />Species: versicolor","Sepal.Length: 6.1<br />Petal.Length: 4.0<br />Species: versicolor","Sepal.Length: 6.3<br />Petal.Length: 4.9<br />Species: versicolor","Sepal.Length: 6.1<br />Petal.Length: 4.7<br />Species: versicolor","Sepal.Length: 6.4<br />Petal.Length: 4.3<br />Species: versicolor","Sepal.Length: 6.6<br />Petal.Length: 4.4<br />Species: versicolor","Sepal.Length: 6.8<br />Petal.Length: 4.8<br />Species: versicolor","Sepal.Length: 6.7<br />Petal.Length: 5.0<br />Species: versicolor","Sepal.Length: 6.0<br />Petal.Length: 4.5<br />Species: versicolor","Sepal.Length: 5.7<br />Petal.Length: 3.5<br />Species: versicolor","Sepal.Length: 5.5<br />Petal.Length: 3.8<br />Species: versicolor","Sepal.Length: 5.5<br />Petal.Length: 3.7<br />Species: versicolor","Sepal.Length: 5.8<br />Petal.Length: 3.9<br />Species: versicolor","Sepal.Length: 6.0<br />Petal.Length: 5.1<br />Species: versicolor","Sepal.Length: 5.4<br />Petal.Length: 4.5<br />Species: versicolor","Sepal.Length: 6.0<br />Petal.Length: 4.5<br />Species: versicolor","Sepal.Length: 6.7<br />Petal.Length: 4.7<br />Species: versicolor","Sepal.Length: 6.3<br />Petal.Length: 4.4<br />Species: versicolor","Sepal.Length: 5.6<br />Petal.Length: 4.1<br />Species: versicolor","Sepal.Length: 5.5<br />Petal.Length: 4.0<br />Species: versicolor","Sepal.Length: 5.5<br />Petal.Length: 4.4<br />Species: versicolor","Sepal.Length: 6.1<br />Petal.Length: 4.6<br />Species: versicolor","Sepal.Length: 5.8<br />Petal.Length: 4.0<br />Species: versicolor","Sepal.Length: 5.0<br />Petal.Length: 3.3<br />Species: versicolor","Sepal.Length: 5.6<br />Petal.Length: 4.2<br />Species: versicolor","Sepal.Length: 5.7<br />Petal.Length: 4.2<br />Species: versicolor","Sepal.Length: 5.7<br />Petal.Length: 4.2<br />Species: versicolor","Sepal.Length: 6.2<br />Petal.Length: 4.3<br />Species: versicolor","Sepal.Length: 5.1<br />Petal.Length: 3.0<br />Species: versicolor","Sepal.Length: 5.7<br />Petal.Length: 4.1<br />Species: versicolor"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(0,186,56,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(0,186,56,1)"}},"hoveron":"points","name":"versicolor","legendgroup":"versicolor","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"y":[6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],"text":["Sepal.Length: 6.3<br />Petal.Length: 6.0<br />Species: virginica","Sepal.Length: 5.8<br />Petal.Length: 5.1<br />Species: virginica","Sepal.Length: 7.1<br />Petal.Length: 5.9<br />Species: virginica","Sepal.Length: 6.3<br />Petal.Length: 5.6<br />Species: virginica","Sepal.Length: 6.5<br />Petal.Length: 5.8<br />Species: virginica","Sepal.Length: 7.6<br />Petal.Length: 6.6<br />Species: virginica","Sepal.Length: 4.9<br />Petal.Length: 4.5<br />Species: virginica","Sepal.Length: 7.3<br />Petal.Length: 6.3<br />Species: virginica","Sepal.Length: 6.7<br />Petal.Length: 5.8<br />Species: virginica","Sepal.Length: 7.2<br />Petal.Length: 6.1<br />Species: virginica","Sepal.Length: 6.5<br />Petal.Length: 5.1<br />Species: virginica","Sepal.Length: 6.4<br />Petal.Length: 5.3<br />Species: virginica","Sepal.Length: 6.8<br />Petal.Length: 5.5<br />Species: virginica","Sepal.Length: 5.7<br />Petal.Length: 5.0<br />Species: virginica","Sepal.Length: 5.8<br />Petal.Length: 5.1<br />Species: virginica","Sepal.Length: 6.4<br />Petal.Length: 5.3<br />Species: virginica","Sepal.Length: 6.5<br />Petal.Length: 5.5<br />Species: virginica","Sepal.Length: 7.7<br />Petal.Length: 6.7<br />Species: virginica","Sepal.Length: 7.7<br />Petal.Length: 6.9<br />Species: virginica","Sepal.Length: 6.0<br />Petal.Length: 5.0<br />Species: virginica","Sepal.Length: 6.9<br />Petal.Length: 5.7<br />Species: virginica","Sepal.Length: 5.6<br />Petal.Length: 4.9<br />Species: virginica","Sepal.Length: 7.7<br />Petal.Length: 6.7<br />Species: virginica","Sepal.Length: 6.3<br />Petal.Length: 4.9<br />Species: virginica","Sepal.Length: 6.7<br />Petal.Length: 5.7<br />Species: virginica","Sepal.Length: 7.2<br />Petal.Length: 6.0<br />Species: virginica","Sepal.Length: 6.2<br />Petal.Length: 4.8<br />Species: virginica","Sepal.Length: 6.1<br />Petal.Length: 4.9<br />Species: virginica","Sepal.Length: 6.4<br />Petal.Length: 5.6<br />Species: virginica","Sepal.Length: 7.2<br />Petal.Length: 5.8<br />Species: virginica","Sepal.Length: 7.4<br />Petal.Length: 6.1<br />Species: virginica","Sepal.Length: 7.9<br />Petal.Length: 6.4<br />Species: virginica","Sepal.Length: 6.4<br />Petal.Length: 5.6<br />Species: virginica","Sepal.Length: 6.3<br />Petal.Length: 5.1<br />Species: virginica","Sepal.Length: 6.1<br />Petal.Length: 5.6<br />Species: virginica","Sepal.Length: 7.7<br />Petal.Length: 6.1<br />Species: virginica","Sepal.Length: 6.3<br />Petal.Length: 5.6<br />Species: virginica","Sepal.Length: 6.4<br />Petal.Length: 5.5<br />Species: virginica","Sepal.Length: 6.0<br />Petal.Length: 4.8<br />Species: virginica","Sepal.Length: 6.9<br />Petal.Length: 5.4<br />Species: virginica","Sepal.Length: 6.7<br />Petal.Length: 5.6<br />Species: virginica","Sepal.Length: 6.9<br />Petal.Length: 5.1<br />Species: virginica","Sepal.Length: 5.8<br />Petal.Length: 5.1<br />Species: virginica","Sepal.Length: 6.8<br />Petal.Length: 5.9<br />Species: virginica","Sepal.Length: 6.7<br />Petal.Length: 5.7<br />Species: virginica","Sepal.Length: 6.7<br />Petal.Length: 5.2<br />Species: virginica","Sepal.Length: 6.3<br />Petal.Length: 5.0<br />Species: virginica","Sepal.Length: 6.5<br />Petal.Length: 5.2<br />Species: virginica","Sepal.Length: 6.2<br />Petal.Length: 5.4<br />Species: virginica","Sepal.Length: 5.9<br />Petal.Length: 5.1<br />Species: virginica"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(97,156,255,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(97,156,255,1)"}},"hoveron":"points","name":"virginica","legendgroup":"virginica","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":31.4155251141553},"plot_bgcolor":"rgba(235,235,235,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[4.12,8.08],"tickmode":"array","ticktext":["5","6","7","8"],"tickvals":[5,6,7,8],"categoryorder":"array","categoryarray":["5","6","7","8"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"Sepal.Length","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.705,7.195],"tickmode":"array","ticktext":["2","4","6"],"tickvals":[2,4,6],"categoryorder":"array","categoryarray":["2","4","6"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"Petal.Length","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.96751968503937},"annotations":[{"text":"Species","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"36347f3c202e":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"36347f3c202e","visdat":{"36347f3c202e":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### ggplot

``` r
iris %>%
  group_by(Species) %>%
  summarize(mean(Sepal.Length))
```

    ## # A tibble: 3 x 2
    ##   Species    `mean(Sepal.Length)`
    ##   <fct>                     <dbl>
    ## 1 setosa                     5.01
    ## 2 versicolor                 5.94
    ## 3 virginica                  6.59

<pre><code class='language-r'><code>iris <span style="background-color:#ffff7f">%>%</span><br>&nbsp;&nbsp;<span style="color:brown">group_by</span>(Species) <span style="background-color:#ffff7f">%>%</span><br>&nbsp;&nbsp;<span style="color:brown">summarize</span>(<span style="color:brown">mean</span>(Sepal.Length))</code></code></pre>


    ## # A tibble: 3 x 2
    ##   Species    `mean(Sepal.Length)`
    ##   <fct>                     <dbl>
    ## 1 setosa                     5.01
    ## 2 versicolor                 5.94
    ## 3 virginica                  6.59

<pre><code class='language-r'><code><span style="color:Coral;text-decoration:underline">ggplot</span>(<span style="background-color:Aquamarine">iris</span>, <span style="color:Coral;text-decoration:underline">aes</span>(<span style="color:CornflowerBlue">x</span> = <span style="background-color:Aquamarine"><span style="background-color:pink">Sepal.Length</span></span>, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;y = <span style="background-color:Aquamarine"><span style="background-color:pink">Petal.Length</span></span>, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color = <span style="background-color:Aquamarine">Species</span>)) +<br>&nbsp;&nbsp;<span style="color:Coral;text-decoration:underline">geom_point</span>()</code></code></pre>

<img src="{{< blogdown/postref >}}index_files/figure-html/how_to_ggplot-flaired-1.png" width="672" style="display: block; margin: auto;" />

<details>
<summary>
Click to expand!
</summary>

``` r
mtcars[1:5, "mpg"]
```

    ## [1] 21.0 21.0 22.8 21.4 18.7

</details>

## Migrating the content

{{< panelset class="greetings" >}}
{{< panel name="Hello! :wave:" >}}
  hello
{{< /panel >}}
{{< panel name="Goodbye :dash:" >}}
  goodbye
{{< /panel >}}
{{< /panelset >}}

<details>
<summary>
Click to expand!
</summary>

``` r
    ― Checking netlify.toml...
    ○ Found HUGO_VERSION = 0.82.1 in [build] context of netlify.toml.
    | Checking that Netlify & local Hugo versions match...
    | Mismatch found:  blogdown is using Hugo version (0.69.2) to build site locally.  Netlify is using Hugo version (0.82.1) to build site.
    ● [TODO] Option 1: Change HUGO_VERSION = "0.69.2" in netlify.toml to match local version.
    ● [TODO] Option 2: Use blogdown::install_hugo("0.82.1") to match Netlify version, and set options(blogdown.hugo.version = "0.82.1") in .Rprofile to pin this Hugo version (also remember to restart R).
    | Checking that Netlify & local Hugo publish directories match...
    ○ Good to go - blogdown and Netlify are using the same publish directory: public
    ― Check complete: netlify.toml
```

</details>
