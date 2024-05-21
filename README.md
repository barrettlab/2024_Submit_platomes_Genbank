# 2024_Submit_platomes_Genbank
A step by step guide for submitting weird plastomes to genbank

# Preparing plastid genomes for submission to NCBI GenBank

 1. Assemble the complete plastome with your favorite assembler (GetOrganelle, NOVOPlasty, FastPlast, etc.)

 2. When you have a finalized, non-draft plastome, conduct annotation. We typically use GeSeq (Tillich et al., 2017) https://chlorobox.mpimp-golm.mpg.de/geseq.html

 3. Import the ‘.gb’ file (GenBank flat file format) into Geneious. There are always things you will need to fix, especially pseudogenes or missed genes, intron/exon boundaries, etc. Fix these, and save the file in Geneious (.gb format).

 4. Now, export the .gb file from Geneious and save it in an annotations_Genbank folder for your project. 

 5. Next, export the fasta sequence from the same file and save in the same place. 

 6. Open the fasta file in a text editor and give the file a name that is informative. 

 7. Here, you will also add __source modifiers__, including specimen_voucher, collection date, country, etc. Example below.

```bash

>2010_Cephalanthera_austiniae [organism=Cephalanthera austiniae] [specimen_voucher=CFB 593c OR] [country=USA] [lineage=Eukaryota; Viridiplantae; Streptophyta; Streptophytina; Embryophyta; Tracheophyta; Euphyllophyta; Spermatophyta; Magnoliopsida; Mesangiospermae; Liliopsida; Petrosaviidae; Asparagales; Orchidaceae; Epidendroideae; Neottieae; Cephalanthera]
TGTTAGCTCAACATATACGACGACGAAGGTAGCAATCCCACCAATATCTTCTTCTTAGAAGAAGATATTGGTGGGATTGCTACCTTCAAAAAT…

```

 8. Use the gb2sequin feature to convert the genbank flat file to a 5-column feature annotation table. https://chlorobox.mpimp-golm.mpg.de/GenBank2Sequin.html


 9. Under ‘Definition’ enter:

```bash

Cephalanthera austiniae plastid, complete genome

```

 10. For ‘Organism’ enter

```bash

Cephalanthera austiniae

```

 11. Click ‘complete’ and ‘circular,’ and ‘plastid’ for Location. For genetic code, choose ‘Bacterial, Archaeal, and Plant Plastid.’ Export the file and save it as the same base name of your fasta file, but use the ‘.tbl’ extension.


 12. Now comes the annoying part. You need to manually edit the .tbl file with a text editor (e.g. Notepad++). Make sure you edit the header of the .tbl file to be the SAME as that in your fasta file!!!

 13. There are four types of features we need to annotate: CDS (Coding DNA sequences), tRNA (transfer RNAs), rRNA (ribosomal RNAs), and ‘misc_features’ (pseudogenes, inverted repeat regions, etc.)

 14A. You’ll need to remove a bunch of nonsense lines, e.g. protein_id, yada yada, and remove the extra gene line that Geneious inserts. CDS should look like this:

```bash

3347	1794	CDS
			codon_start	1
			product	maturase K
			transl_table	11
3347	1794	gene
			gene	matK

```

 CDS that have exons/introns look like this, where you’ll define the coordinates of the coding exons:

```bash
13393	13250	CDS
12455	12045
			codon_start	1
			product	ATP synthase CF0 subunit I
			transl_table	11
13393	12045	gene
			gene	atpF

```

 B. Then there is everyone’s favorite, rps12, which has a 5 prime trans-spliced exon in the LSC (exon 1), and two cis-spliced exons in the IR (exons 2 and 3, which means they each have 2 copies, one in ISb and one in IRa). 

 C. You need to annotate the gene twice: e.g.

```bash

61072	60959	CDS
122496	122727
123269	123294
			codon_start	1
			exception	trans-splicing
			product	ribosomal protein S12
			transl_table	11
61072	123294	gene
			gene	rps12

```

 D. And again…

```bash
61072	60959	CDS
89675	89444
88902	88877
			codon_start	1
			exception	trans-splicing
			product	ribosomal protein S12
			transl_table	11
61072	88877	gene
			gene	rps12

```

 E. Note that you are using the same 5’ exon (in the LSC) for both annotations! Fun times!!!
 

15A. tRNA annotations look like this:

```bash
57616	57543	tRNA
			product	tRNA-Trp
57616	57543	gene
			gene	trnW-CCA
```

 15B. Sometimes tRNAs have an intron, e.g. trnK:

```bash
4311	4275	tRNA
1494	1466
			product	tRNA-Lys
4311	1466	gene
			gene	trnK-UUU
```

 16. rRNAs look like this:

```bash

91761	93252	rRNA
			product	16S ribosomal RNA
91761	93252	gene
			gene	rrn16
```

 17A. Finally, misc_features including the IR and pseudogenes look like this. The key here is they need to have a ‘note’

```bash
74324	100504	misc_feature
			note	inverted repeat B
``` 

 17B. pseudogenes

```bash
124144	126388	misc_feature
			note	ndhB pseudogene
```

 18. Once you have finished, you can check everything in the old Sequin (now mothballed by NCBI), or proceed to BankIt and login (I use my OrcID to log into NCBI). https://www.ncbi.nlm.nih.gov/WebSub/

 19. Click ‘Sequence data not listed above…’ then ‘Start Bankit submission’

 20. Fill in all the info as you go along, and follow the prompts. The rest should be pretty straightforward.

 21. When you get to the part where you upload your feature table, you may see a few errors. The nice thing is you can fix these in your .tbl file and re-upload as many times as needed.

 22. Submit your annotation, voila!





