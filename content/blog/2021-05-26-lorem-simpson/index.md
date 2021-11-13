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
output: hugodown::md_document()
---
<script src="{{< blogdown/postref >}}index_files/clipboard/clipboard.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/xaringanExtra-clipboard/xaringanExtra-clipboard.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/xaringanExtra-clipboard/xaringanExtra-clipboard.js"></script>
<script>window.xaringanExtraClipboard(null, {"button":"<i class=\"fa fa-clipboard\"><\/i> Copy Code","success":"<i class=\"fa fa-check\" style=\"color: #90BE6D\"><\/i> Copied!","error":"Press Ctrl+C to Copy"})</script>
<link href="{{< blogdown/postref >}}index_files/font-awesome/css/all.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index_files/font-awesome/css/v4-shims.css" rel="stylesheet" />



## Some code to <mark class="black_red">start</mark>

Some test `text09` 

hi <i class="fas fa-hands-helping"></i>
<p class="blue">This is a paragraph</p>

### Libraries Used


```r
library(flair)
library(dplyr)
library(ggplot2)
```

### ggplot


```r
iris %>%
  group_by(Species) %>%
  summarize(mean(Sepal.Length))
```

```
## # A tibble: 3 x 2
##   Species    `mean(Sepal.Length)`
##   <fct>                     <dbl>
## 1 setosa                     5.01
## 2 versicolor                 5.94
## 3 virginica                  6.59
```


<pre><code class='language-r'><code>iris <span style="background-color:#ffff7f">%>%</span><br>&nbsp;&nbsp;<span style="color:brown">group_by</span>(Species) <span style="background-color:#ffff7f">%>%</span><br>&nbsp;&nbsp;<span style="color:brown">summarize</span>(<span style="color:brown">mean</span>(Sepal.Length))</code></code></pre>

```

## # A tibble: 3 x 2
##   Species    `mean(Sepal.Length)`
##   <fct>                     <dbl>
## 1 setosa                     5.01
## 2 versicolor                 5.94
## 3 virginica                  6.59

```





<pre><code class='language-r'><code><span style="color:Coral;text-decoration:underline">ggplot</span>(<span style="background-color:Aquamarine">iris</span>, <span style="color:Coral;text-decoration:underline">aes</span>(<span style="color:CornflowerBlue">x</span> = <span style="background-color:Aquamarine"><span style="background-color:pink">Sepal.Length</span></span>, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;y = <span style="background-color:Aquamarine"><span style="background-color:pink">Petal.Length</span></span>, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color = <span style="background-color:Aquamarine">Species</span>)) +<br>&nbsp;&nbsp;<span style="color:Coral;text-decoration:underline">geom_point</span>()</code></code></pre>


<img src="{{< blogdown/postref >}}index_files/figure-html/how_to_ggplot-flaired-1.png" width="672" style="display: block; margin: auto;" />

<details>
  <summary>Click to expand!</summary>


```r
mtcars[1:5, "mpg"]
```

```
## [1] 21.0 21.0 22.8 21.4 18.7
```

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
  <summary>Click to expand!</summary>
  
```r
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


