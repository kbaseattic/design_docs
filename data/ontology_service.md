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
* typecomp
* auth
* erdb_service
* workspace_deluxe

##Types
###Ontology
####Description 
Appears to be GO term with the genome and gene ids it corresponds to

####Relationships
In the gene list there is genome id and feature ids.  
Note both of these are NOT WS references, but based on the documentation thet are assuming it would likely be KBase ids.

####Fields
* acc - the ontology term GO:NNNN
* type - string of some sort.  Unknown otherwise
* name - Name of the ontology?
* evidence_codes - List of strings, unknown otherwise
* gene_list - mapping of genome_id to a list of feature ids.

###GeneOntologyAnnotation
####Description 
The info for the annotation?

###Relationships
None from what I can tell

####Fields
* ga - gene_annotation_map (gene id key, to a OntologyTermAnnontation 
  * The OntologyTermAnnotation has the following fields
    * ontology_type
    * ontology_description
    * evidence_codes - list of evidenced codes.
* source - source of the annotation ?


###OntologyAccMap
####Description 
The information for the ontology term?

###Relationships
None from what I can tell

####Fields
* ontology_acc_term_map - this a mapping of the ontology term (typically GO:NNNN) to an ontology term subobject. 
  * The ontology term subobject has the following fields
    * type
    * name
    * id
    * parent_list - list of parent term subobjects (contains fields rel_type_id, id)

###Mapping
####Description 
Mapping object holds data on subsystems and complexes.  does not seem like it it should be ontology.

###Relationships
None from what I can tell

####Fields
* id
* name
* roles - list of roles
* subsystems - list of subsystems
* complexes - list of complexes
* role_aliases - mapping of role id to a map (string key? with list of roles aliases as the value)
* complex_aliases - mapping of complex id to a map (string key? with list of complex aliases as the value)
* subsytem_aliases - mapping of subsystem id to a map (string key? with list of subsystem aliases as the value)

