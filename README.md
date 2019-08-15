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
    
1. Indentify persisters/dormant species in a community    
    RNA <<< DNA genome wide (or possibly just with 16S rRNA<<16S rDNA) for specific organism
2. Which genes are differentially expressed depending on their genetic context?    
    Same gene has high variance in RNA coming from different species in the same sample    
    Can this be explained by methylation patterns? different regulatory elements?     
3. Which genes (across samples) vary a lot in their expression, but not in their DNA copy number?     
    Same gene has high variance in RNA (and low variance in DNA) across metagenomic samples
![Fig3](https://www.pnas.org/content/pnas/111/22/E2329/F6.large.jpg?width=800&height=600&carousel=1)
    
~~4. Is the taxonomic profile we get from MetaTrans similar to one from metagenomic taxonomic profiles reported?~~    
    The MetaTrans paper shows some differences between 16S rRNA profiles and 19S rDNA profiles. They attribute this to 16S rDNA not being able to capture the "active" microbial community. 
    
5. Try to classify clinical outcome (IBD/CD/UC vs healthy) based on metatranscriptomic profiles    
    use IBDMDB dataset
6. Inferring metabolomic profiles from metatranscriptomic data (can we avoid doing LC-MS??)     
    use IBDMDB dataset
