# Analysis and Scripts Description

## Data Annotation and Analysis Methods 

Data Annotation and Metadata
For the FUN-1 staining data, FCS files were imported into R using the Flow Core package. The Attune generated file names contain a few common phrases that hinder the
interpretation of the graphs. Thus, the longest substring function from the PTXQC package was used to remove the common phrases in the file names, while the unique sample labels were
kept intact. The FCS files were then separated into species. The write.table function was used to write wrangled data into .tsv files.

For the FungaLight data, event count within the live population gate, total events, and CFU counts were written into a table using the Cbind function. Variables of interest such as
“percent live” were added into the table. Specifically, percent live variable was calculated as (events in live population gate) / (total events). CFU Survival was calculated as (colonies in treatment condition) / (colonies in mock treated).

Data Analysis
Data Graphing
Data was graphed using R packages ggplot2, ggcyto, and ggridges. Graph size, axes, and order of experimental conditions were adjusted as needed. The intensity (height) of BL1
(green), BL2 (red), and FSC channel are graphed separately in the FUN-1 flow cytometry panels (Fig. 1A, Fig. 1B). The mean intensity of BL1 and BL2 were calculated and graphed as
independent variables. The CFU survival was graphed as the dependent variable (Fig. 1C, Fig.1D). A two-way scatter plot was generated.
Fore FungaLight data, percent live was graphed as the independent variable and the CFU survival rate was graphed as a dependent variable. A two-way scatterplot was generated.
Colors of data points indicate different H2O2 treatment conditions.

Statistical Analysis
Data analysis in Fig. 1C and Fig. 1D was done using a linear regression model and the LM function in base R. The adjusted R-squared value was calculated for the corresponding
variables and reported in the graph. In Fig. 1E, outliers due to documented technical errors or arbitrary settings are filtered
out of analysis. The linear regression model function was used to build a model where Y is the CFU survival rate and X is the percent gated for each population. The predicted linear
regression line is then added onto the scatter plot. The adjusted R-squared values and p-value was also reported in the graph.

## Script File Correspondance

Each script file is in both R markdown and HTML format. Each script corresponds to a figure panel in the output folder. The correspondance is as following:

Panel A - FUN1 Live vs Heated.html
Panel B - FUN1-H2O2-Treated.html
Panel C & Panel D - FUN1 H2O2 vs CFU.html 
Panel E - Fungalight-Plotting.html

