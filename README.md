# Metatranscriptomics Pilot
A Pilot Project for scoping an upcoming hackathon focused on metatranscriptomics including topics such as Read Counts, Novel Transcripts and Population Level Functions    

**Authors:**    
Allissa Dillman  
Defne Surujon    
Shurjo Sen    


## Potential Transcriptomic Tools/Pipelines:     

**HUMAnN2**: http://huttenhower.sph.harvard.edu/humann2
https://www.ncbi.nlm.nih.gov/pubmed/30377376
* ID species
* map reads to pangenome of found species
* translated-search for unclassified genes
* gene family and pathway abundance (RPKM)

![Image description](http://huttenhower.sph.harvard.edu/sites/default/files/humann2_diamond_500x500.jpg)


**SAMSA2**: https://transcript.github.io/samsa2/ 
https://www.ncbi.nlm.nih.gov/pubmed/29783945
* matching pair-end reads, QC, remove ribosomal
* align and annotate
* subsystems/RefSeq analysis (DEseq2)
	*who is there
	*what systems are abundant
	*what systems/genes are differentially expressed?

![Image description](https://www.biorxiv.org/content/biorxiv/early/2017/09/29/195826/F1.medium.gif)

**MetaTrans**: http://www.metatrans.org/
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4876386/
* QC, remove ribosomal
* use rRNA for OTU analysis (QIIME)
* use non rRNA for mapping, functional assignment, differential expression (DEseq2)

![Image description](https://media.nature.com/m685/nature-assets/srep/2016/160523/srep26447/images_hires/srep26447-f1.jpg)

**SqueezeMeta**: https://www.frontiersin.org/articles/10.3389/fmicb.2018.03349/full    
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
Human Stool samples; metagenomic (DNA) and metatranscriptomic (RNA) sequencing from 8 people.     
https://www.pnas.org/content/pnas/111/22/E2329.full.pdf    
PRJNA188481    
    
Activated sludge (3 samples);metagenomic (DNA) and metatranscriptomic (RNA) sequencing    
https://www.sciencedirect.com/science/article/pii/S0160412019307603?via%3Dihub    
PRJNA406858    

IBDBMB (The Inflammatory Bowel Disease Multi'omics Database)    
https://ibdmdb.org/    
735 MATCHED Metatranscriptomics and Metagenomics datasets from human stool     
Also includes 16S, proteomics, metabolomics, host transcriptomics and serology data. Also includes rich metadata. 

## A potential method for DNA/RNA comparison: 
Relating the metatranscriptome and metagenome of the human gut    
https://www.pnas.org/content/111/22/E2329.long    

Sample Collection: DNA and RNA collected from the same stool sample, metagenomics and metatranscriptomics processed separately        
![SampleCollection](https://www.pnas.org/content/pnas/111/22/E2329/F1.medium.gif)    
    
Comparison of DNA and RNA abundance    
![DNAvsRNA](https://www.pnas.org/content/pnas/111/22/E2329/F4.medium.gif)    
    
**1. Identify persisters/dormant species in a community**    
    Persisters are often defined as metabolically inactive bacteria, characterized by arrested growth, low ATP levels, and low mRNA expression. Bacteria can enter a persister state when exposed to supra-lethal concentrations of antibiotic, and can resume growth after the antibiotic is removed from the environment. Thus, persistence is a form of transient antibiotic tolerance, and can cause treatment failure and relapse of infection in the clinic (even in the absence of antibiotic resistance). It is therefore crucial to be able to detect persisters in clinical samples. One possible method of detection of persisters is genome-wide absence of RNA transcripts, but a presence of genomic DNA. This can be accomplished by considering the mean or median RNA vs DNA abundances across all pathways of each individual species.

![Bvulgatus](https://github.com/NCBI-Hackathons/Metatranscriptomics_Pilot/blob/master/g__Bacteroides.s__Bacteroides_vulgatus.png?raw=true)     
Mean RNA and DNA abundances for Bacteroides vulgatus. Each point represents a patient sample. Most patients have lower (relative) amounts of RNA from this organism compared to DNA.     

**2. Which genes/pathways are differentially expressed depending on their genetic context?**    
    Homologs of the same gene may be differentially expressed depending on which bacterial species they appear in, despite being in the same environment. This may result in an oversimplification/misinterpretation of metatranscriptomic data. For example, one gene/pathway may be found in high abundance in two very different samples, due to this gene being upregulated in response to different cues, in different organisms. These two cases of high transcript abundance are not biologically equivalent. 
    Can this be explained by methylation patterns? different regulatory elements in different organisms affecting homologs?     
**3. Which genes/pathways (across samples) vary a lot in their expression, but not in their DNA copy number?**     
    Similar to how the same genome in a human can yield vastly different cell types, similar metagenomic compositions in microbial communities can have vastly different transcriptional/functional profiles. While for most genes/pathways there may be a strong correlation between RNA and DNA abundance, there are examples of pathways where DNA abundance does not vary much across samples, but RNA abundance does. 
![FUC-RHAMCAT](https://github.com/NCBI-Hackathons/Metatranscriptomics_Pilot/blob/master/FUC-RHAMCAT-PWY.png?raw=true)    
Fucose-rhamalose catabolism pathway is an example of low variability in terms of DNA abundance, but high variability in RNA abundance.     
~~4. Is the taxonomic profile we get from MetaTrans similar to one from metagenomic taxonomic profiles reported?~~    
    The MetaTrans paper shows some differences between 16S rRNA profiles and 16S rDNA profiles. They attribute this to 16S rDNA not being able to capture the "active" microbial community. 
    
**5. Try to classify clinical outcome (IBD/CD/UC vs healthy) based on metatranscriptomic profiles**    
    Existing studies aim to classify healthy vs diseased patients based on NGS data. This has not yet been attempted with metatranscriptomic data (**check if true**), which potentially has richer and more informative features than metagenomic or 16S data. The IBDMDB dataset would be a good testing ground for training ML models, as it has metatranscriptomics data, and disease metadata.     
**6. Inferring metabolomic profiles from metatranscriptomic data (can we avoid doing LC-MS??)**     
    The IBDMDB dataset is a comprehensive multi-omics dataset that includes metatranscriptomics and metabolomics data. Generating both metatranscriptomic and metabolomic data can be labor-intensive, time-consuming and expensive. (**Why transcriptomics -> metabolomics and not the other way around? Which is more expensive/accessible?**) Therefore, it would be advantageous to be able to infer the metabolomic profile of a sample *in silico* using metatranscriptomic data. 
