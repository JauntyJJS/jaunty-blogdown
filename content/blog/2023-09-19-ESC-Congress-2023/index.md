---
title: "Reflections on ESC Congress 2023"
subtitle: ""
excerpt: "This is a write up of what I have learned during the [ESC Congress](https://www.escardio.org/Congresses-Events/ESC-Congress) 2023 Edition"
format: hugo
date: 2023-9-19
author: "Jeremy Selva"
draft: true
tags:
  - ESC Congress 2023
categories:
  - ESC Congress 2023
layout: single-sidebar
editor_options: 
  chunk_output_type: console
bibliography: utils/bibliography.bib
csl: utils/esc.csl
---

<a name="top"></a>

## Table of Content

-   [Introduction](#introduction)
-   [p-values](#p-values)

## Introduction

The [European Society of Cardiology (ESC) Congress](https://www.escardio.org/Congresses-Events/ESC-Congress) is the largest conference of cardiology in Europe. It covers many topics in cardiovascular medicine, technology and research. The 2023 edition was held in Amsterdam from 25 to 28 August 2023. Below are some takeaways that I have consolidated.

<a href="#top">Back to top</a>

## p-values

A formal definition of p-value is the likelihood of observing a result that is (more) extreme than your data, if the null hypothesis were true. When used in the field of clinical trials, it is the likelihood of observing a result that is (more) extreme than the trial's results, if the treatment were truly ineffective.

p \< 0.05 was an arbitrary threshold proposed by Ronald Fisher in the 1920s to make a decision if a deviation from the null hypothesis is considered to be significant or not. The threshold over time became widely adopted in biomedical research.

The conference provides a summary and understanding of the p-values can or cannot do and its use in clinical trials.

### What p-values cannot do

-   Cannot inform how reproducible the study result is.

    -   Confidence interval can provide some information on this.

-   Cannot inform if a future study would be statistically significant.

    -   Statistical power can provide some information on this.

-   Cannot inform if the null hypothesis is true or false.

    -   It is not possible to achieve this using statistics alone.

-   Cannot inform the probability that the null hypothesis is true or false.

    -   Bayesian statistics can provide a quantification of the likelihood that the null hypothesis is true.

-   Cannot inform if a regulatory agency will approve the treatment.

    -   A [clinical trail](https://www.nejm.org/doi/full/10.1056/NEJMoa1908655)<sup>1</sup> on Sacubitril-Valsartan did not have a statistically significantly result in lowering rate of total hospitalizations for heart failure and death from cardiovascular causes among patients with heart failure but it was later [approved](https://www.medscape.com/viewarticle/945936) by the FDA to treat preserved ejection fraction (HFpEF). On the other hand, a [clinical trial](https://www.nejm.org/doi/full/10.1056/NEJMoa2025797)<sup>2</sup> on Omecamtiv Mecarbil had a statistically significantly result but was later [declined](https://www.medscape.com/viewarticle/988948) by the FDA to treat preserved ejection fraction (HFpEF)

### What p-values can do

-   Inform how incompatible the data are with a specific hypothesis or model.

-   Quantify the evidence against the null hypothesis using an "innocent until proven guilty" approach.

-   Distinguish true effect vs good luck.

    -   Larger p-value suggests that results could be attributable to the play of chance.
    -   Smaller p-value suggests that results are less likely to have occured by chance.
    -   Small enough p-value: Rule out "chance" and assume "true effect".

### Advice

It is best to improve the interpretation of p values by creating a range table to help translate them into plain English. Below is an example from this [link](https://www.jcpcarchives.org/full/p-value-statistical-significance-and-clinical-significance-121.php)<sup>3</sup> from the Journal of Clinical and Preventive Cardiology.

| Values of p         | Inference                                     |
|---------------------|-----------------------------------------------|
| p \> 0.1            | No evidence against null hypothesis.          |
| 0.05 \< p \< 0.1    | Weak evidence against null hypothesis.        |
| 0.01 \< p \< 0.05   | Moderate evidence against null hypothesis.    |
| 0.005 \< p \< 0.01  | Good evidence against null hypothesis.        |
| 0.001 \< p \< 0.005 | Strong evidence against null hypothesis.      |
| p \< 0.001          | Very strong evidence against null hypothesis. |

Include other parameters like effect size to provide additional evidence if the treatment is truly working.

## Treatment Effect in Complicated Clinical Trials

Most clinical trials usually examine a patient's time to the first occurrence of an event alone or in a composite outcome. A limitation with this approach is that given a patient with only one but early non-fatal morbidity event and a patient with a later but multiple morbidity events and subsequent death. The approach to look just at the first occurrence will wrongly identify that the former patient in a worse state the latter.

Failure to consider recurrent/multiple events and event types may lead to bias that can mask the true effect of a treatment. There is a need for clinical trial analysis to go beyond the first event such as recurrent and total events to better understand the total impact of a treatment and reveal changes in important biomarkers.

### correcting for Multiple or Recurrent Events

Fortunately there are statistical tools that are available for such complicated analysis.
For recurrent event data, the Cox proportional hazards model, used to model time to the first event can be expanded with the Lin, Wei, Yang, and Ying (LWYY) and a joint frailty model. A paper from Claggett et al. recommended some model-free approaches to quantify a patient's temporal recurrent-event profile and treatment effects using an area under the curve (AUC) approach.

An application of this can be found in this DELIVER Trial paper which uses the three methods to investigate the effect of SGLT2 inhibitor dapagliflozin on total heart failure events and cardiovascular death.

### Correcting for Mortality Endpoints

We may be interested in understanding the effect of a drug on surrogate markers like the estimated glomerular filtration rate (eGFR), blood pressure and biomarkers. The Cox proportional hazards model has its limitation because these variables are measured with error (due to biological variation) and only observable when the measured subject is alive. As such, we do not know the exact underlying value of the variable between measurements or at death (time of specific endpoint).

The Joint Model helps to mitigate the issue by bringing the survival model (modelling the mortality outcome) and the linear mixed-effects model (modelling the longitudinal outcome) together, allowing us to model the change of surrogate markers between measurements and at death (time of event). It is basically a mixed linear model that is corrected for drop-out events like death.

More information can be found in https://academic.oup.com/ckj/article/13/2/143/5818093?login=false and

### Correcting for both groups of outcomes

Unfortunately, both groups of outcomes may be measured in a clinical trial and they should not be treated as separate (independent) outcomes. The key is to create hierarchical composite endpoints to combine different clinical outcomes of patients into a composite so as to preserve their different natures. The endpoints can later be analysed using win statistics (win ratio, win odds and net benefit).

An application of this technique can be found in this Heart failure design paper.

https://www.sciencedirect.com/science/article/pii/S2213177923002457#mmc1

More information on win statistics can be found in

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10322884/

## References

<span class="csl-left-margin">1. </span><span class="csl-right-inline">Solomon SD, McMurray JJV, Anand IS, Ge J, Lam CSP, Maggioni AP, Martinez F, Packer M, Pfeffer MA, Pieske B, Redfield MM, Rouleau JL, Veldhuisen DJ van, Zannad F, Zile MR, Desai AS, Claggett B, Jhund PS, Boytsov SA, Comin-Colet J, Cleland J, Düngen H-D, Goncalvesova E, Katova T, Kerr Saraiva JF, Lelonek M, Merkely B, Senni M, Shah SJ, Zhou J, Rizkala AR, Gong J, Shi VC, Lefkowitz MP. [Angiotensin--neprilysin inhibition in heart failure with preserved ejection fraction](https://doi.org/10.1056/NEJMoa1908655). *New England Journal of Medicine* 2019;**381**:1609--1620. </span>

<span class="csl-left-margin">2. </span><span class="csl-right-inline">Teerlink JR, Diaz R, Felker GM, McMurray JJV, Metra M, Solomon SD, Adams KF, Anand I, Arias-Mendoza A, Biering-Sørensen T, Böhm M, Bonderman D, Cleland JGF, Corbalan R, Crespo-Leiro MG, Dahlström U, Echeverria LE, Fang JC, Filippatos G, Fonseca C, Goncalvesova E, Goudev AR, Howlett JG, Lanfear DE, Li J, Lund M, Macdonald P, Mareev V, Momomura S, O'Meara E, Parkhomenko A, Ponikowski P, Ramires FJA, Serpytis P, Sliwa K, Spinar J, Suter TM, Tomcsanyi J, Vandekerckhove H, Vinereanu D, Voors AA, Yilmaz MB, Zannad F, Sharpsten L, Legg JC, Varin C, Honarpour N, Abbasi SA, Malik FI, Kurtz CE. [Cardiac myosin activation with omecamtiv mecarbil in systolic heart failure](https://doi.org/10.1056/NEJMoa2025797). *New England Journal of Medicine* 2021;**384**:105--116. </span>

<span class="csl-left-margin">3. </span><span class="csl-right-inline">Padam S. [P value, statistical significance and clinical significance](https://www.jcpcarchives.org/full/p-value-statistical-significance-and-clinical-significance-121.php). *Journal of Clinical and Preventive Cardiology* 2013;**2**:202--204. </span>
