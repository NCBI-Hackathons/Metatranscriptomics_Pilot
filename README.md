# Metatranscriptomics_Pilot
A Pilot Project for Read Counts, Novel Transcripts and Population Level Functions in Metatranscriptomes

### BrainStorming:
### Tools ATM:     

**HUMAnN2**: http://huttenhower.sph.harvard.edu/humann2
https://www.ncbi.nlm.nih.gov/pubmed/30377376
*This is aval on Biowulf!
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
Accommodates nanopore long reads
Metagenomics and metatranscriptomics

![Image description](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6353838/bin/fmicb-09-03349-g001.jpg)

**Ideas**:    
1.) Looking for mismatch between DNA and RNA, as in low signal in DNA high in RNA and visa versa.    
2.) Able to process short OR long read data    
3.) If methylation data is available, match methylation data with transcription     
4.) “Dark Matter” of metatranscriptomics data: how do we use seq’s that don’t align to any reference genome? How to get functional insight into unaligned reads    

