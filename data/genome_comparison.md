#Genome Comparison
##Description 
This service compares two proteomes using Blast

##Owner/Author
Roman Sutormin

##Repo
https://github.com/kbase/genome_comparison

##Data Sources
* Private Data : Data from outside users.  
* Workspace : Public Genomes (which originally came from the CS)

Uses SQL to insert and select from a job queuing tables.  This is only an intermediate database.

##Dependencies
Jars

##Workspace with Data
Private data (creates ProteomeComparison object)

##Workspace Module
GenomeComparison

##Types
###ProteomComparison
####Description 
Stores the proteome comparison of two genomes. 

####Relationships
It has two relationships to KBaseGenomes.Genome ws typed objects. 
These are genome1ref and genome2ref

####Fields
* genome1ws - (depricated, use genome1ref instead)
* genome1id - (depricated, use genome1ref instead)
* genome1ref - ws reference to genome 1
* genome2ws - (depricated, use genome2ref instead)
* genome2id - (depricated, use genome2ref instead)
* genome2ref - ws reference to genome 2
* sub_bbh_percent - optional parameter, minimum percent of bit score compared to best bit score, default is 90
* max_evalue - optional parameter, maximum evalue, default is 1e-10
* proteome1names - list of gene names from Genome 1
* proteome1map - mapping of the genes and their position in Genome 1
* proteome2names - list of gene names from Genome 2
* proteome2map - mapping of the genes and their position in Genome 2
* data1 - List of lists : outer list iterates over positions of genome1 gene names, inner list iterates over hits from given gene1 to genome2
* data1 - List of lists : outer list iterates over positions of genome2 gene names, inner list iterates over hits from given gene2 to genome1
