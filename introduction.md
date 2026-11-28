---
layout: default
---

# Introduction
COVID-19 severity is usually described as a progressive disease: patients move from asymptomatic to mild, moderate, severe and critical state. These categories are assigned by doctors and determine the treatment. However, it is not clear if the molecular signals measured in a patient’s blood correlate with the disease degree of severity. 

Hence, we propose to test whether clinically determined severity is reflected in single-cell RNA-sequencing data. Instead of treating individual cells as the unit of analysis, we look at donors: by pseudobulking each donor’s cells within a given cell type, we build one expression profile per donor and cell type and ask what these profiles say about the patient.

This website will first walk you through how donor profiles are constructed and whether clinical severity emerges from them. Subsequently, we examine whether severity is better described as a continuous gradient or as a series of discrete stages. Finally, we show where clinical labels and RNA-sequencing data agree, where they diverge and why these findings matter in defining the COVID-19 phase.
 
<img src="https://c.pxhere.com/images/0d/85/a5167ad80e545a7bae4572f1c344-1608792.jpg!d" srcset="https://c.pxhere.com/images/0d/85/a5167ad80e545a7bae4572f1c344-1608792.jpg!d" alt="covid 19, coronavirus, covid, cellule, pandemic, corona virus, rouge, organisme, plante, Art fractal, pollen, textile, fleur, symétrie, art, Images Gratuites In PxHere">

# Research Questions
<div style="display: flex; gap: 20px;">
    <a href="aim1.md" style="color: black; ; background-color:  #c1ddf8; padding: 10px; text-align: center; border-radius: 15px;">
        <strong style="font-size: 24px;"> Aim 1 </strong> .<br>
        Does clinically defined severity emerge from donor profiles? Where do profiles support or contradict the assigned clinical severity, and which cell types are most informative for separating particular severity groups?
    </a>
      <a href="aim2.md" style="color: black;  background-color:  #c1ddf8; padding: 10px; text-align: center; border-radius: 15px;">
        <strong style="font-size: 24px;"> Aim 2 </strong> .<br>
        Is severity better modelled as a continuous gradient or as discrete stages? Where are neighbouring severities clearly separated, and where do they overlap, and which cell types change smoothly versus sharply between particular severity groups?
    </a>

</div>





# Exploring the data and preprocessing

Before diving into our aims, we need first to establish how versatile our data collection is. For this reason we explore the data and perform some preprocessing and filtering in order to keep only those we are interested in.

## Exploration
We assess the data in order to determine if the gender, age interval or the collection site influence  the Covid-19 status and severity. Our result could be summarized as follows: 

![Sample distribution in relation to gender, age interval and site of collection](images/Covid_status.png)

In the first histogram we can see that the gender is relatively balanced in the data set including the distribution of the groups studied (e.g. Healthy, LPS, etc.). 

The second histogram shows the sample distribution across ages. We can clearly see that the healthy donors were in the younger age groups with LPS group present only in the first two age groups (20 to 39). From age 80, only Covid cases are present.

The third histogram displays the unequal distribution in the number of samples between the regions. In London, there is roughly 6 time less samples than in Camberage and 7 times less samples than in Newcastel. We can immediately see that the majority of samples come from the Covid-19 patient in all the 3 sites. However, Newcastel is the only one where the two control samples were collected (Non-covid and LPS).


![Severity stages representation across the gender, age interval and site of collection](images/Stage_severity_according_age_gendre_region.png)

The gender histogram shows that the major differences are in the distribution of Mild and Moderate cases. Namely, in female group there are two times more Mild cases, while the male group contains three times more of Moderate cases.

The age histogram shows an unequal distribution of cases according to the disease severity. In younger age (20 to 39) and old groups (80-99) there are no Critical cases.

The collection sites contribute differently in terms of disease severity. As observed previously, London site took into account only the Covid-19 manifested patients, hence the total lack of the Asymptomatic group. The Cambridge site has the equally represented all disease stages. 

![Exploring cell-type composition across groups and disease severity](images/Mean_cell_type_for_all_stages.png)

The 10 most abundant cell types account for approximately 75% of the mean cell-type composition across all groups and disease severities.

Differences in cell-type composition can be observed between groups. The LPS group shows a higher proportion of naive B cells, while CD16+ NK cells are more abundant in both the LPS and non-COVID-19 groups.

A particularly interesting pattern emerges among the less frequently detected cell types. Cell types present in 20% or fewer of the samples are exclusively observed in donors with critical COVID-19. Although detected in relatively few samples, these populations collectively account for more than 5% of the mean cell-type composition in this group.

These rare populations include B-cell malignancies, T helper 17 (Th17) cells and cells associated with the megakaryocyte lineage.



## Prepossessing