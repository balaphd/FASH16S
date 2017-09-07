#!/bin/bash
#header for the bash script
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
### The annotation of the command will be with three ###
###connecting/mounting the files using Common internet file system(cifs)
#sudo mount.cifs //helfs01.stakes.fi/groups2/NGS /mnt -o user=bjam,domain=DOMAIN
###making directory 
#mkdir /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder
###copied the files to the analysis folder in Results
#cp /mnt/TEAM/16S/Projects/HSY/data/PrimerClipped/Sample_341F-785R-*/*bz2 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/.
###checking whether the files copied correctly
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/ | wc -l
###unziping the fastq files 
#bunzip2 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*
### checking the files whether it is correctly  unzipped
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/
#less /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
### since fourth line is  containing quality scores , you can only extract every fourth line using sed command as below
#sed -n '0~4p' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq > only.quality.scores
### initial overlook of the bad quality reads.  I need to optimise this code to identify for every sequences. The order below is from very bad quality value to very high quality down below. it is good idea to check  it out the overall distribution and  feel the data.
#grep -c "!" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c '"' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "#" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "\\$" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "%" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "&" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "'" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "(" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c ")" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "*" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "+" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "," /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "-" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "." /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "/" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "0" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "1" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "2" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "3" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "4" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "5" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "6" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "7" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "8" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "9" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c ":" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c ";" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "<" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "=" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c ">" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "?" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "@" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "A" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "B" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "C" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "D" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "E" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "F" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "G" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "H" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "I" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "J" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "K" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "L" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "M" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "N" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "O" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "P" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "Q" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "R" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "S" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "T" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "U" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "V" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "W" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "X" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "Y" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "Z" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "[" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "\" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "]" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "^" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "_" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "`" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "a" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "b" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "c" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "d" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "e" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "f" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "g" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "h" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "i" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "j" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "k" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "l" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "m" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "n" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "o" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "p" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "q" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "r" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "s" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "t" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "u" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "v" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "w" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "x" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "y" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "z" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "{" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "|" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "}" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
#grep -c "~" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R2.fastq
### look for particular sample in order to see pattern in the fastq file
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/
### calculating the number of raw reads in each sample
#wc -l /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R1.fastq
#less /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R1.fastq
#tail /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R1.fastq
#head /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R1.fastq
#grep -c "@MISEQ-M" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-A01-16V439_R1.fastq
### after checking the pattern in the sequences the count of raw sequences were calculated by grep as above for one sample. But for all samples we use regular expression as below
#grep -c "@MISEQ-M" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/* > /path/to/raw.reads.txt
### save the output of the grep  command that we used above as raw.reads.txt or you can pipe(|) it to the following commands too
#grep "_R1.fastq" /path/to/raw.reads.txt | sed -e 's:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/341F-785R-::g' -e 's/:/ /g' -e 's/_R1.fastq/ /g' > /path/to/raw.reads.fmt.txt
###We used the R code to integrate the raw reads into the mapping file to see whether there is some weird samples based on just raw reads. But we will do the same once we process the data too. This is preliminary check to make sure what the data tells and have some alarming info
#R CMD merge.R
### lof of this R run will be saved in the sources-script folder
################ merge.R  ###########################################
#table <- read.csv('mapping_file_HSY_18.8.17.txt',header=T,sep="\t")
#table.raw <- read.csv('raw.reads.fmt.txt',header=T,sep="")
#MERGE.raw.with.map <- merge(table,table.raw,by="run_prefix")
#write.table(MERGE.raw.with.map,file="map.with.raw.reads.txt",sep="\t",row.names=F,quote=F)
#quit()
#####################################################################
### testing any blank lines in the raw ngs reads  ### add print "No blank line found" (will do it later)
#awk '!NF{print NR}' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*
###  testing whether there is no missing lines in raw reads
#sed -n '1~4p' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/* | wc -l
#sed -n '2~4p' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/* | wc -l
#sed -n '3~4p' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/* | wc -l
#sed -n '4~4p' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/* | wc -l
### combining all the raw reads together to see the overall quality of the raw reads
#cat /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*_R1.fastq > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/qc/all_R1.fastq
#echo Bala!!! r1 reads were combined
#cat /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*_R2.fastq > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/qc/all_R2.fastq
#echo Bala!!! r2 reads were combined
### fastqc is the software that can be use to access the quality of the data per position
#fastqc all_R1.fastq -o output_r1_all_HSY -f fastq --kmers 8
#echo Bala!!! r1 reads were run by fastqc
#fastqc all_R2.fastq -o output_r2_all_HSY -f fastq --kmers 8
#echo Bala!!! r2 reads were run by fastqc
### checking whether the forward primers were overrepresented from  fastqc results above
#grep --color "CCTACGGG[ACGT]GGC[AT]GCAG" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/qc/all_R1.fastq
#echo primer sequences were checked
### checking the reverse compliment too to make sure we dont  miss in other direction of pcr or sequencing but it is less possible to get this way as the sequencing of forward is from 5' to 3' direction
#grep --color "CTGC[AT]GCC[ACGT]CCCGTAGG" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/qc/all_R1.fastq
#echo reverse compliment forward primers were checked too just in case
### checking the reverse primer sequences as well
#grep "GACTAC[ACT][ACG]GGGTATCTAA[TG]CC" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/qc/all_R1.fastq
#grep "GACTAC[ACT][ACG]GGGTATCTAA[TG]CC" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/qc/all_R2.fastq
#grep "GG[AC]TTAGATACCC[CGT][AGT]GTAGTC" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/qc/all_R1.fastq
#grep "GG[AC]TTAGATACCC[CGT][AGT]GTAGTC" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/qc/all_R2.fastq
### The conclusion is that the primers are not really overrepresented and blast of those overrepresented sequences were done with customised only  16S bacteria and Archaea database and the results show that those sequences were  bacteria such as sphingomonas, rhizobales, etc..etc..jenni will try this when she practice and add more taxa that were over-represented
### The removal of adapter sequnces from illumina sequencing was performed by cutadapt
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*R1.fastq > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/1
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*R2.fastq > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/2
#sed -e 's/^/cutadapt -a AGATCGGAAGAGCACACGTCTGAACTCCAGTCAC -A AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTAGATCTCGGTGGTCGCCGTATCATT -o /g' -e 's/R1.fastq/R1_adap.rmv.fastq/g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/1 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/3
#sed -e 's/^/ -p /g' -e 's/R2.fastq/R2_adap.rmv.fastq/g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/2 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/4
#paste /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/3 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/4 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/1 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/2 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_for_cutadapt.sh
### installation of cutadapt (if needed)
#sudo apt-get -y install python-pip
#sudo pip install cutadapt
#script -a catch.cutadapt.output.throwing
#sh /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_for_cutadapt.sh
#use Ctrl+A+D to save the catch.cutadapt.output.throwing file when the run was complete.
### Other way of doing this is using just > after the shell script like below
#sh /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_for_cutadapt.sh > catch.cutadapt.output.throwing
### Trimming of the  reads  with Trimmomatic software before the flash2 based merging/combining the forward and reverse reads
### installing Trimmomatic software locally
#wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip --directory-prefix=/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder 
#unzip /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/Trimmomatic-0.36.zip -d /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder
#sed -e 's:^:java -jar /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/Trimmomatic-0.36/trimmomatic-0.36.jar PE -phred33 :g' -e 's/R1.fastq/R1_adap.rmv.fastq/g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/1 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/5
#sed -e 's/R1.fastq/R1_adap.rmv.fastq/g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/1 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/6
#sed -e 's/R2.fastq/R2_adap.rmv.fastq/g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/2 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/7
#sed 's:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/output_paired_:g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/6 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/8
#sed 's:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/output_unpaired_:g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/6 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/9
#sed 's:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/output_paired_:g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/7 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/10
#sed -e 's:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/output_unpaired_:g' -e 's/$/ ILLUMINACLIP:TruSeq3-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36/g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/7 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/11
#paste /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/5 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/7 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/8 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/9 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/10 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/11 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_for_trimmomatic.sh
#sh /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_for_trimmomatic.sh
### combine the reads of trimmed  paired forward and reverse reads using  Flash2  software
#wget https://github.com/dstreett/FLASH2/archive/master.zip --directory-prefix=/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder
#unzip /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/master.zip -d /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder
#cd /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/FLASH2-master/
#make
#cd /mnt/TEAM/16S/Projects/HSY/sources-scripts
#PATH=$PATH:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/FLASH2-master
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/output_paired_*R1_adap.rmv.fastq > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/12
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/output_paired_*R2_adap.rmv.fastq > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/13
#sed -e 's/R1/combined/g' -e 's:^: -d /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder -o :g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/12 | sed 's:-o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/:-o :g' > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/14
#paste /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/12 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/13 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/14 | sed -e 's/^/flash2 -m 10 -M 600 -x 0.60 /g' > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_for_combine.sh
#echo done
#sh /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_for_combine.sh
###  combine the R1 orphan reads from trimmomatic, R1 orphan reads from flash2 and combined reads from flash2
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*extendedFrags* | sed 's/^/cat /g' > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/15 
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/output_unpaired*R1* > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/16
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*notCombined_1* > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/17
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/*extendedFrags* | sed -e 's/combined_adap.rmv.fastq.extendedFrags.fastq/all.combined.fastq/g' -e 's/output_paired_//g' -e 's:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/: > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/:g' > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/18
#paste /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/15 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/16 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/17 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/18 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_to_combine_all_reads.sh
#sh /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/run_to_combine_all_reads.sh
### now we are making the pre or dummy mapping file  in order to process further for quality, N bases removal and so on and also demultiplex the samples so that each sample get a unique sampleid useful to follow in the downstream process of the analysis. we are still in the upstream processing .
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/*.fastq | sed -e 's/341F-785R-//g' -e 's/_all.combined.fastq//g' -e 's/-/./g' -e 's:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/::g' > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampleid
#echo LinkerPrimerSequence > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/LinkerPrimerSequence
#######################################HERE I NEED TO FIX THE CODE  AS IT IS NOT EXECUTING FROM .SH  FILE BUT JUST EXECUTES FROM COMMAND LINE 
#for i in {1..96}
#do 
#echo CCTACGGGNGGCWGCAG
#done 
#for i in {1..96}; do echo CCTACGGGNGGCWGCAG; done >> /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/LinkerPrimerSequence
#sh for.loop.for.filling.linkerprimersequence.sh >> /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/LinkerPrimerSequence
#echo BarcodeSequence > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/BarcodeSequence
#echo Description > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/Description
#cat /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampleid >> /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/Description
#cp /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampleid /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampletemp
### add #SampleID to sampleid
#sed  -i '1i #SampleID' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampleid
#paste /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampleid /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/BarcodeSequence /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/LinkerPrimerSequence /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/Description > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/mapping_file_pre_HSY.txt
#sed -e "s:^:sed -ne '1p' -e '/:g" -e "s:$:/p' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/mapping_file_pre_HSY.txt:g" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampletemp > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/run_for_map_part1
#sed 's:^: > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/mappingfile_:g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampletemp > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/run_for_map_part2
#paste /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/run_for_map_part1 /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/run_for_map_part2 > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/run_for_map.sh
#sh /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/run_for_map.sh
### After pre mapping file is created  then it is used for running the additional major preprocessing using split_libraries_fastq.py as below
#ls /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/*.fastq > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/inputfile
#sed 's:^:-m /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/mappingfile_:g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampletemp > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/mapping
#sed 's:^:-o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/slout_:g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampletemp > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/outfile
#sed 's/^/--sample_id /g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampletemp > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampleidtag
#paste /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/inputfile /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/mapping /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/outfile /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/sampleidtag | sed -e 's/^/split_libraries_fastq.py -i /g' -e 's/$/ --phred_offset 33 -q 20 --barcode_type not-barcoded/g' > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/run_for_split_HSY_16s.sh
### installing qiime to run split_libraries_fastq quality filtering and demultiplexing
#pip install numpy
#pip install qiime
#sh /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/run_for_split_HSY_16s.sh
### checking the size of the files
#ls -l /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/slout_*/seqs.fna
### counting the processed read counts
#grep -c "^>" /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/slout_*/seqs.fna > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/read.counts.after.processing.split
#sed -e "s:/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/slout_::g" -e 's|/seqs.fna:| |g' /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/read.counts.after.processing.split >  /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final.read.counts.after.processing.txt
### saving the read counts for merging with mapping file
#sed 's/-/./g' /mnt/TEAM/16S/Projects/HSY/documents/map.with.raw.reads.txt > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/map.with.raw.reads.fmt.txt
### merge.map.with.reads.R
### This is R code for merging processed read counts with mapping file with raw reads ###
#table1 <- read.csv('/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/map.with.raw.reads.fmt.txt',header=T,sep="\t")
#table2 <- read.csv('/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final.read.counts.after.processing.txt',header=T,sep=" ")
#MERGE <- merge(table1,table2,by="samples")
#write.table(MERGE,file="/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/map.with.raw.readcounts.plus.split.readcounts.txt",sep="\t",row.names=F,quote=F)
#quit()
###########
#R CMD BATCH /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/merge.map.with.reads.R
### add the plate well location for each sample in mapping file and see the read counts and plate well location have some patterns
###  Corner wells in plate were A1,A12,H1,H12 etc...
### Check with the PCR cycle numbers and see the higher cycle number creates more artificial sequences by comparing the  chimera removed sequences
#cat /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/slout_*/seqs.fna > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final_demultiplexed_16s_seqs_HSY.fasta
#example of mothur is like this from command line $ mothur "#read.dist(phylip=98_sq_phylip_amazon.dist, cutoff=0.1); cluster(); collect.single(); rarefaction.single()"
#mothur "#summary.seqs(fasta=/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final_demultiplexed_16s_seqs_HSY.fasta)"
### Removing chimeras from the sequences by vsearch
### installing the vsearch software
#git clone https://github.com/torognes/vsearch.git
#cd vsearch
#./autogen.sh
#./configure
#make
#make install
#PATH=$PATH:/mnt/TEAM/16S/Projects/HSY/sources-scripts/vsearch
#vsearch --derep_full /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final_demultiplexed_16s_seqs_HSY.fasta --output /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/derep_HSY_all.fasta --log=log --sizeout --minuniquesize 2
#vsearch --uchime_denovo /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/derep_HSY_all.fasta --nonchimeras /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/nonchimeras_all.fasta --sizein --xsize --chimeras /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/chimeras_all.fasta
#cat /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/chimeras_all.fasta | grep "^>" | sed -e 's/>//g' -e 's/;.*//g' > /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/chimeras_seqid.txt
#filter_fasta.py -f /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final_demultiplexed_16s_seqs_HSY.fasta -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final_chimera_rmv_seqs_16s_HSY_ALL.fasta -s /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/chimeras_seqid.txt -n
### checking the summary of sequences using summay.seqs() function in mothur 
#mothur "#summary.seqs(fasta=/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final_chimera_rmv_seqs_16s_HSY_ALL.fasta)"
### check the low length reads and remove it
#mothur "#screen.seqs(fasta=/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final_chimera_rmv_seqs_16s_HSY_ALL.fasta, minlength=250)"
### check the distribution of length of reads
### check the kmer frequencies
### check the PhiX reads and remove them in the sequences 
### blast the reads against nr database and see whether you find any sequences other than bacterial kingdom
### blast again against customised 16S database or greengenes to see whether we have any contamination
### Remove the sequences identified as non-bacterial/archaeal sequences 
### construct a phylogenetic tree with "no hit" reads along with all other reads to see the reads closer association with any species
####### parameter file for open reference OTU picking
#nano open_params.txt
# cat open_params.txt
#pick_otus:otu_picking_method swarm
#assign_taxonomy:assignment_method sortmerna
#wget ftp://greengenes.microbio.me/greengenes_release/gg_13_5/gg_13_8_otus.tar.gz --directory-prefix=/mnt/TEAM/16S/Projects/HSY/sources-scripts/database
#tar -xvzf /mnt/TEAM/16S/Projects/HSY/sources-scripts/database/gg_13_8_otus.tar.gz --directory /mnt/TEAM/16S/Projects/HSY/sources-scripts/database/
#pick_open_reference_otus.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/final_chimera_rmv_seqs_16s_HSY_ALL.good.fasta -r /mnt/TEAM/16S/Projects/HSY/sources-scripts/database/gg_13_8_otus/rep_set/97_otus.fasta -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus -a -O 4 --percent_subsample 1 -v
#### downstream of data processing starts here. The raw otu table has to be processed to obtain final otu table
#### filtering the spurious OTUs
#filter_otus_from_otu_table.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/otu_table_mc2_w_tax_no_pynast_failures.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/bact_otu_table_mc2_w_tax_no_pynast_failures_min00001.biom --min_count_fraction 0.00001
#### filtering the chloroplast and mitochondrial OTUs
#filter_taxa_from_otu_table.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/bact_otu_table_mc2_w_tax_no_pynast_failures_min00001.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/bact_otu_table_mc2_w_tax_no_pynast_failures_min00001_nochloro.biom -n  c__Chloroplast,f__mitochondria
#### filtering the singletons OTUs
#filter_otus_from_otu_table.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/bact_otu_table_mc2_w_tax_no_pynast_failures_min00001_nochloro.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.biom -n 1
#### convert the biom format to readable txt or excel openable format
#biom convert -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.txt --header-key taxonomy --table-type "OTU table" --to-tsv
#### Summarize the OTU table  for total read count in each sample and its stats
#biom summarize-table -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/summary.with.controls.txt
### Till this point the pipeline automatically process all the samples you put in the PRIMERCLIPPED folder in "/mnt/TEAM/16S/Projects/HSY/data" folder. So, since we did not seperate vesitorni and  HSY  in the inital analysis, the otu table summary contains both dataset summary. 
####### merge.final.samples.with.control.R ######
#table_map_pre <- read.csv('/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/mapping_file_pre_HSY.txt',header=T,sep="\t",check.names=F)
#table_map_final <- read.csv('/mnt/TEAM/16S/Projects/HSY/documents/Mappingfile.THL.HSYaktiivi.31.08.2017.txt',header=T,sep="\t",check.names=F)
#MERGE <- merge(table_map_pre,table_map_final,by="#SampleID")
#write.table(MERGE,file="/mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/map.merged.txt",sep="\t",row.names=F,quote=F)
#quit()
#################################################
#R CMD BATCH merge.final.samples.with.control.R
#################################################
### filter samples only HSY
#filter_samples_from_otu_table.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.all.biom --sample_id_fp /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/map.merged.txt -m  /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/map.merged.txt --output_mapping_fp /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/map.filtered.with.controls.txt
### convert the biom table into readable txt file
#biom convert -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.all.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.txt --header-key taxonomy --table-type "OTU table" --to-tsv
#biom summarize-table -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.all.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/summary.HSY.only.with.controls.txt

# change the names using the code column and  use the sort otu table  script and then use taxa plot 



### make the taxa summary of all samples so that we knew what microbes in those few sequences too


#summarize_taxa_through_plots.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.all.updated.biom -o taxa_summary_individuals_all
### Filter the biom table for low read counts
### Then, beta diversity plots along with controls with the selected reasonable counts 
#beta_diversity_through_plots.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/final.otu.table.HSY.with.controls.all.biom 
### Here look at the summary and add the rarefaction value based on lowest number with controls to see in the beta plot whether the  samples and controls were seperate and explain the biological signal or any contamination
### filter the otu table for only HSY by merging the dummy mapping file with original HSY mapping file

### filter-out the samples below the selected e value and get filtered otu.table and  mapping file

### Then add that value below in -e and -o naming parameters of beta_diversity_through_plots.py replacing "put.e.value.here" and input the filtered  

#sort_otu_table.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/bact_otu_table_mc2_w_tax_no_pynast_failures_min00001_nochloro.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/sorted_otutable.biom -l /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/samples_order.txt
#beta_diversity_through_plots.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/bact_otu_table_mc2_w_tax_no_pynast_failures_min00001_nochloro.biom -e put.e.value.here -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/bdiv_eput.e.value.here -t /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/rep_set.tre -m /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/map.txt -v -a -O 4
#alpha_rarefaction.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/bact_otu_table_mc2_w_tax_no_pynast_failures_min00001_nochloro.biom -e 411 -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/arare_e411 -t /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/rep_set.tre -m /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/map.txt -v -a -O 4
#summarize_taxa_through_plots.py -i /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/sorted_otutable.biom -o /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/taxa_summary -p /mnt/TEAM/16S/Projects/HSY/Results/Analysis.folder/final_combined_reads/bact_open_ref_picked_otus/taxa_params.txt

### then check the list of mock microbes in positive control samples whether they were identified with good taxonomic resolution

### Filter out all the controls and only keep the actual samples

### creating alpha diversity rarefaction for actual samples

### creating beta diversity plot for actual samples

### performing stats for alpha diversity values ()

### performing stats for beta diversity values (anosim,adonis)

#echo "the samples which has low read counts were xxx,yyy,zzz"
#echo "the samples failed in the preprocessing were xxx,yyy,zzz"
#echo "the mapping file with combined raw, split processed, chimera removed, otu table read counts (both continuous and categorised)were in the follwing path /mnt/TEAM/16S/Projects/HSY/Results/"
#echo "the otu table were in /mnt/TEAM/16S/Projects/HSY/Results/otu.table.txt"
#echo "the representavive sequences were in /mnt/TEAM/16S/Projects/HSY/Results/rep_set.fna"
#echo "the otu tree were in /mnt/TEAM/16S/Projects/HSY/Results/rep_set.tre"
#for i in {1..96}; do echo CCTACGGGNGGCWGCAG; done
echo done
 
