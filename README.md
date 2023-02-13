# Developing a flow cytometry based viability assay for post-oxidative stress survival in yeast species

## Introduction
Yeasts display an acquired stress resistance (ASR) response where a mild dose of primary stress helps the cells to survive a secondary dose of severe stress. The mild primary stress may be the same or different from the secondary severe stress. The overall goal of the project is to understand ASR traits in evolutionary related yeasts species. Specifically, previous work in the lab has identified an increased magnitude of ASR response in C. glabrata when exposed to phosphate starvation as a primary stress and hydrogen peroxide treatment as a secondary stress. This increased magnitude of ASR is not seen in the closely related S. cerevisiae. Downstream investigations suggest the ASR phenotype is closely related to the nutrient sensing TOR pathway.

Motivated by these previous discoveries, the current project seeks to understand the evolutionary trajectory of ASR. While C. glabrata and S. cerevisiae are closely related, the magnitude of their ASR phenotype does not provide information on the ancestral state of the trait. Therefore, the magnitude of ASR in an evolutionarily related outgroup species needs to be accessed and compared. Accessing ASR in multiple species requires a high-throughput method and data analysis pipeline.

The post-oxidative stress survival rate in ASR is traditionally accessed using the gold standard colony forming units (CFU) assay. CFU assay is labor intensive and the small sample plated may induce variance in the output. In addition, CFU assay only gauges cell viability and depends on cells’ ability to proliferate on an agar plate. The hallmark of cell death in yeast is the permanent loss of membrane permeability. CFU assay cannot reliably access this hallmark of death.

My project aims to develop a flow cytometry based high-throughput viability assay using yeast viability dyes. The specific viability dyes used include FUN-1, Fungalite 1, and Fungalite 2. FUN-1 and its analogs are transported from cytosol to the vacuole in metabolically active yeast. The stains then give rise to the formation of CIVS structures in the vacuoles of metabolically active cells. The CIVS emits bright, concentrated red fluorescence. Dead and permeabilized cells do take up the dye. Proteins and nucleic acids in dead, permeabilized cells stain brightly and have a broad ﬂuorescence emission spectrum. They show appreciable signals in both the green and red regions of the spectrum. This is because free thiols of proteins and peptides may react spontaneously with FUN-1 stain, generating red-ﬂuorescence in permeabilized cells. Fungalite 1 and Fungalite 2 are membrane permeability based dyes where the red-fluorescent nucleic acid stain, propidium iodide, stains dead cells with compromised cell membrane.

In this bioinformatics course project, I hope to build a pipeline for processing and analyzing flow cytometry based FCS data and use R to construct informative figures that help in evaluating the results. FCS stands for Flow Cytometry Standard, and it provides a standard format for flow cytometer output across different machine brands and models. FCS is a binary file with three major segments. A header segment records instrument settings and keywords, a data segment, and an analysis segment. The data segment contains all recorded parameters for each event in flow cytometry.

## Figure
![Figure 1](/space/htang5/Documents/FUN1_data_analysis/goal_figure.png)
Figure 1. Ridges plot for flow cytometry results in post-oxidative stress yeast cells. Intensity of the FSC, BLH1, and BLH2 channels are recorded. FUN-1 fluorescence level appears to be altered after different H2O2 treatments.

An example of the figure I want to generate is the ridge plot. This figure has species and experimental conditions on the y-axis. The intensity of flow cytometer channels are on the x-axis. The figure shows low FUN-1 fluorescence in mock treated cells, high fluorescence in stock concentration [H2O2] treated cells, and some potential shifts in the intermediate [H2O2] conditions. Using this figure, I hope to compare fluorescence level of FUN-1 stained post-oxidative stress cells, and eventually decide if FUN-1 is useful for reliability accessing viability. 

## Materials and Methods
1. Post-oxidative stress yeast cells were collected and stained with FUN-1 or Fungalite dyes. (See ELN on specific collection protocol).
2. Stained cells were run through Attune flow cytometry. Settings in ELN. Data have been collected by me and are FCS files, with one file for each experimental condition.
3. To generate figures, FCS files need to be imported in R with file names shortened by removing common phrases.
4. Each species’ data need to be linked to its metadata.
5. Use “flow core” package to read FCS files.
6. Generate graph using ggplot2, ggcyto, and ggridges.
7. Adjust graph axes and change order of experimental conditions as needed.

## Reference
David B. Berry,Qiaoning Guan,James Hose,Suraiya Haroon,Marinella Gebbia,Lawrence E. Heisler,Corey Nislow,Guri Giaever,Audrey P. Gasch. “Multiple Means to the Same End: The Genetic Basis of Acquired Stress Resistance in Yeast.” PLOS Genetics, November 10, 2011
https://doi.org/10.1371/journal.pgen.1002353


