# Red Wine Quality - Project Description

In this project I analyse a dataset containing different chemical properties that can influence the quality of red wine. 
I perform exploratory analysis using `R` on the data and calculate correlations to decide what factors can influence the quality of red wine the most.

***

### Files in this directory

1. The dataset I use is `wineQualityReds.csv` and you can find it from [here](https://github.com/Nazaniiin/EDA_ExploratoryDataAnalysis/blob/master/Red_Wine_Quality/wineQualityReds.csv)

2. The `EDA_RedWineQuality.rmd` file that contains all the code, plots and thorough description of my analysis.

3. The `EDA_RedWineQuality.pdf` and `EDA_RedWineQuality.html` contain the plots and descriptions without code snippets. If you
   wish to go through my analysis without having to deal with the code, these either of these files can be your choice.
   
4. `Figures` directory contains all the plots used throughout the analysis

5. `RedWine_Database_Description.txt` has detailed information about the variables in the dataset. You can find this information in this README file as well.

***

### Variables in the Dataset

This dataset is public available for research. The details are described in [Cortez et al., 2009]. 

  P. Cortez, A. Cerdeira, F. Almeida, T. Matos and J. Reis. 
  Modeling wine preferences by data mining from physicochemical properties.
  In Decision Support Systems, Elsevier, 47(4):547-553. ISSN: 0167-9236.

  Available at: [@Elsevier] http://dx.doi.org/10.1016/j.dss.2009.05.016
                [Pre-press (pdf)] http://www3.dsi.uminho.pt/pcortez/winequality09.pdf
                [bib] http://www3.dsi.uminho.pt/pcortez/dss09.bib

1. Title: Wine Quality 

2. Sources
   Created by: Paulo Cortez (Univ. Minho), Antonio Cerdeira, Fernando Almeida, Telmo Matos and Jose Reis (CVRVV) @ 2009
   
3. Past Usage:

  P. Cortez, A. Cerdeira, F. Almeida, T. Matos and J. Reis. 
  Modeling wine preferences by data mining from physicochemical properties.
  In Decision Support Systems, Elsevier, 47(4):547-553. ISSN: 0167-9236.

  In the above reference, two datasets were created, using red and white wine samples.
  The inputs include objective tests (e.g. PH values) and the output is based on sensory data
  (median of at least 3 evaluations made by wine experts). Each expert graded the wine quality 
  between 0 (very bad) and 10 (very excellent). Several data mining methods were applied to model
  these datasets under a regression approach. The support vector machine model achieved the
  best results. Several metrics were computed: MAD, confusion matrix for a fixed error tolerance (T),
  etc. Also, we plot the relative importances of the input variables (as measured by a sensitivity
  analysis procedure).
 
4. Relevant Information:

   The two datasets are related to red and white variants of the Portuguese "Vinho Verde" wine.
   For more details, consult: http://www.vinhoverde.pt/en/ or the reference [Cortez et al., 2009].
   Due to privacy and logistic issues, only physicochemical (inputs) and sensory (the output) variables 
   are available (e.g. there is no data about grape types, wine brand, wine selling price, etc.).

   These datasets can be viewed as classification or regression tasks.
   The classes are ordered and not balanced (e.g. there are munch more normal wines than
   excellent or poor ones). Outlier detection algorithms could be used to detect the few excellent
   or poor wines. Also, we are not sure if all input variables are relevant. So
   it could be interesting to test feature selection methods. 

5. Number of Instances: red wine - 1599; white wine - 4898. 

6. Number of Attributes: 11 + output attribute
  
   Note: several of the attributes may be correlated, thus it makes sense to apply some sort of
   feature selection.

7. Attribute information:

   For more information, read [Cortez et al., 2009].

   Input variables (based on physicochemical tests):
   1 - fixed acidity (tartaric acid - g / dm^3)
   2 - volatile acidity (acetic acid - g / dm^3)
   3 - citric acid (g / dm^3)
   4 - residual sugar (g / dm^3)
   5 - chlorides (sodium chloride - g / dm^3
   6 - free sulfur dioxide (mg / dm^3)
   7 - total sulfur dioxide (mg / dm^3)
   8 - density (g / cm^3)
   9 - pH
   10 - sulphates (potassium sulphate - g / dm3)
   11 - alcohol (% by volume)
   Output variable (based on sensory data): 
   12 - quality (score between 0 and 10)

8. Missing Attribute Values: None

9. Description of attributes:

   - fixed acidity: most acids involved with wine or fixed or nonvolatile (do not evaporate readily)
   - volatile acidity: the amount of acetic acid in wine, which at too high of levels can lead to an unpleasant, vinegar taste
   - citric acid: found in small quantities, citric acid can add 'freshness' and flavor to wines
   - residual sugar: the amount of sugar remaining after fermentation stops, it's rare to find wines with less than 1 gram/liter and wines with greater than 45 grams/liter are considered sweet
   - chlorides: the amount of salt in the wine
   - free sulfur dioxide: the free form of SO2 exists in equilibrium between molecular SO2 (as a dissolved gas) and bisulfite ion; it prevents microbial growth and the oxidation of wine
   - total sulfur dioxide: amount of free and bound forms of S02; in low concentrations, SO2 is mostly undetectable in wine, but at free SO2 concentrations over 50 ppm, SO2 becomes evident in the nose and taste of wine
   - density: the density of water is close to that of water depending on the percent alcohol and sugar content
   - pH: describes how acidic or basic a wine is on a scale from 0 (very acidic) to 14 (very basic); most wines are between 3-4 on the pH scale
   - sulphates: a wine additive which can contribute to sulfur dioxide gas (S02) levels, wich acts as an antimicrobial and antioxidant
   - alcohol: the percent alcohol content of the wine

   Output variable (based on sensory data): 
   - quality (score between 0 and 10)
