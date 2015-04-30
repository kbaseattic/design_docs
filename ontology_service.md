#Ontology Service
##Description 
The main functionality of ontology service is to allow the retrieval of ontology term 
distribution for a given a set of genes and additionally, identifies statistically overrepresented 
GO terms within given gene sets

##Owner/Author
Shinjae Yoo, BNL (sjyoo@bnl.gov)
Sunita Kumari, CSHL (kumari@cshl.edu)
Chris Henry (did the workspace typespec)

##Repo
https://github.com/kbase/ontology_service

##Data Sources
* CS (uses the ERDB service to run queries against the feature table)
* Private Data : Data from outside users.  
* Workspace : Public Genomes (which originally came from the CS)
* NY Mysql DB: 
  * mysqldb-host=devdb1.newyork.kbase.us
  * dbname=kbase_plant
  * dbuser=networks_pdev
  * dbport=3306
  * Uses the following tables:
    * ontology_enrichment_annotation - neighbor enrichment and corresponding pValue. 
    * ontology_enr_anno_val - some top level ontology info.
    * ontologies_int - seems to have infor on kbase features and their corresponding ontology and evidence.



##Dependencies
typecomp
auth
erdb_service
workspace_deluxe


*********************************************
*********************************************

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
