---
layout: page
title: WSL Attendance Demand
description: An empirical estimation of the determinants of demand within English women's football
img: assets/img/Arsenal-WSL.jpg
importance: 1
category: Academic
related_publications: false
---

<div class="row justify-content-center">
    <div class="col-13 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Arsenal-WSL-cropped.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div style="border: 1px solid #ddd; border-radius: 6px; padding: 16px; margin: 16px 0; background-color: #f8f9fa;">
    <p style="font-size: 110%; text-align: center;"><strong><u>Summary</u></strong></p>
    <p style="text-align: center"> This page covers the paper <strong><em> Determinants of Attendance in the English Women's Super League: Does Demand for Men's Football Spillover? </em></strong> which I completed the empirical analysis for and wrote 
    alongside my co-author <a href = "https://www.liverpool.ac.uk/people/juan-de-dios-tena-horrillo">Dr. Juan de Dios Tena Horrillo</a>. This paper has been accepted, and is pending publication, in the <a href = "https://fitpublishing.com/journals/ijsf">International Journal of Sport Finance.</a></p>

    <p style="text-align: center"> Using attendance data from a range of sources, we run a basic ordinary least squares (OLS) regression to uncover what determinats are correlated with the demand for domestic English women's football. We find that a
    range of common determinants, such as the quality of the competing teams and the weather on the day of the match, affects attendance similar to how they do in men's football. We further find that there is a degree
    of demand spillover from the men's team to the women's team and that the success of the English international women's team positively stimulates attendance at domestic women's football. </p><br>

    <p style="font-size: 110%; text-align: center;"><strong><u>Relevant Links</u></strong></p>
    <p>Pre-Publication: <a href="/portfolio-Owen-Croft/assets/pdf/determinants_of_attendance_in_the_English_Womens_Super_league.pdf">PDF link</a></p>
    <p>Replication Package: 🚧 Repository In Progress 🚧</p>
    <br>
    Est. Reading Time: 3-4 Minutes
</div>



<p style = "font-size: 200%"><strong>Background and Motivation</strong></p>

Interest in women's football has surged in recent years, with record breaking audiences and increased media coverage. Particularly, the FA Women's Super League (WSL) has seen a sharp increase in average attendances since the leagues commencement in 2011, as seen below:

<div class="row justify-content-center">
    <div class="col-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Figure 1 - WSL Att Demand.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Despite this, interest in the WSL is still far from its male counterpart, although attendances are now above that of the 4th tier of English professional football. Again, as seen below:

<div class="row justify-content-center">
    <div class="col-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/attendance_across_leagues_1000_600.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

A unique feature of the WSL is the association of women's teams with football clubs traditionally focused on the men's teams - in fact, in the 2022/23 season, all teams within the league were integrated with football club's playing in the men's professional leagues. This integration of the women's teams to the predominantly male football clubs can have a range of benefits for the team, such as improved training facilities and financial resources. However, the focus of our research is whether they also benefit from a brand spillover from the association to a successful football club. 

<p style = "font-size: 200%"><strong>Methodology</strong></p>


Our empirical strategy follows that of previous attendance demand studies, using a <strong>fixed effects regression model</strong> using the match level as the unit of observation. This data is spread across all seasons in the WSL at the time of research, that being the 2011 season up to and inclusive of the 2022/23 season, with the exception of the 2020/21 season due to Covid restrictions on stadium attendance. 

To understand the factors that influence stadium attendance, we employ a range of covariates (independent variables) and regress them on the log of stadium attendance for each match  to measure their impact on demand. Such variables can be grouped into separate categories that are seen frequently in the attendance demand literature, those being economic factors, viewing quality, chracteristics of the sporting event, consumer preferences, and stadium capacity. A full list of the covariates can be seen below. To control for any other unobserved confounders, we also control for the home team, away team, season, day, and month fixed effects.

<div class="row justify-content-center">
    <div class="col-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/List of covariates.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


<p style = "font-size: 200%"><strong>Results</strong></p>

We find that the determinants that shape demand at women's football matches share much of the same characteristics as those shaping demand for men's football. We present the point estimates for the general determinants of demand below, showing that demand is negatively correlated with the distance between competing teams and the weather on the match day, but positively correlated with the quality of the competing teams, derby matches, the foothold the home team has within the league (through the no. of seasons played within that league), and the probability of the home team winning.

<div class="row justify-content-center">
    <div class="col-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Table 1 - Determinants of Attendance.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Moving to the main focus of the study, we review the effect of the men's team success on the demand for women's football. Again, the results can be seen in the table below. Quite interestingly we see that there is a statistically significant relationship between the success of the men's team and the demand for the associated women's teams, with attendance increasing by ~10% for every trophy won by the men's team and a short term boost of ~13% the season after the men's team win a trophy. We also find that demand is affected when there is a conflict of scheduling between men's and women's matches. Turning back to the table above, we see that matches played in the men's home stadium see a significant rise in demand, with matches specially relocated in these stadiums seeing a 167% increase in attendance and matches which are normally played in the men's stadium seeing greater demand by 47%.

<div class="row justify-content-center">
    <div class="col-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Table 2 - Male team spillover.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Finally, we investigate whether the success of the English women's national team has any effect on the demand for domestic women's football. As we included season fixed effects within our regression specification, we can untangle the effect via t-tests. We see the results from such tests below, finding suggestive evidence that attendance sees a large increase following a successful tournament for the Lionesses, though the results aren't consistent. 

<div class="row justify-content-center">
    <div class="col-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/table 3 - intl effect.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<p style = "font-size: 200%"><strong>Conclusion</strong></p>

We find much of our results align with the determinants found to affect attendance for men's football, with performances, derbies, and the probability of the home team winning resenting as significant predictors for stadum attendance. However, our research expands upon previous publications by reviewing any potential spillover effect from the success and demand for the men's side has on the demand for the women's team. Here, we do find evidence of a brand spillover that affects the demand for the women's team, with attendance being stimulated from the number of trophies the men's side won and if they won a trophy in the previous season. We also find that there is a contraction in demand for the women's side when there is a clash in schedules between the two teams. 

Our results gives new strategic insights to football clubs and governing bodies that aim to increase the demand for women's football in England. 