# Metatranscriptomics_Pilot
A Pilot Project for Read Counts, Novel Transcripts and Population Level Functions in Metatranscriptomes

BrainStorming:
Tools ATM:
HUMAnN2: http://huttenhower.sph.harvard.edu/humann2
https://www.ncbi.nlm.nih.gov/pubmed/30377376

-This is aval on Biowulf!
-ID species
-map reads to pangenome of found species
-translated-search for unclassified genes
-gene family and pathway abundance (RPKM)


SAMSA2: https://transcript.github.io/samsa2/ 
https://www.ncbi.nlm.nih.gov/pubmed/29783945
* matching pair-end reads, QC, remove ribosomal
* align and annotate
* subsystems/RefSeq analysis (DEseq2)
	*who is there
	*what systems are abundant
	*what systems/genes are differentially expressed?

MetaTrans: http://www.metatrans.org/
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4876386/
* QC, remove ribosomal
* use rRNA for OTU analysis (QIIME)
* use non rRNA for mapping, functional assignment, differential expression (DEseq2)



SqueezeMeta: https://www.frontiersin.org/articles/10.3389/fmicb.2018.03349/full
Accommodates nanopore long reads
Metagenomics and metatranscriptomics

Ideas:
Looking for mismatch between DNA and RNA, as in low signal in DNA high in RNA and visa versa.
Able to process short OR long read data
If methylation data is available, match methylation data with transcription
“Dark Matter” of metatranscriptomics data: how do we use seq’s that don’t align to any reference genome? How to get functional insight into unaligned reads

