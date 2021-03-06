Kidney Transplant Risk Calculator
=======================================

Task
-------------------
- DATA3888 Capstone Project **Report Only**
 - [Shiny App repo repo](https://github.com/alexwong23/DATA3888-Project-ShinyApp "Shiny App repo")
- Mar 2020 - May 2020

Background / Motivation
-------------------
Kidney failure is the final stage of renal disease and poses a major threat to the body as the excretory system fails to function properly. To combat kidney failure patients can choose two forms of treatment in terms of medical intervention; renal dialysis or organ transplantation. While organ transplantation is greatly preferred, kidney organ allocation has posed itself as a major resource allocation problem. Donors and patients need to be matched effectively and accurately to each other to not only preserve the life of the patient but also, maximise functionality of these limited kidney organs.

With this problem in mind, we developed a tool to aid in the effective and accurate allocation of donor organs to their respective patients. The developed risk calculator will assist practitioners in their decision making and shall even in- form the prescriptions for immunosuppressive drugs. The risk calculator was developed with the intention that it would be used in a clinical setting where shared decision making is implemented. According to Gordan (2013), shared decision making promotes patient centered care. It permits the integration of the nephrologist’s expertise on renal allograft dysfunction with the patient’s values and beliefs concerning future treatment. Within this clinical setting, we hope that the risk calculator provides an opportunity of discussion that concerns the nature of treatment prior to, during and post organ transplantation.

Description
-------------------
The Risk Calculator has 3 different components, and some of them have a very long computation time to process the data and create models. To avoid excessive time in compiling a single PDF, we have decided to put the code onto three separate Rmd files, each representing the code used for data processing and model selection involved for each component of the product (e.g. “Part1.Rmd” etc.).

Take note, the data folder has been 'git ignored' as it was too big to upload - approximately 1GB of raw datasets taken from GEO - Gene Expression Omnibus.

Please also note that since the PDF does not have direct access to the R objects from these separate Rmd files, the figures within this report were embedded as PNGs, which can still be reproduced by running the Rmd files of each part (i.e. Part1.Rmd, Part2.Rmd, Part3.Rmd), since the chunks save PNGs from the figure-producing code.

In summary, the figures/models within this report for each part of the product can be entirely reproduced by running the three separate Rmd files. This separation was done otherwise knitting this report in one go could potentially take ~ **30 minutes**.

Please let us know if you have any further questions regarding the re- producibility of this report. Also note that tinytex needs to be installed for the PDF to knit through install.packages('tinytex'), and then tinytex::install_tinytex()

Conclusion
-------------------
We believe the risk calculator will aid in the effective and accurate allocation of kidney donor organs to those needing the lifesaving treatment of transplantation. In particular, by predicting a patient’s graft outcome in terms of acute rejection, operational tolerance, and estimated time until DSA appear (in relation to the sub-population corresponding to their phenotype), we hope that we can assist practitioners in their decision-making and make more informed choices in immunosuppressive prescriptions.

Challenges & Learning Points
-------------------
1. Data processing
   - gene expression matrices
     - convert Ensembl IDs to official gene symbols
     - joined multiple matrices by common gene symbols
     - transformations (e.g. log~2) and normalisations
   - CEL files - into a gene expression matrix

2. Model selection
   - use of penalised logistic regression methods to account for the large p small n situation
   - use of the Brier Score as metric to evaluate models for both Part 1 and Part 3 as a way to validate the results from the AUC

3. Shiny application
   - Designing the interface
   - Reading in raw files
   - Create alternative models on the spot if the input data is not suitable for the trained model (e.g. genes from input patient data does not match filtered genes used in the trained model)

Files
-------------------
1. Part1.Rmd - Predicting Acute Rejection
   - Pre-processing gene expression data, using the most significant genes (top 5 up to top 120)
   - Training and selecting models based on their performance in predicting the CV test-set

2. Part2.Rmd - Estimating DSA (donor-specific HLA antibodies) Presence
   - Processing Eplet data
   - Stratified data by phenotype - age and gender

   | age | gender | Class II eplet mismatches |
   | --- | --- | --- |
   | '25-35' | Male | '< 30 ' |
   | '36-45' | Female | '>= 30' |
   | '46-55' |  |  |

3. Part3.Rmd - Predicting Operational Tolerance
   - Gene expression data on patients that were either tolerant or not

4. Report.Rmd
   - Produces a professional pinp document

5. images folder
   - Diagrams generated by rmd files and used in the report
