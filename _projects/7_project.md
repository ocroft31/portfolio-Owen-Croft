---
layout: page
title: Racial Bias in Footballer Ratings
description: A replication of a paper reviewing whether journalists' ratings of footballers exhibit a degree of racial bias
img: assets/img/italian newspapers.jpg
importance: 2
category: Academic
related_publications: false
---

<div class="row justify-content-center">
    <div class="col-13 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/italian newspapers cropped.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div style="border: 1px solid #ddd; border-radius: 6px; padding: 16px; margin: 16px 0; background-color: #f8f9fa;">
    <p style="font-size: 110%; text-align: center;"><strong><u>Summary</u></strong></p>
    <p style="text-align: center"> This page covers my dissertation for the fulfillment of my MSc Economics, where I replicate the paper <a href = "https://www.sciencedirect.com/science/article/pii/S0014292121002622">Racial bias in newspaper ratings of professional football players</a>, authored by <a href="https://sites.google.com/view/principefrancesco/">Francesco Principe</a> and <a href="https://sites.google.com/site/homepagejanvanours/">Jan van Ours.</a></p>
    
    <p style="text-align: center"> The replication uses the dataset provided by the authors to validate thier empirical methods and the subsequent results. I find that, given their data, the results presented in the original article are valid, finding that the subjective ratings of black and non-Italian footballers are conditionally lower than that of Italian and non-black players. However, further robustness checks find a handful of improvements and small errors that improve the accuracy of the results, finding that the degree of racial bias is overstated when using a different measure to codify someones race and that the ratings penalty by the newspaper Gazzetta is likely due to a bias for Italian players instead of against black players.</p><br>

    <p style="font-size: 110%; text-align: center;"><strong><u>Relevant Links</u></strong></p>
    <p><strong>Copy of Dissertation: </strong><a href="/portfolio-Owen-Croft/assets/pdf/Owen Croft Dissertation.pdf">PDF link</a></p>
    <p><strong>Replication Package: </strong><a href="https://github.com/ocroft31/Bias-in-Footballer-Ratings---Dissertation-">Bias-in-Footballer-Ratings---Dissertation-</a></p>
    <br>

    <strong>Software Used:</strong> <span class="notion-pill pill-purple">R</span> <span class="notion-pill pill-purple">Stata</span><br>
    <strong>Est. Reading Time: </strong><span class="notion-pill pill-green">6 Minutes</span>
</div>

Here, I will be mainly covering my additions to the original paper and the results I gathered from my analysis. This will involve a review of the results, but I will leave the discussion both for <a href = "https://www.sciencedirect.com/science/article/pii/S0014292121002622">the original paper</a> and my dissertation (which dives deeper into related literature regarding the economics of discrimination, race, and subjective evaluations).

<p style = "font-size: 200%"><strong>Descriptive Analysis</strong></p>

A graphical analysis of the footballer ratings presents alot of interesting information about the presence of bias within the evaluations. In the figure below, we see the kernal densities of the footballer ratings and wages, separated between black and non-black players.


<div class="row justify-content-center">
    <div class="col-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/racial_bias/Kernel Densities - Ratings and wages.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Looking at the graph on the left hand side, we can see a fairly large difference between the densities for black and non-black players, with non-black players having a slightly higher mean rating of 5.78 compared to that of black players (5.69) and black players recieving lower scores at a higher frequency to non-black players. Turning to the right hand side of the graph, we do not see much difference between the distribution of wages between black and non-black players.

We see something similar when we look at the empirical cumulative distribution function of the footballer ratings by newspaper. Again the figure is shown below. Unsurprisingly we see on the average, and for the newspapers Corriere and Tuttosport, there is a larger share of lower ratings for black players when compared to non-black players, with the distributions converging at the higher ratings. However, we also see that the distribution of ratings between black and non-black players is approximately the same for the newspaper Gazzetta, something we see empirically later.

<div class="row justify-content-center">
    <div class="col-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/racial_bias/ECDF.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<p style = "font-size: 200%"><strong>Methodology</strong></p>

The approach to understanding the extent of the racial bias in the footballer ratings is quite simple. We regress a dummy variable, <em>B</em>, indicating whether a player is black, along with a range of controls indicating their performance, personal characteristics, and team and season fixed effects on their end of season average rating across newspapers. If the players ratings were not affcted by a degree of racial bias then we would expect that the parameter estimate for <em>B</em> is statistically equal to 0.

This analysis is expanded by reviewing the effect of the dummy variable <em>B</em> across ratings quintiles. I will not touch on this as it is abit more complicated than analysing the bias on the ratings mean (of course, more detail can be found wihtin the original paper and the dissertation), but the coefficient estiamte has the same interpretation. Finally, we do the same statistical analyses using wages as our dependent variable; however, from the graphical analysis, we do not expect to see much.

<p style = "font-size: 200%"><strong>Results</strong></p>

The results of the main statistical analysis is presented below. Reviewing the first column, we find that, after controlling for a players characteristics and sporting performance, the average rating is 0.085 points lower for black footballers compared to their non-black counterparts, highlighting that the evaluations present a degree of racial bias. This result is consistent across the individual newspapers, with Corriere and TuttoSport having similar coefficient sizes of -0.096 and -0.102 respectively. Finally, there is no evidence of a racial difference between player wages.

<div class="row justify-content-center">
    <div class="col-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/racial_bias/Main results.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Interestingly, when we turn to the remaining columns in the table, we see that the presence of this bias is not consistent across the ratings distribution, instead being focused at the lower 10th and 30th quartiles. Although we are still uncertain why this is the case, it could be suggestive of negative stereotyping on the part of the journalists, associating poor performances to a players race. All of the results found are consistent with the original paper.

<p style = "font-size: 200%"><strong>Robustness Analysis</strong></p>

Both the dissertation and the original article which the dissertation replicates run a range of robustness exercises, but I make some additions which do affect the interpretation of the results.

<p style = "font-size: 125%"><strong>Classification of a Players Race</strong></p>

There is an interesting strand of literature that reviews how race is classified, which is unfortuantely beyond the scope of this summary. However, for our puropse, it does present an important empirical issue - how do we classify a players race? 

The original paper takes the approach of asking four colleague who were unaffiliated with the research to classify the race of all players as either black or non-black. The footballer is then classified as black if at least one of the colleagues said that the player is black. This is a good way of classifying the players race, as it works off of the perceptions of the players race, which is like how the journalists classify race in our study. 

However, classifying a player as black if at least one player as black could theoretically bias results and pick up any sensitivity in an evaluators choice of labelling a player. Due to this, I re-run the analysis outlined above but with different thresholds for a player to be labelled black (e.g two or more etc.). The results are shown below.

<div class="row justify-content-center">
    <div class="col-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/racial_bias/Race Classification Robustness.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Interestingly, we see that the racial bias found by Gazzetta is no longer statistically significant once we use a more restrctive definition of a players race, perhaps indicating that using the definition from the original paper is creating spurious results. We also find that the parameter estimate is not significant when we class a player as black if all four people label the player as black, though we do not put much focus on this result as only 45 players in our sample have all four evaluators labelling the player as black.

<p style = "font-size: 125%"><strong>Subsamples based on nationality</strong></p>

The final sensitivity analysis from the original paper reviews whether racial bias is driven by favouritism towards Italian players. Given only 7 players in the sample are black Italians compared to 81 black non-Italians, there may be a potential influence of Italian favouritism influencing the results. To understand if this is the case, we can re-run our analysis on different samples and using different parameters, shown below. In addition to the analysis done in the original paper, I run the same regression but on the sample of Italian players. Though it would be surprising to find a result given that their are only 7 black Italian players, it is still interesting if we do find something.

<div class="row justify-content-center">
    <div class="col-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/racial_bias/subsamples.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Quite interestingly we do find evidence that the footballer ratings are driven by a degree of Italian favouritism, with Italian players recieving a higher score by 0.038 across all papers, which is higher for ratings by Gazzetta (0.045) and TuttoSport (0.059). When we reduce our sample to that of all non-Italian players, we do find that the ratings penalty for black players still remains across the newspapers apart from Gazzetta. Although this was not particularly highlighted by the original paper, this provides evidence that racial bias in the ratings of black players is not present for Gazzetta, instead we find a spurious result due to the racial imbalance between Italian and non-Italian samples; perhaps showing the importance of such sensitivity tests when conducting such analysis.

<p style = "font-size: 125%"><strong>Errors in the original data</strong></p>

A final addition to the original paper corrects an error that was missed within the analysis. When conducting exploratory data analysis on the provided data, I noticed that some of the ratings for individual papers were accidentally inputted as 0, where they were perhaps just missing values. Although only a small number of observations had this error (seven in the original dataset), if the missing data is correlated with the players rating (perhaps due to playing time or quality) or the players race then the inclusion biases the results. Due to this, I re-run the analysis after dropping he observations with missing data.

<div class="row justify-content-center">
    <div class="col-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/racial_bias/Removing missing data.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The results from this robustness exercise are shown above. Like expected, the results do not change substantially from the original analysis, but the parameter estimates are ~27% smaller, showing that the error is creating biased estimates and is overstating the racial penalty in ratings. 

<p style = "font-size: 200%"><strong>Conclusion</strong></p>

Studying the end of season ratings of footballers by a set of Italian newspapers, we find that black players, on average, recieve lower ratings than their non-black counterparts. Through extensions to our analysis, we find that this bias is mainly present at the lower end of the ratings distribution, and for one of the newspapers, driven by Italian favouritism instead of black prejudice. Although we are unable to properly disentangle the mechanisms behind the results that we find, the presence of the bias at the lower end of the ratings distribution gives suggestive evidence that negative stereotypes of black players being worse footballers may be driving this results; however, much more through research is necessary to confirm this. 

Such results present several implications for workplace management and the effect media has on consumers. First, we suggest the role of media within society presents unique issues from biased evaluations, potentially leading sports newspaper readers to develop adverse preferences against black players, though this effect may be minimal. Within the firm, biased evaluations of employees present issues of fairness and efficiency for the allocation of incentives within a workplace. Such concerns highlight the potential for policy to intervene.

