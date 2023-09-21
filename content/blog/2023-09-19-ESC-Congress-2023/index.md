---
title: "Reflections on ESC Congress 2023"
subtitle: ""
excerpt: "This is a write up of what I have learned during the [ESC Congress](https://www.escardio.org/Congresses-Events/ESC-Congress) 2023 Edition"
format: hugo
date: 2023-09-19
author: "Jeremy Selva"
draft: false
tags:
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
    -   [What p-values cannot do](#what-p-values-cannot-do)
    -   [What p-values can do](#what-p-values-can-do)
-   [Risk Scores for Cardiovascular diseases](#risk-scores-for-cardiovascular-diseases)
-   [Correcting for Multiple or Recurrent Events](#correcting-for-multiple-or-recurrent-events)
    -   [Correcting for Multiple or Recurrent Events](#correcting-for-multiple-or-recurrent-events)
    -   [Correcting for Mortality Endpoints](#correcting-for-mortality-endpoints)
    -   [Correcting for both groups of outcomes](#correcting-for-both-groups-of-outcomes)
-   [Questions to ask regarding AI](#questions-to-ask-regarding-ai)
    -   [Where is the model](#where-is-the-model)
    -   [What Information is used to build the model](#what-information-is-used-to-build-the-model)
    -   [Has the model been well developed/evaluated](#has-the-model-been-well-developedevaluated)
    -   [Other questions not covered](#other-questions-not-covered)
    -   [Is there any chance for a model to become implemented](#is-there-any-chance-for-a-model-to-become-implemented)

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

<a href="#top">Back to top</a>

## Risk Scores for Cardiovascular diseases

Prevention is usually better than cure. An accurate estimate a healthy individual's risk of developing cardiovascular diseases (CVD) and future CVD events can help identify/prioritise those who may benefit from prevention programmes like lifestyle change and/or pharmacological treatment.

In 2003, the [Systematic COronary Risk Evaluation (SCORE)](https://academic.oup.com/eurheartj/article/24/11/987/427645)<sup>4</sup> project was created to calculating an European individual 10-year risk estimates for fatal CVD over an age range of 40-65. The model was built from a pooled dataset of 12 European cohorts.

However, there were several limitations to the SCORE model. As it was used to only estimate fatal CVD, it underestimates the total CVD burden which came largely from non-fatal CVD events. The cohorts used to build the model were people who were recruited before 1986 which was no longer a decent representation of the European population.

As such, in 2021, the [SCORE2](https://doi.org/10.1093/eurheartj/ehab309)<sup>5</sup> project was launched using 45 more recent cohorts from 13 countries to allow the model to recalibrate and expand its prediction to both fatal and non-fatal CVD outcomes. External validation was also done to ensure that the SCORE2 model is reliable.

While the SCORE2 risk models are intended for use in people aged 40--69 years, there is a need to have a 10-year CVD risk prediction model for those age 70 and above. This is because traditional risk prediction models usually overestimates CVD risk for people in this age group leading to unnecessary treatment and lower quality of life. [SCORE2-Older Persons (SCORE2-OP)](https://doi.org/10.1093/eurheartj/ehab312)<sup>6</sup> was created, in parallel to SCORE2, to estimate 5- and 10-year risk of incident CVD in European people aged over 70 years.

Recently in 2023, a new algorithm is developed called [SCORE2-Diabetes](https://doi.org/10.1093/eurheartj/ehad260)<sup>7</sup>. This algorithm expands the SCORE2 algorithm using diabetes-related information like age at diagnosis of diabetes and glycated haemoglobin (HbA1c) to predict 10-year risk of CVD in European individuals with type 2 diabetes.

The evolution of the SCORE project shows that human variation cannot be completely explained by risk predictors in the model. This is because model derived in one or more populations may severely under or over estimates risk in a new population. Risk prediction models needs to be recalibrated with recent nationally representative incidence data so that it can work well across different populations and time points. In addition, while risk scoring has its advantages, it is not a replacement of usual care as there are no evidence to say that it is better.

<a href="#top">Back to top</a>

## Treatment Effect in Complicated Clinical Trials

Most clinical trials usually examine a patient's time to the first occurrence of an event alone or in a composite outcome. A limitation with this approach is that given a patient with only one but early non-fatal morbidity event and a patient with a later but multiple morbidity events and subsequent death. The approach to look just at the first occurrence will wrongly identify that the former patient in a worse state the latter.

Failure to consider recurrent/multiple events and event types may lead to bias that can mask the true effect of a treatment. There is a need for clinical trial analysis to go beyond the first event such as recurrent and total events to better understand the total impact of a treatment and reveal changes in important biomarkers.

### Correcting for Multiple or Recurrent Events

Fortunately there are statistical tools that are available for such complicated analysis.
For recurrent event data, the Cox proportional hazards model, used to model time to the first event can be expanded with the [Lin, Wei, Yang, and Ying](https://doi.org/10.1111/1467-9868.00259)<sup>8</sup> (LWYY) and a [joint frailty](https://onlinelibrary.wiley.com/doi/abs/10.1002/sim.6853)<sup>9</sup> model. A paper from [Claggett et al.](https://evidence.nejm.org/doi/abs/10.1056/EVIDoa2200047)<sup>10</sup> recommended some model-free approaches to quantify a patient's temporal recurrent-event profile and treatment effects using an area under the curve (AUC) approach.

An application of this can be found in this [DELIVER](https://doi.org/10.1001/jamacardio.2023.0711)<sup>11</sup> trial paper which uses the three methods to investigate the effect of SGLT2 inhibitor dapagliflozin on total heart failure events and cardiovascular death.

### Correcting for Mortality Endpoints

We may be interested in understanding the effect of a drug on surrogate markers like the estimated glomerular filtration rate (eGFR), blood pressure and biomarkers. The Cox proportional hazards model has its limitation because these variables are measured with error (due to biological variation) and only observable when the measured subject is alive. As such, we do not know the exact underlying value of the variable between measurements or at death (time of specific endpoint).

The [Joint Model](https://doi.org/10.1093/ckj/sfaa024)<sup>12</sup> helps to mitigate the issue by bringing the survival model (modelling the mortality outcome) and the linear mixed-effects model (modelling the longitudinal outcome) together, allowing us to model the change of surrogate markers between measurements and at death (time of event). It is basically a mixed linear model that is corrected for drop-out events like death.

### Correcting for both groups of outcomes

However, both groups of outcomes may be measured in a clinical trial and they should not be treated as separate (independent) outcomes. The key is to create hierarchical composite endpoints to combine different clinical outcomes of patients into a composite so as to preserve their different natures. The endpoints can later be analysed using win statistics (win ratio, win odds and net benefit).

An application of this technique can be found in this Heart failure design paper by [Kosiborod et al.](https://www.sciencedirect.com/science/article/pii/S2213177923002457)<sup>13</sup>.

More information on win statistics can be found in [Ajufo et al.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10322884/)<sup>14</sup>.

<a href="#top">Back to top</a>

## Questions to ask regarding AI

I had attended a talk from [Maarten van Smeden](https://twitter.com/MaartenvSmeden?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor) which summarised the [original paper](https://doi.org/10.1093/eurheartj/ehac238)<sup>15</sup> on what questions to raise when appraising the development and validation of AI prediction models. It went down to a few simple questions.

### Where is the model

While AI systems are mainly computer code, most of the AI systems are live only on the hard drive of the developer. This makes external validation by others almost impossible. The speaker believed that sharing of computer code should be the standard procedure to allow a fair evaluation of the AI prediction model.

### What Information is used to build the model

A [model](https://www.sciencedirect.com/science/article/pii/S1936879819313123?via%3Dihub)<sup>16</sup> using logistic regression to predict in-hospital mortality after Transcatheter Aortic Valve Replacement (TAVR) was met with some [skepticism](https://www.tctmd.com/news/machine-learning-helps-predict-hospital-mortality-post-tavr-skepticism-abounds) on its usefulness. While the model had the highest area under the curve (AUC) score of 0.92 compared to other published models, it was built using both preprocedural and postoperative factors. This means that the model could only be used to predict in-hospital mortality after the patient was discharged. By then, the doctors would have already known if in-hospital mortality has occurred.

The above incident shows that the right kind of information needs to be provided for the model to be effective in what it was meant to be built for. The speaker advised developers to ensure proper reporting of AI systems by using the [TRIPOD checklist](https://www.equator-network.org/reporting-guidelines/tripod-statement/)<sup>17</sup>.

### Has the model been well developed/evaluated

Researchers have evaluated different kind of models over the past few years for risk of bias and use of external validation. Unfortunately, the overall result of the review has been poor.

-   [Wynants et al.](https://www.bmj.com/content/369/bmj.m1328.long)<sup>18</sup> reviewed 606 models for prognosis of Covid-19 and found only 7 newly developed models and 22 external validations of existing models were at low risk of bias.
-   [Navarro et al.](https://www.sciencedirect.com/science/article/pii/S0895435623000756)<sup>19</sup> reported that 74 out of 133 (55.6% of) diagnostic and prognostic prediction model studies made recommendations of its models for clinical use but did not have any external validation.
-   [Dhiman et al.](https://doi.org/10.1186/s41512-022-00126-w)<sup>20</sup> investigated 152 developed prognostic models in the oncology domain and found that 84% were at high risk of bias.

### Other questions not covered

A summary of other important questions were stated but not in detail due to limited time.

-   How do we ensure implemented AI models remain safe and effective over time and place ?
    -   Model updating, monitoring, transfer learning
-   How do we ensure AI models are not leading to disadvantage for certain groups of patients ?
    -   Algorithmic bias, fairness
-   How do we let the AI tell us when a prediction is uncertain ?
    -   Conformal prediction
-   How do we increase trust and transparency of AI models ?
    -   Trustworthy AI, explainable AI

### Is there any chance for a model to become implemented

[Sculley et al.](https://papers.nips.cc/paper_files/paper/2015/hash/86df7dcfd896fcaf2674f757a2463eba-Abstract.html)<sup>21</sup> pointed out that machine Learning code is only a small fraction in a real-world machine learning architecture. The required surrounding infrastructure like automation, process and resource Management can be complicated. The risk of failure is very high. [Royen et al.](https://osf.io/sc2pz)<sup>22</sup> provided a nice overview of how implementation can go wrong in the below [leaky pipeline example](https://twitter.com/MaartenvSmeden/status/1539485495809409025).

```
{{< tweet user="MaartenvSmeden" id="1539485495809409025" >}}
```

To make the task of machine learning implementation less daunting, a [guidance article](https://www.datavoorgezondheid.nl/documenten/publicaties/2021/12/17/guideline-for-high-quality-diagnostic-and-prognostic-applications-of-ai-in-healthcare) is available.

<a href="#top">Back to top</a>

## References

<span class="csl-left-margin">1. </span><span class="csl-right-inline">Solomon SD, McMurray JJV, Anand IS, Ge J, Lam CSP, Maggioni AP, Martinez F, Packer M, Pfeffer MA, Pieske B, Redfield MM, Rouleau JL, Veldhuisen DJ van, Zannad F, Zile MR, Desai AS, Claggett B, Jhund PS, Boytsov SA, Comin-Colet J, Cleland J, Düngen H-D, Goncalvesova E, Katova T, Kerr Saraiva JF, Lelonek M, Merkely B, Senni M, Shah SJ, Zhou J, Rizkala AR, Gong J, Shi VC, Lefkowitz MP. [Angiotensin--neprilysin inhibition in heart failure with preserved ejection fraction](https://doi.org/10.1056/NEJMoa1908655). *New England Journal of Medicine* 2019;**381**:1609--1620. </span>

<span class="csl-left-margin">2. </span><span class="csl-right-inline">Teerlink JR, Diaz R, Felker GM, McMurray JJV, Metra M, Solomon SD, Adams KF, Anand I, Arias-Mendoza A, Biering-Sørensen T, Böhm M, Bonderman D, Cleland JGF, Corbalan R, Crespo-Leiro MG, Dahlström U, Echeverria LE, Fang JC, Filippatos G, Fonseca C, Goncalvesova E, Goudev AR, Howlett JG, Lanfear DE, Li J, Lund M, Macdonald P, Mareev V, Momomura S, O'Meara E, Parkhomenko A, Ponikowski P, Ramires FJA, Serpytis P, Sliwa K, Spinar J, Suter TM, Tomcsanyi J, Vandekerckhove H, Vinereanu D, Voors AA, Yilmaz MB, Zannad F, Sharpsten L, Legg JC, Varin C, Honarpour N, Abbasi SA, Malik FI, Kurtz CE. [Cardiac myosin activation with omecamtiv mecarbil in systolic heart failure](https://doi.org/10.1056/NEJMoa2025797). *New England Journal of Medicine* 2021;**384**:105--116. </span>

<span class="csl-left-margin">3. </span><span class="csl-right-inline">Padam S. [P value, statistical significance and clinical significance](https://www.jcpcarchives.org/full/p-value-statistical-significance-and-clinical-significance-121.php). *Journal of Clinical and Preventive Cardiology* 2013;**2**:202--204. </span>

<span class="csl-left-margin">4. </span><span class="csl-right-inline">Conroy RM, Pyörälä K, Fitzgerald AP, Sans S, Menotti A, De Backer G, De Bacquer D, Ducimetière P, Jousilahti P, Keil U, Njølstad I, Oganov RG, Thomsen T, Tunstall-Pedoe H, Tverdal A, Wedel H, Whincup P, Wilhelmsen L, Graham on behalf of the S project group I. M. [<span class="nocase">Estimation of ten-year risk of fatal cardiovascular disease in Europe: the SCORE project</span>](https://doi.org/10.1016/S0195-668X(03)00114-3). *European Heart Journal* 2003;**24**:987--1003. </span>

<span class="csl-left-margin">5. </span><span class="csl-right-inline">group S working, collaboration EC risk. [<span class="nocase">SCORE2 risk prediction algorithms: new models to estimate 10-year risk of cardiovascular disease in Europe</span>](https://doi.org/10.1093/eurheartj/ehab309). *European Heart Journal* 2021;**42**:2439--2454. </span>

<span class="csl-left-margin">6. </span><span class="csl-right-inline">group S-O working, collaboration EC risk. [<span class="nocase">SCORE2-OP risk prediction algorithms: estimating incident cardiovascular event risk in older persons in four geographical risk regions</span>](https://doi.org/10.1093/eurheartj/ehab312). *European Heart Journal* 2021;**42**:2455--2467. </span>

<span class="csl-left-margin">7. </span><span class="csl-right-inline">Group S-DW, ESC Cardiovascular Risk Collaboration the. [<span class="nocase">SCORE2-Diabetes: 10-year cardiovascular risk estimation in type 2 diabetes in Europe</span>](https://doi.org/10.1093/eurheartj/ehad260). *European Heart Journal* 2023;**44**:2544--2556. </span>

<span class="csl-left-margin">8. </span><span class="csl-right-inline">Lin DY, Wei LJ, Yang I, Ying Z. [<span class="nocase">Semiparametric Regression for the Mean and Rate Functions of Recurrent Events</span>](https://doi.org/10.1111/1467-9868.00259). *Journal of the Royal Statistical Society Series B: Statistical Methodology* 2002;**62**:711--730. </span>

<span class="csl-left-margin">9. </span><span class="csl-right-inline">Rogers JK, Yaroshinsky A, Pocock SJ, Stokar D, Pogoda J. [Analysis of recurrent events with an associated informative dropout time: Application of the joint frailty model](https://doi.org/10.1002/sim.6853). *Statistics in Medicine* 2016;**35**:2195--2205. </span>

<span class="csl-left-margin">10. </span><span class="csl-right-inline">Claggett BL, McCaw ZR, Tian L, McMurray JJV, Jhund PS, Uno H, Pfeffer MA, Solomon SD, Wei L-J. [Quantifying treatment effects in trials with multiple event-time outcomes](https://doi.org/10.1056/EVIDoa2200047). *NEJM Evidence* 2022;**1**:EVIDoa2200047. </span>

<span class="csl-left-margin">11. </span><span class="csl-right-inline">Jhund PS, Claggett BL, Talebi A, Butt JH, Gasparyan SB, Wei L-J, McCaw ZR, Wilderäng U, Bengtsson O, Desai AS, Petersson M, Langkilde AM, Boer RA de, Hernandez AF, Inzucchi SE, Kosiborod MN, Lam CSP, Martinez FA, Shah SJ, Vaduganathan M, Solomon SD, McMurray JJV. [<span class="nocase">Effect of Dapagliflozin on Total Heart Failure Events in Patients With Heart Failure With Mildly Reduced or Preserved Ejection Fraction: A Prespecified Analysis of the DELIVER Trial</span>](https://doi.org/10.1001/jamacardio.2023.0711). *JAMA Cardiology* 2023;**8**:554--563. </span>

<span class="csl-left-margin">12. </span><span class="csl-right-inline">Chesnaye NC, Tripepi G, Dekker FW, Zoccali C, Zwinderman AH, Jager KJ. [<span class="nocase">An introduction to joint models---applications in nephrology</span>](https://doi.org/10.1093/ckj/sfaa024). *Clinical Kidney Journal* 2020;**13**:143--149. </span>

<span class="csl-left-margin">13. </span><span class="csl-right-inline">Kosiborod MN, Abildstrøm SZ, Borlaug BA, Butler J, Christensen L, Davies M, Hovingh KG, Kitzman DW, Lindegaard ML, Møller DV, Shah SJ, Treppendahl MB, Verma S, Petrie MC. [Design and baseline characteristics of STEP-HFpEF program evaluating semaglutide in patients with obesity HFpEF phenotype](https://doi.org/10.1016/j.jchf.2023.05.010). *JACC: Heart Failure* 2023;**11**:1000--1010. </span>

<span class="csl-left-margin">14. </span><span class="csl-right-inline">Ajufo E, Nayak A, Mehra MR. [Fallacies of using the win ratio in cardiovascular trials: Challenges and solutions](https://doi.org/10.1016/j.jacbts.2023.05.004). *JACC: Basic to Translational Science* 2023;**8**:720--727. </span>

<span class="csl-left-margin">15. </span><span class="csl-right-inline">Smeden M van, Heinze G, Van Calster B, Asselbergs FW, Vardas PE, Bruining N, Jaegere P de, Moore JH, Denaxas S, Boulesteix AL, Moons KGM. [Critical appraisal of artificial intelligence-based prediction models for cardiovascular disease](https://doi.org/10.1093/eurheartj/ehac238). *European Heart Journal* 2022;**43**:2921--2930. </span>

<span class="csl-left-margin">16. </span><span class="csl-right-inline">Hernandez-Suarez DF, Kim Y, Villablanca P, Gupta T, Wiley J, Nieves-Rodriguez BG, Rodriguez-Maldonado J, Feliu Maldonado R, da Luz Sant'Ana I, Sanina C, Cox-Alomar P, Ramakrishna H, Lopez-Candales A, O'Neill WW, Pinto DS, Latib A, Roche-Lima A. [Machine learning prediction models for in-hospital mortality after transcatheter aortic valve replacement](https://doi.org/10.1016/j.jcin.2019.06.013). *JACC: Cardiovascular Interventions* 2019;**12**:1328--1338. </span>

<span class="csl-left-margin">17. </span><span class="csl-right-inline">Collins GS, Reitsma JB, Altman DG, Moons KG. [<span class="nocase">Transparent reporting of a multivariable prediction model for individual prognosis or diagnosis (TRIPOD): the TRIPOD Statement</span>](https://doi.org/10.1186/s12916-014-0241-z). *BMC Medicine* 2015;**13**:1. </span>

<span class="csl-left-margin">18. </span><span class="csl-right-inline">Wynants L, Van Calster B, Collins GS, Riley RD, Heinze G, Schuit E, Albu E, Arshi B, Bellou V, Bonten MMJ, Dahly DL, Damen JA, Debray TPA, Jong VMT de, De Vos M, Dhiman P, Ensor J, Gao S, Haller MC, Harhay MO, Henckaerts L, Heus P, Hoogland J, Hudda M, Jenniskens K, Kammer M, Kreuzberger N, Lohmann A, Levis B, Luijken K, Ma J, Martin GP, McLernon DJ, Navarro CLA, Reitsma JB, Sergeant JC, Shi C, Skoetz N, Smits LJM, Snell KIE, Sperrin M, Spijker R, Steyerberg EW, Takada T, Tzoulaki I, Kuijk SMJ van, Bussel BCT van, Horst ICC van der, Reeve K, Royen FS van, Verbakel JY, Wallisch C, Wilkinson J, Wolff R, Hooft L, Moons KGM, Smeden M van. [Prediction models for diagnosis and prognosis of covid-19: Systematic review and critical appraisal](https://doi.org/10.1136/bmj.m1328). *BMJ* 2020;**369**. </span>

<span class="csl-left-margin">19. </span><span class="csl-right-inline">Andaur Navarro CL, Damen JAA, Takada T, Nijman SWJ, Dhiman P, Ma J, Collins GS, Bajpai R, Riley RD, Moons KGM, Hooft L. [Systematic review finds 'spin' practices and poor reporting standards in studies on machine learning-based prediction models](https://doi.org/10.1016/j.jclinepi.2023.03.024). *Journal of Clinical Epidemiology* 2023;**158**:99--110. </span>

<span class="csl-left-margin">20. </span><span class="csl-right-inline">Dhiman P, Ma J, Andaur Navarro CL, Speich B, Bullock G, Damen JAA, Hooft L, Kirtley S, Riley RD, Van Calster B, Moons KGM, Collins GS. [Risk of bias of prognostic models developed using machine learning: A systematic review in oncology](https://doi.org/10.1186/s41512-022-00126-w). *Diagnostic and Prognostic Research* 2022;**6**:13. </span>

<span class="csl-left-margin">21. </span><span class="csl-right-inline">Sculley D, Holt G, Golovin D, Davydov E, Phillips T, Ebner D, Chaudhary V, Young M, Crespo J-F, Dennison D. [Hidden technical debt in machine learning systems](https://proceedings.neurips.cc/paper_files/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf). Cortes C, Lawrence N, Lee D, Sugiyama M, Garnett R, eds. *Advances in neural information processing systems*. Curran Associates, Inc.; 2015. </span>

<span class="csl-left-margin">22. </span><span class="csl-right-inline">Royen FS van, Moons KGM, Geersing G-J, Smeden M van. [Developing, validating, updating and judging the impact of prognostic models for respiratory diseases](https://doi.org/10.1183/13993003.00250-2022). *European Respiratory Journal* 2022. </span>
