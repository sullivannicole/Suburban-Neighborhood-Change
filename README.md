# Suburban Neighborhood Change

## Background

The Suburban Neighborhood Change project is a [Metropolitan Council](https://metrocouncil.org) initiative to identify communities that are changing in similar ways, for similar reasons.  In connecting communities that are experiencing like patterns of transition, we hope to provide them with better resources and enhance our regional cohesion from the bottom-up.

## The Variables

The variables used in this analysis were (unless listed otherwise, the source of data is American Community Survey):

* Median household income (imputed where missing)
* % Race (disaggregated by groups)
* % Aged 65+
* % Aged 18 & under
* Median home value (imputed where missing)
* Median gross rent (imputed where missing)
* % Renters
* Total housing units (Met Council estimate)
* % limited English proficiency (disaggregated by largest groups in region)
* % concentration of poverty (185% below Federal Poverty Line)
* Average household size
* Population (Met Council estimate)
* % households residing in mobile homes

## The Timeframe

The timepoints examined were 2000, 2010, and 2017.  While American Community Survey (ACS) data is available for years between 2010 and 2017 and some years prior to 2010, we chose to examine these three time points specifically to remove small variations that occurred over time and instead emphasize the larger trends that were occurring in these decades.

## KML:  The Cluster Algorithm

This project used a form of unsupervised machine learning called clustering, in which observations are classified into groups based on their distances from one another.  The form of clustering used in our analysis, known as KML, is shape-respecting; that is, if observations are changing in much the same ways, but in different magnitudes, the algorithm will favor those observations with similar magnitudes (i.e. shapes).  This means that slightly staggered changes of the same shape (for example, a tract rapidly increasing in total housing units and decreasing in their % aged 65+, but starting in different years) will be classified together.

This is in contrast to other time-series clustering methods (such as PROC FASTCLUS in SAS) that favor changes that are temporally cyclical (called "dynamically evolving systems"), such as seasonal variations in weather, or annual variations in gas prices.  Proc Fastclus clustering is most effectively used to define *stages* of change, rather than to define *groups* experiencing similar changes over time.  Although it is possible to combine it with change variables in order to isolate groups experiencing different trajectories in the same time period, staggered changes are less likely to be classified as similar.

## Opening the Black Box:  Reverse-engineering the Clusters with a Multinomial Logit Model

After clustering, it was important to our users to know how we obtained the clusters we did - what were the driving variables, and driving changes?  In order to answer this question, we "reverse-engineered" our clusters.  Similar to physical reverse engineering, in which one starts with the end-product, and duplicates it without the aid of any drawings or instructions, we started with our clusters and then used all of our variables as predictors of those clusters.  The outputs of the multinomial logit model are *probabilities*; using these probabilities, we can test new data against the model and see how an increase or decrease in a particular variable (or an interaction with another variable), or an increase or decrease in the *change* of that variable affects the probability of that tract being classified in a particular cluster.

## Who We Are

The Met Council is the [Minneapolis-St. Paul metropolitan planning organization (MPO)](https://metrocouncil.org/About-Us/The-Council-Who-We-Are.aspx), a type of federally-mandated agency that exists to serve the region with its long-range planning for transportation, economic development, environmental preservation, and more.

## Reproducing the Project

All libraries needed are imported in the import code chunk.  Note that it's possible to reproduce creation of the Census Bureau's American Community Survey (ACS) 'percent new builds' variable from full ACS data using the commented out code chunk.  The full ACS dataset exceeds GitHub's storage limit and is therefore not available here.

## Contributors

* Dennis Farmer - **Initial work**
* Paul Hanson - **Initial work (GIS)**
* Nicole Sullivan - **Contributor**
* Elizabeth Roten - **Contributor**
* Katie Jolly - **Contributor**
* Barış Gumus-Dawes - **Project Manager**