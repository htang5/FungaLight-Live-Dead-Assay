# Developing a flow cytometry based viability assay for post-oxidative stress survival in yeast species

## Introduction
Yeasts display an acquired stress resistance (ASR) response where a mild dose of primary stress helps the cells to survive a secondary dose of severe stress. The mild primary stress may be the same or different from the secondary severe stress. The overall goal of the project is to understand ASR traits in evolutionary related yeasts species. Specifically, previous work in the lab has identified an increased magnitude of ASR response in C. glabrata when exposed to phosphate starvation as a primary stress and hydrogen peroxide treatment as a secondary stress. This increased magnitude of ASR is not seen in the closely related S. cerevisiae. Downstream investigations suggest the ASR phenotype is closely related to the nutrient sensing TOR pathway.

Motivated by these previous discoveries, the current project seeks to understand the evolutionary trajectory of ASR. While C. glabrata and S. cerevisiae are closely related, the magnitude of their ASR phenotype does not provide information on the ancestral state of the trait. Therefore, the magnitude of ASR in an evolutionarily related outgroup species needs to be accessed and compared. Accessing ASR in multiple species requires a high-throughput method and data analysis pipeline.

The post-oxidative stress survival rate in ASR is traditionally accessed using the gold standard colony forming units (CFU) assay. CFU assay is labor intensive and the small sample plated may induce variance in the output. In addition, CFU assay only gauges cell viability and depends on cells’ ability to proliferate on an agar plate. The hallmark of cell death in yeast is the permanent loss of membrane permeability. CFU assay cannot reliably access this hallmark of death.

My project aims to develop a flow cytometry based high-throughput viability assay using yeast viability dyes. The specific viability dyes used include FUN-1, Fungalite 1, and Fungalite 2. FUN-1 and its analogs are transported from cytosol to the vacuole in metabolically active yeast. The stains then give rise to the formation of CIVS structures in the vacuoles of metabolically active cells. The CIVS emits bright, concentrated red fluorescence. Dead and permeabilized cells do take up the dye. Proteins and nucleic acids in dead, permeabilized cells stain brightly and have a broad ﬂuorescence emission spectrum. They show appreciable signals in both the green and red regions of the spectrum. This is because free thiols of proteins and peptides may react spontaneously with FUN-1 stain, generating red-ﬂuorescence in permeabilized cells. Fungalite 1 and Fungalite 2 are membrane permeability based dyes where the red-fluorescent nucleic acid stain, propidium iodide, stains dead cells with compromised cell membrane. If this high throughput flow cytometry based viability assay can be well estabilshed and verified as a CFU replacement, then it could increase the work flow and allow efficient examination of post-oxidative stress survival in multiple yeast species. By applying this method to various evolutionarily related yeast species and comparing the magnitude of ASR in these species, we can gain insights regarding the evolution trajectory of the ASR trait.  

In this bioinformatics course project, I hope to build a pipeline for processing and analyzing flow cytometry based FCS data and use R to construct informative figures that help in evaluating the results. FCS stands for Flow Cytometry Standard, and it provides a standard format for flow cytometer output across different machine brands and models. FCS is a binary file with three major segments. A header segment records instrument settings and keywords, a data segment, and an analysis segment. The data segment contains all recorded parameters for each event in flow cytometry.

## Materials and Methods
**Data**
Data for analysis is obtained through my own experimental work. The data is stored on the lab RDSS drive. I have copied and pasted the data folder through the GUI. The folder is titled with experiment date and each FCS file is labeled with experimental conditions. These labels were generated during the experiment. If you would like to recieve a copy of the data, please contact me at hanxi-tang@uiowa.edu.

**Methods**
*Experimental Techniques* Post-oxidative stress yeast cells were collected and stained with FUN-1 or Fungalight viability dyes (detailed experimental protocols are avaliable upon request). Stained cells were run through Attune flow cytometry. Two filter settings,the seperate red and green setting and the long pass filter setting, were applied in the FUN1 experiment. A single filter setting was applied in the Fungalite experiment. Data was exported in forms of FCS files through Attune's interface and stored on a shared RDSS drive. For Fungalight flow cytometry experiments, an additional set of CFU assays were also conducted and data was appended to the corresponding flow cytometry data.

*Data Annotation and Metadata* For the FUN1 staining data, FCS files are imported in R. The Attune generated file names have a few common phrases that hinder the interpretation of the graphs. Thus,the longest substring function from the PTXQC package is used to remove the common phrases in the file names, while the unique sample labels are kept intact. The write.table function is used to write data into .tsv files and thus linking it to its metadata.
For the Fungalite data, cell populations are gated on the Attune software based on its fluorescence intensity. Cells with low green and low red fluorescence is gated in the "unstained" gate. Cells with high green but low red is gated in the "live" gate. Cells with high green and high red is gated in the "dead" gate. Cell count within each gate is exported from Attune software. Cell counts for each condition is correlated with their CFU count in Excel.

*Graphing* In order to analyze the FUN1 staining data, the “flow core” package from Bioconductor is installed and used to read the FCS files. All needed packages need to be loaded before analysis is run. The goal graph is generated  using ggplot2, ggcyto, and ggridges. Graph axes and order of experimental conditions are adjusted as needed. The intensity (height) of BLH1 (green), BLH2 (red), and FSC channel are graphed seperately in the FUN1 seperate red and green setting. The intensity (height) of the BLH2 and the FSC channels are graphed seperately in the FUN1 long pass filter setting.
When graphing the Fungalite data, a percent variable was generated for each cell population using the equation: percentage = cell count in the population / total cell count. The percent variable is graphed on the x-axis and the CFU survival rate was graphed on the y-axis. A scatterplot was generated. Color of data points indicates different treatment conditions.

*Statistical Analysis* After previous graphing, Fungalite appeared to have superior distinguishing power in predicting CFU survival results. Therefore, data analysis was focused on Fungalite results. Outliers due to documented technical errors or arbituary settings are filtered out of analysis. The linear regression model function was used to build a model where Y is the CFU survival rate and X is the percent gated for each population. The predcited linear regression line is then added onto the scatter plot. The next step in statistical analysis would be to add multiple variables to the model in order to increase the predicting power.

## Results and Discussion
**Figure 1**

![Figure 1](/space/htang5/Documents/FUN1_data_analysis/biol-4386-course-project-htang5/Output/Final_Figure.jpg)

Figure 1. Analysis of flow cytometry results from yeast samples stained with viability dyes. (A) Ridges plots for flow cytometry of FUN-1 stained post heat stress yeasts. Sample names
indicating yeast species and treatment conditions are shown on the vertical axis. Intensity of FSC, FUN-1 Green and FUN-1 Red channels are plotted on the horizontal axis. (B) Ridges
plots for flow cytometry of FUN-1 stained post-oxidative stress yeasts. Sample names indicating yeast species and treatment conditions are shown on the vertical axis. Intensity of FSC, FUN-1
Green and FUN-1 Red channels are plotted on the horizontal axis. (C) Scatter plot of FUN-1 stained post-oxidative stress C. glabrata cells’ mean green fluorescence and CFU survival rate.
Adjusted R-squared value is shown. (D) Scatter plot of FUN-1 stained post-oxidative stress C. glabrata cells’ mean red fluorescence and CFU survival rate. Adjusted R-squared value is
shown. (E) Scatter plot of FungaLight stained post-oxidative stress C. glabrata. The flow cytometry result was gated by population. Percentage of live population is plotted against CFU
survival rate. The line of best fit (blue) from a linear regression model and its 95% confidence intervals (shades) are also graphed. Adjusted R2 and p-value are shown. Colors depict various treatment conditions.

This project aims to develop a flow cytometry based high throughput yeast viability assay and verify its accuracy against the gold standard CFU assay, and thereby provide a
method to potentially quantify the magnitude of ASR trait in various species. The initial approach to this method development utilized the FUN-1 vitality dye. FUN-1
distinguishes live and severe heat killed yeast cells in C. glabrata, S. cerevisiae, and K. lactis (Fig. 1A). Mock treated cells show a spectrum of low fluorescence signals in both the FUN-1
green (0~103) and the FUN-1 red channels (0~102). Heat killed cells show high intensity fluorescence in the green (above 103) and red channels (above 102). The live and dead cell
fluorescence patterns are distinct from each other. In this staining process, live cells were stained with the dye and actively transported the dye to form CVIS structure in its vacuole. Heat
killed cells are unable to actively transport and metabolize FUN-1. Therefore, FUN-1 diffused into heat killed cells are accumulating and emits bright green and red fluorescence. It is clear
that FUN-1 is capable of distinguishing live and heat killed yeasts in flow cytometry. FUN-1 is also capable of distinguishing live and severe hydrogen peroxide treated cells
in C. glabrata, S. cerevisiae, and K. lactis (Fig. 1B). Mock treated cells gave low signals in both the red and green channels. Yeasts treated with severe oxidative stress (1M H 2O2) show high
intensity fluorescence in the green (above 103) and red channels (above 102). However, in yeasts treated with mild oxidative stress (0.1mM-1mM H2O2), the staining pattern is similar to
mock treated cells. Severe oxidative stress is known to immediately kill yeasts. Yeasts treated with a high concentration of H2O2 will become immediately metabolically inactive, and passively
accumulate FUN-1 dye. In mild oxidative stress treated conditions, the reactive oxygen species level remain low and do not cause threat to survival. The yeasts remain metabolically active in
these mild treatment conditions, and actively metabolize FUN-1 to give low florescence in both channels. These data indicates that FUN-1 is capable of distinguishing live and severe oxidative
stress treated yeasts.

FUN-1’s post-oxidative stress survival prediction power was compared to the traditional CFU assays. C. glabrata was exposed to a range of various oxidative stress (0-1M H2O2), then
stained with FUN-1 and also plated for CFU. The mean fluorescence signals is then plotted against CFU survival rate (Fig. 1C, Fig.1D). The mean green fluorescence level is clustered
around 0-5000 for a varied range (0%-100%) of CFU survival rates. The mean red fluorescence level is clustered around 0-1000 for a varied range (0%-100%) of CFU survival rates. The
adjusted R2 values are all around 5% for both correlations. These results suggest that FUN-1 staining is not as sensitive as CFU in assessing post-oxidative stress survival. FUN-1 cannot
distinguish intermediate levels of post-oxidative stress survival.

A yeasts cell death assessment dye, FungaLight, was then used to develop the flow cytometry assay (Fig. 1E). In this approach, C. glabrata was exposed to a range of various
oxidative stress (0-1M H2O2), then stained with FungaLight and also plated for CFU. In intermediate H2O2 treated conditions, FungaLight stained cells separate into clear live and
dead populations with distinct staining patterns (graph not shown here, FCS files available in repository). The live cell population was gated based on staining patterns of mock treated cells.
The percentages of live cells correlate strongly with CFU survival rates in various post-oxidative stress conditions. With an adjusted R2 value of 86%, FungaLight flow cytometry data can be
used as a good predictor of CFU survival rate.Comparing the two dyes, FungaLight is a superior option for developing this flow
cytometry based viability assay. Even though FungaLight as been used as a method of verification in previous papers, a pure flow cytometry based viability have not been established.
This project aims at developing such assay and verifying its prediction power against the CFU assays.

Even though the current data showed FungaLight’s prediction power in post-oxidative stress C. glabrata, FungaLight’s usage in other yeasts species have not yet been explored. A
plausible next step is to establish FungaLight’s usage in other yeasts, and verify its prediction power against CFU survival results. In addition, FungaLight’s prediction power may be further
improved by using an alternative survival assessment timepoint. Yeasts membrane integrity is further compromised at 24 hour post oxidative stress treatment. Therefore, an incubation may
help in improving FungaLight’s accuracy and sensitivity. However, the incubation timepoints and incubation media need to be carefully chosen.

## Reference
David B. Berry,Qiaoning Guan,James Hose,Suraiya Haroon,Marinella Gebbia,Lawrence E. Heisler,Corey Nislow,Guri Giaever,Audrey P. Gasch. “Multiple Means to the Same End: The Genetic Basis of Acquired Stress Resistance in Yeast.” PLOS Genetics, November 10, 2011
https://doi.org/10.1371/journal.pgen.1002353

Rego, A., Ribeiro, A., Côrte-Real, M. et al. “Monitoring yeast regulated cell death: trespassing the point of no return to loss of plasma membrane integrity.” Apoptosis, July 07,
2022. https://doi.org/10.1007/s10495-022-01748-7


