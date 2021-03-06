---
layout: default
title: Data Normalization
nav_order: 6
---

# Data Normalization
One last thing we need to do is control for any confounding factors.  For example, the DAs are different sizes.  To get a better sense of green vegetation per DA, we will Normalize the Green Vegetation area by the Shape Area of the DAs.

## Adding a New Field
Add a Field called Green_Vegetation_Fraction.
* Give it the alias Green Vegetation Fraction.
* Make sure its type is: double.

## Normalizing
Now we can Normalize the total area of green vegetation by DA size.  Normalizing, also know as standardizing, is the process of dividing one variable by another correlated variable to account for their relationship.  It can help us identify patterns that might be masked by a confounding variable.

**1)** Calculate the Green Vegetation Fraction field.
* The Field Calculator allows you to do more than just set values like we did in the last step.  We can also create multivariate expressions.
* Divide SUM_Green_Veg_Area (yours might have a slightly different name) by the Shape_Area.
* This will give us the percentage of the DA that is covered by Dense Green Vegetation.

<div style="overflow: hidden;
  padding-top: 56.25%;
  position: relative">
  <iframe src="Norm.mp4" title="Processes" scrolling="no" frameborder="0"
    style="border: 0;
   height: 100%;
   left: 0;
   position: absolute;
   top: 0;
   width: 100%;">
   <p>Your browser does not support iframes.</p>
 </iframe>
</div>
<a href="Norm.mp4" target="_blank">View Image in New Tab</a>

## Question 13)
What does data normalization do? How does normalizing effect the relationship with income? Create a new chart with Green Vegetation Fraction on the X-axis and Income on the Y-axis to find out.  How does this compare to when we were looking at the relationship between Total Green Vegetation Area and income?

<!-- Normalizing accounts for a confounding/secondary/other variable by dividing the variable of interest by the confounder.  This helps control for correlation between the two variables. The R2 score goes up to 0.073, Accounting for the different sizes of the DA "improves" the relationship. But not by much -->
