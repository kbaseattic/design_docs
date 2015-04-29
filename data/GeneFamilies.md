#Gene Families Service (KBaseGeneFamilies)
##Description This service identifies protein domains from widely used domain libraries. It requires a Genome as input, which must already have annotated genes.

##Data
* The domain library files are being stored in Shock.
* Public objects required for the service to work are stored in the KBasePublicGeneDomains workspace.
* All other objects are read from and written to the user's workspace.
* No Central Store data are used.

##Owners/Authors
John-Marc Chandonia, Roman Sutormin, Pavel Novichkov

##Workspace Module
KBaseGeneFamilies

##Workspace with Data
KBasePublicGeneDomains

##Repo
https://github.com/kbase/gene_families

##Data Sources
* COGs (clusters of orthologous groups, http://www.ncbi.nlm.nih.gov/COG/) from the NCBI conserved domains database (CDD) version 3.12.
* NCBI's CDD models from the NCBI conserved domains database (CDD) version 3.12. This dataset includes only the NCBI-curated domains.
* SMART (Simple Modular Architecture Research Tool, http://smart.embl-heidelberg.de/) version 6.0, from the NCBI conserved domains database (CDD) version 3.12.
* Pfam version 27.0 hidden Markov models, from http://pfam.xfam.org/.
* TIGRFAMs version 15.0 hidden Markov models, from the J. Craig Venter Institute.

The licenses for the above external sources are documented here:
https://github.com/kbase/project_guides/blob/master/External_data_sources.md

##Third Party Software used
* RPS-BLAST version 2.2.30, from the BLAST+ package at NCBI
* HMMER version 3.1b1

##Dependencies
* Workspace
* Shock
* NO Central Store dependency

##Module: KBaseGeneFamilies

##Types
###DomainModel
####Description
A Domain Model corresponds to a single HMM model or RPS-BLAST profile, from one of the public domain libraries listed under Data Sources.
####Relationships
Does not reference any other KBase objects, but does contain strings
that refer to the public accessions in the libraries.

####Fields:
* accession : accession string of domain model (e.g., PF00244.1, or COG0001)
* cdd_id : (optional) for CDD models, the inner id that is reported by RPS-BLAST
* name : name of domain model
* description : description of domain model
* length : length of profile
* model_type : domain model type (string enum: PSSM, HMM-Family, HMM-Domain, HMM-Repeat, HMM-Motif)
* trusted_cutoff : (optional) trusted cutoff of domain model for HMM libraries

###Handle
####Description
A Handle refers to a file in Shock.
####Relationships
Contains Shock ids.

####Fields:
* file_name : the original file name of the file stored in Shock
* shock_id : Shock ID

###DomainLibrary
####Description
A Domain Library stores info about a set of domain models that
came from a single source (e.g., a single release of COG or Pfam)
####Relationships
Encapsulates sets of Handles and DomainModels.

####Fields:
* id : id of library
* source : source of library (e.g., COG, Pfam, ...)
* source_url : ftp/http url where library can be downloaded 
* version : version of library release
* release_date : release date of library (in ISO 8601 format; e.g., 2014-11-26)
* program : program for running domain search (enum: hmmscan-3.1b1, rpsblast-2.2.30)
* domain_prefix : prefix of domain accession defining library
* dbxref_prefix : url prefix for db, for external linking
* library_files : list of Handles to the library files
* domains : mapping of accession strings to DomainModel objects

###DomainModelSet
####Description
A Domain Model Set is a set of one or more domain libraries, that
a user can use to search for domains in a Genome in their workspace.
####Relationships
Includes WS references to one or more DomainLibrary objects.

####Fields:
* set_name : name of the set
* domain_libs : mapping of domain prefixes to WS ids of DomainLibrary objects
* domain_prefix_to_dbxref_url : a mapping that caches all the prefixes of the accession strings for various libraries to URLs with external pages with more info about each model (for use in the UI).
* domain_accession_to_description : mapping that caches the description of each model in all the libraries (for use in the UI).

###DomainAnnotation
####Description
A Domain Annotation object contains all the annotations made when
a DomainModelSet is used to search a Genome for domains.
####Relationships
Includes WS references to Genome and DomainModelSet objects.

####Fields:
* genome_ref : reference to Genome that was searched for domains
* used_dms_ref : reference to DomainModelSet used to search the genome
* data : a fairly complex object that stores where domains were annotated in the genome, and the confidence in those annotations
* contig_to_size_and_feature_count : mapping that caches the location of features in contigs in the Genome that was searched (for efficient display in UI)
* feature_to_contig_and_index : mapping that caches the index of every feature in feature list in every contig in the Genome that was searched (for UI)


##Methods

1. Method Name - version
  * Description - returns version number of service
  * Inputs - none
  * Outputs - string containing version number of service
  * Data hit : none

2. Method Name - search_domains
  * Description - searches for domains in a single Genome
  * Inputs
    * genome : Genome WS reference to search for domains (from user's Workspace)
    * dms_ref : DomainModelSet WS reference (from KBasePublicGeneDomains) to search against Genome
    * out_workspace : User's workspace to store the resulting DomainAnnotation object
    * out_result_id : WS reference to the resulting DomainAnnotation object
  * Outputs - the job ID, a string.
  * Data hit : WS objects in KBasePublicGeneDomains, Shock to retrieve library files
