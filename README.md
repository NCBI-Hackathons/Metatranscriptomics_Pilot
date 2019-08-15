# Metatranscriptomics Pilot
A Pilot Project for scoping an upcoming hackathon focused on metatranscriptomics including topics such as Read Counts, Novel Transcripts and Population Level Functions    

**Authors:**    
Allissa Dillman  
Defne Surujon    
Shurjo Sen    


## Potential Transcriptomic Tools/Pipelines:     

**HUMAnN2** (Franzosa et al., 2018):     
http://huttenhower.sph.harvard.edu/humann2

* ID species
* map reads to pangenome of found species
* translated-search for unclassified genes
* gene family and pathway abundance (RPKM)

![Image description](http://huttenhower.sph.harvard.edu/sites/default/files/humann2_diamond_500x500.jpg)


**SAMSA2** (Westreich et al., 2018):     
https://transcript.github.io/samsa2/ 

* matching pair-end reads, QC, remove ribosomal
* align and annotate
* subsystems/RefSeq analysis (DEseq2)

![Image description](https://www.biorxiv.org/content/biorxiv/early/2017/09/29/195826/F1.medium.gif)

**MetaTrans** (Martinez et al., 2016):     
http://www.metatrans.org/
* QC, remove ribosomal
* use rRNA for OTU analysis (QIIME)
* use non rRNA for mapping, functional assignment, differential expression (DEseq2)

![Image description](https://media.nature.com/m685/nature-assets/srep/2016/160523/srep26447/images_hires/srep26447-f1.jpg)

**SqueezeMeta** (Tamames and Puente-Sanchez, 2019):     
* Accommodates nanopore long reads    
* Metagenomics and metatranscriptomics    
* Co-assembly of multiple metagenomes simultaneously    

![Image description](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6353838/bin/fmicb-09-03349-g001.jpg)

From SqueezeMeta paper: comparison of different methods:    
![Comparison table](https://www.frontiersin.org/files/Articles/425882/fmicb-09-03349-HTML/image_m/fmicb-09-03349-t001.jpg)
## Ideas:    
1.) Looking for mismatch between DNA and RNA, as in low signal in DNA high in RNA and visa versa.        
2.) Able to process short OR long read data - *SqueezeMeta claims to do this*    
3.) If methylation data is available, match methylation data with transcription     
4.) “Dark Matter” of metatranscriptomics data: how do we use seq’s that don’t align to any reference genome? How to get functional insight into unaligned reads - *HUMANn2 addresses this*     
5.) Normalization of expression data based on taxon abundance    
5.b) Take gene copy number into account (same gene may be duplicated in the same genome)        
6.) Co-assembly of multiple metagenomes - *SqueezeMeta addresses this*     


## Datasets:    
| Name              | Type                | Number of Samples | Publication              | SRA Accession | Other Data Resource | Other associated Data                                                   |
|-------------------|---------------------|-------------------|--------------------------|---------------|---------------------|-------------------------------------------------------------------------|
| IBDBMDB           | matched MGX and MTX | 735               | Lloyd-Price et al., 2019 | PRJNA398089   | https://ibdmdb.org/ | Metabolomics, host transcriptomics, 16S, viromics, proteomics, serology |
| Human Stool pilot | matched MGX and MTX | 8                 | Franzosa et al., 2019    | PRJNA188481   |                     |                                                                         |
| Activated sludge  | matched MGX and MTX | 3                 | Liu et al., 2019         | PRJNA406858   |                     |                                                                         |
## A potential method for DNA/RNA comparison: 
Relating the metatranscriptome and metagenome of the human gut    
https://www.pnas.org/content/111/22/E2329.long    

Sample Collection: DNA and RNA collected from the same stool sample, metagenomics and metatranscriptomics processed separately        
![SampleCollection](https://www.pnas.org/content/pnas/111/22/E2329/F1.medium.gif)    
    
Comparison of DNA and RNA abundance    
![DNAvsRNA](https://www.pnas.org/content/pnas/111/22/E2329/F4.medium.gif)    
    
**1. Identify persisters/dormant species in a community**    
    Persisters are often defined as metabolically inactive bacteria, characterized by arrested growth, low ATP levels, and low mRNA expression. Bacteria can enter a persister state when exposed to supra-lethal concentrations of antibiotic, and can resume growth after the antibiotic is removed from the environment (Fisher et al., 2017). Thus, persistence is a form of transient antibiotic tolerance, and can cause treatment failure and relapse of infection in the clinic (even in the absence of antibiotic resistance). It is therefore crucial to be able to detect persisters in clinical samples. One possible method of detection of persisters is genome-wide absence of RNA transcripts, but a presence of genomic DNA. This can be accomplished by considering the mean or median RNA vs DNA abundances across all pathways of each individual species.

![Bvulgatus](https://github.com/NCBI-Hackathons/Metatranscriptomics_Pilot/blob/master/g__Bacteroides.s__Bacteroides_vulgatus.png?raw=true)     
Mean RNA and DNA abundances for Bacteroides vulgatus. Each point represents a patient sample. Most patients have lower (relative) amounts of RNA from this organism compared to DNA.     

**2. Which genes/pathways are differentially expressed depending on their genetic context?**    
    Homologs of the same gene may be differentially expressed depending on which bacterial species they appear in, despite being in the same environment. This may result in an oversimplification/misinterpretation of metatranscriptomic data. For example, one gene/pathway may be found in high abundance in two very different samples, due to this gene being upregulated in response to different cues, in different organisms. These two cases of high transcript abundance are not biologically equivalent. 
    Can this be explained by methylation patterns? different regulatory elements in different organisms affecting homologs?     
**3. Which genes/pathways (across samples) vary a lot in their expression, but not in their DNA copy number?**     
    Similar to how the same genome in a human can yield vastly different cell types, similar metagenomic compositions in microbial communities can have vastly different transcriptional/functional profiles (Franzosa et al., 2014). While for most genes/pathways there may be a strong correlation between RNA and DNA abundance, there are examples of pathways where DNA abundance does not vary much across samples, but RNA abundance does. 
![FUC-RHAMCAT](https://github.com/NCBI-Hackathons/Metatranscriptomics_Pilot/blob/master/FUC-RHAMCAT-PWY.png?raw=true)    
Fucose-rhamalose catabolism pathway is an example of low variability in terms of DNA abundance, but high variability in RNA abundance.     
~~4. Is the taxonomic profile we get from MetaTrans similar to one from metagenomic taxonomic profiles reported?~~    
    The MetaTrans paper shows some differences between 16S rRNA profiles and 16S rDNA profiles. They attribute this to 16S rDNA not being able to capture the "active" microbial community. 
    
**5. Try to classify clinical outcome (IBD/CD/UC vs healthy) based on metatranscriptomic profiles**    
    Existing studies aim to classify healthy vs diseased patients based on NGS data (Bang et al., 2019; Pasolli et al., 2016). Early analysis of metatranscriptomic data has has identified differentially expressed pathways in periodontal disease when compared to healthy oral microbial communities (Jorth et al., 2014). Transcriptomic profiling data potentially has richer and more informative features than metagenomic or 16S data; since it provides information on which genes and pathways have higher transcript abundance and may contribute to a host phenotype. The IBDMDB dataset would be a good testing ground for training ML models, as it has metatranscriptomics data, and disease metadata.     
**6. Inferring metabolomic profiles from metatranscriptomic data (can we avoid doing LC-MS??)**     
    The IBDMDB dataset is a comprehensive multi-omics dataset that includes metatranscriptomics and metabolomics data. Generating both metatranscriptomic and metabolomic data can be labor-intensive, time-consuming and expensive. Moreover, MS often cannot distinguish between highliy similar metabolites **[REF]**, and transcriptomics would potentially provide more detailed information on which metabolic processes are active. Therefore, it would be advantageous to be able to infer the metabolomic profile of a sample *in silico* using metatranscriptomic data. Flux Balance Analysis (Feist et al., 2007; Orth et al., 2010) is a potential approach that can be applied.     
    
## Bibliography

1. Feist AM, Henry CS, Reed JL, Krummenacker M, Joyce AR, Karp PD, et al. A genome-scale metabolic reconstruction for Escherichia coli K-12 MG1655 that accounts for 1260 ORFs and thermodynamic information. Mol Syst Biol [Internet]. 2007 Jun 26 [cited 2019 Aug 15];3. Available from: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1911197/
2. Bang S, Yoo D, Kim S-J, Jhang S, Cho S, Kim H. Establishment and evaluation of prediction model for multiple disease classification based on gut microbial data. Sci Rep. 2019 Jul 15;9(1):1–9. 
3. Pasolli E, Truong DT, Malik F, Waldron L, Segata N. Machine Learning Meta-analysis of Large Metagenomic Datasets: Tools and Biological Insights. PLOS Computational Biology. 2016 Jul 11;12(7):e1004977. 
4. Liu Z, Klümper U, Liu Y, Yang Y, Wei Q, Lin J-G, et al. Metagenomic and metatranscriptomic analyses reveal activity and hosts of antibiotic resistance genes in activated sludge. Environment International. 2019 Aug 1;129:208–20. 
5. Martinez X, Pozuelo M, Pascal V, Campos D, Gut I, Gut M, et al. MetaTrans: an open-source pipeline for metatranscriptomics. Scientific Reports. 2016 May 23;6:26447. 
6. Jorth P, Turner KH, Gumus P, Nizam N, Buduneli N, Whiteley M. Metatranscriptomics of the Human Oral Microbiome during Health and Disease. mBio. 2014 May 1;5(2):e01012-14. 
7. Lloyd-Price J, Arze C, Ananthakrishnan AN, Schirmer M, Avila-Pacheco J, Poon TW, et al. Multi-omics of the gut microbial ecosystem in inflammatory bowel diseases. Nature. 2019 May;569(7758):655–62. 
8. Fisher RA, Gollan B, Helaine S. Persistent bacterial infections and persister cells. Nature Reviews Microbiology. 2017 Aug;15(8):453–64. 
9. Franzosa EA, Morgan XC, Segata N, Waldron L, Reyes J, Earl AM, et al. Relating the metatranscriptome and metagenome of the human gut. Proceedings of the National Academy of Sciences. 2014 Jun 3;111(22):E2329–38. 
10. Franzosa et al. - 2014 - Relating the metatranscriptome and metagenome of t.pdf [Internet]. [cited 2019 Aug 15]. Available from: https://www.pnas.org/content/pnas/111/22/E2329.full.pdf
11. Westreich ST, Treiber ML, Mills DA, Korf I, Lemay DG. SAMSA2: a standalone metatranscriptome analysis pipeline. BMC Bioinformatics. 2018 May 21;19(1):175. 
12. Tamames J, Puente-Sánchez F. SqueezeMeta, A Highly Portable, Fully Automatic Metagenomic Analysis Pipeline. Front Microbiol [Internet]. 2019 [cited 2019 Aug 15];9. Available from: https://www.frontiersin.org/articles/10.3389/fmicb.2018.03349/full
13. Orth JD, Thiele I, Palsson BØ. What is flux balance analysis? Nat Biotechnol. 2010 Mar;28(3):245–8. 
