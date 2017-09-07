# FASH16S
Fast Automated SHell based 16S NGS data analysis

#This is the pipeline for running analysis in Terveyden ja hyvinvoinnin laitos (thl) for 16S ngs sequences

#AUTHOR # Balamuralikrishna Jayaprakash #

###Manual (Github,gitlab,Youtube tutorial,wiki page,twitter,facebook,Workshops)

###Title: FASHRUN16S - Fast automated analysis shell based running pipeline for 16S rRNA amplicon NGS data stored in secured windows network drive 

###Introduction

###Next generation sequencing revolutionized the science with the possibility to do massively parallel sequencing of the whole microbiome in many sample altogether. This opens a great possibility to investigate the entire microbial profile rather than just testing few ones in the samples. Also, culture-independent approach in this methods is another advantage to its crown. The genotype or sequence based approach is more useful than the assay or phenotype approach to investigate many questions and also to formulate some questions as well for further research.  In addition, the cost of NGS sequencing is getting low and low which make it feasible to apply and get NGS data. However, this also brings the challenges of how we deal with million and million of sequences and 100s of projects.  The computational analysis by bioinformaticians using various programs helps analyze the data. But over the time, the demand gets increased and many people needs to analyse the data. So, There is a need for the  software tool which can perform automatically the analysis steps and present the results is essential to deal with this situation. FASHRUN16S was developed to achieve this.  

###The main objective of this tool is to automate the 16S NGS data analysis and can be used by biologist or non-programmers around the world who uses similar data analysis. 

###Some of the problems addressed by FASHRUN16S pipeline includes
###(1) automation of running 16S ngs analysis with multiple steps as single tool useful to quickly check the sequences upon arrival
###(2) Confidential data within certain  network can be mounted using CIFS on any Linux workstation or server securely using FASHRUN16S and can be analysed within that network
###(3) Data management organisation integrated in the pipeline which saves time in the present and future of the analysis
###(4) Transperancy and reproducibility is possible in github(www.github.com/FASH16S) 
###(5) R codes executed by R CMD BATCH can perform the data analysis schema included in the pipeline so that the report can be generated with statistics and visualizations
###()

###Method

###This tool was developed under shell scripting approach and use several programming languages like sed,awk,R,python,etc... and several software tools like QIIME version 1.9.1, mothur version x.x.x,  vsearch, etc... The code was documented and tested in github. The data anlaysis can be initiated by SIRI or Google Assisstant. FASHRUN16S uses Common Internet File System (CIFS)to mount the ngs reads in windows network drive to linux workstation or cloud computers or servers or clusters or supercomputers. Then, the sequences provided by  sequnce provider (here the pipeline using demultiplexed sequences which is one of the common files usually provided by such sequencing facilities) which were organised by the pipeline in specific folder such as Results/Analysis.folder from the data/PrimerClipped folder. In order to run the pipeline, the pre-requisite is to have the following folder structure (PROJECT)->data,(PROJECT)->sources-scripts,(PROJECT)->Results,(PROJECT)->documents and sequences  provided were  kept in (PROJECT)->data folder. Then, you run the pipeline ./FASHRUN16S. After the completion of run, FASHRUN16S produces the  following results which is useful for the  initial quick check on whether everything went well with the sample preparation and sequencing. 
### At the end of  FASHRUN16S, considering the data storage demand in NGS, all the  intermediate files will be deleted and only data and results will be organised in a structured data management way so that it will be easy to follow  by the biologist/environmental scientists.
###tested in workstation,cpouta,amazon cloud computing, macbook pro
###This tool aimed for purely biologist or non programmers who dont have any experience in using different command line tools or programming. The idea is that they just place the files in the right folder and follows the folder structure and when they just run FASHRUN16S then they will have the required results from the analysis done by the pipeline. 

###Results

###The results obtain from FASHRUN16S will be in RESULTS folder and organised as mapping file integrated with raw.read.counts,processed.split.read.counts,chimera.removed.read.counts, final.processed.read.counts, final.otu.read.counts, final.otu.table.biom/txt,rep_set.fna,rep_set.tre,alpha_plot_with_controls, beta_plot_with_controls. The results of differences between samples along with control is useful for the quick quality check.

###Discussion

### FASHRUN16S is a useful automated tool for 16S ngs analysis. This framework will be useful for many researchers who were non-programmers for preliminary analysis as well as for the developers to make it better. In addition, the automation helps to reduce the waiting time for a bioinformatician to run the analysis and can be used bay anyone in the lab basically. So, instead of many bioinformatician, one few or one can easily manage the runs with many users using the tool for the analysis.The CIFS (optional) based mounting is useful in situations where your data is sensitive and confidential that you need to run in your own network drives. In addition, in most of the institutes the data is saved in windows network drives and the analysis needs X platforms. So, usually they  copy the files and do the analysis and copy again the results. This increase the data storage demand and FASHRUN16S can be used directly on Windows network drives by CIFS  mount on linux systems or servers.
###Although FASHRUN16S uses the up to date software and the default recommended parameters mentioned in those papers, Remember that the data analysis can be done in multiple ways. So, FASHRUN16S does not claim to be the most optimized pipeline or the best one but rather gave the non-programmers or environmental scientists the option/oppurtunity to run the 16S NGS data analysis in automated way with less or no manual implementation for initial interpretation. However there is option in FASHRUN16S to try different values for the analysis parameters and do your own receipe to see what best fits for your data. It is very flexible to modify FASHRUN16S by the non-programmers as we have explained in simple terms. 
