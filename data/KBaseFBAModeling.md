#FBA Modeling
##Description 
Flux Balance Analysis Modeling

##Owner/Author
Chris Henry

##Repo
https://github.com/kbase/KBaseFBAModeling

##Data Sources
* Uses mongo db
* CS - Uses CDMI
* Workspace
* idserver - which uses mongo


##Dependencies
typecomp
kb_seed
auth
idserver
kb_model_seed
probabilistic_annotation
workspace_deluxe
genome_annotation

##SPECS: 
Note there are 12 spec files.
11 appear to be WS specs and one is a spec file for 95 functions.
Note that many of these specs are duplicated from other repos.
Since the spec is being stored in two locations there is a probability for the WS specs in this repo to be out of date.
The Specs are : 

1. Biochem.spec 
2. Expression.spec
3. FBAModel.spec
4. Genome.spec
5. GenomeComparison.spec
6. Metabolome.spec
7. Ontology.spec
8. Phenotypes.spec
9. ProbabilisticAnnotation.spec
10. Regulation.spec
11. RegulatoryFBA.spec
12. fbaModelServices.spec  - This is where the function specs reside.

##Methods from https://github.com/kbase/KBaseFBAModeling/blob/master/fbaModelServices.spec
95 Methods.

1. get_models(get_models_params input) returns (list<FBAModel> out_models);
  * typedef structure {
		list<fbamodel_id> models;
		list<workspace_id> workspaces;
		string auth;
        string id_type;
    } get_models_params
2. get_fbas(get_fbas_params input) returns (list<FBA> out_fbas);
  * typedef structure {
		list<fba_id> fbas;
		list<workspace_id> workspaces; 
		string auth;
        string id_type;
    } get_fbas_params;
3. get_gapfills(get_gapfills_params input) returns (list<GapFill> out_gapfills);
  * typedef structure {
		list<gapfill_id> gapfills;
		list<workspace_id> workspaces; 
		string auth;
        string id_type;
    } get_gapfills_params;
4. get_gapgens(get_gapgens_params input) returns (list<GapGen> out_gapgens);
  * typedef structure {
		list<gapgen_id> gapgens;
		list<workspace_id> workspaces;
		string auth;
        string id_type;
    } get_gapgens_params;
5. get_reactions(get_reactions_params input) returns (list<Reaction> out_reactions);
  * typedef structure {
		list<reaction_id> reactions;
		string auth;
        string id_type;
    } get_reactions_params;
6. get_compounds(get_compounds_params input) returns (list<Compound> out_compounds);
  * typedef structure {
		list<compound_id> compounds;
		string auth;
        string id_type;
    } get_compounds_params;
7. get_alias(get_alias_params input) returns (list<get_alias_outputs> output);
  * typedef structure {
		string object_type;
		string input_id_type;
		string output_id_type;
		list<string> input_ids;
		string auth;
    } get_alias_params;
  * typedef structure {
		string original_id;
		list<string> aliases;
    } get_alias_outputs;
8. get_aliassets(get_aliassets_params input) returns ( list<string> aliassets );
  * typedef structure {
	string object_type;
	string auth;
    } get_aliassets_params;
9. get_media(get_media_params input) returns (list<Media> out_media);
  * typedef structure {
		list<media_id> medias;
		list<workspace_id> workspaces;
		string auth;
    } get_media_params;
10. get_biochemistry(get_biochemistry_params input) returns (Biochemistry out_biochemistry);
  * typedef structure {
        biochemistry_id biochemistry;
        workspace_id biochemistry_workspace;
        string id_type;
        string auth;
    } get_biochemistry_params;
11. import_probanno(import_probanno_params input) returns (object_metadata probannoMeta);
  * typedef structure {
		probanno_id probanno;
		workspace_id workspace;		
		genome_id genome;
		workspace_id genome_workspace;
		list<annotationProbability> annotationProbabilities;
		bool ignore_errors;
		string auth;
		bool overwrite;
    } import_probanno_params;
12. genome_object_to_workspace(genome_object_to_workspace_params input) returns (object_metadata genomeMeta);
  * typedef string Genome_uid;
  * typedef structure {
		Genome_uid uid;
		GenomeObject genomeobj;
		workspace_id workspace;
		string auth;
		bool overwrite;
    } genome_object_to_workspace_params;
13. genome_to_workspace(genome_to_workspace_params input) returns (object_metadata genomeMeta);
  * typedef structure {
		genome_id genome;
		workspace_id workspace;
		string sourceLogin;
		string sourcePassword;
		string source;
		string auth;
		bool overwrite;
		Genome_uid uid;
    } genome_to_workspace_params;
14. domains_to_workspace(domains_to_workspace_params input) returns (object_metadata GenomeDomainMeta);
  * typedef structure {
		genome_id genome;
		string output_id;
		workspace_id workspace;
		string auth;
    } domains_to_workspace_params;
15. compute_domains(compute_domains_params params) returns (object_metadata output);
  * typedef structure {
		string genome;
		string genome_workspace;
		list<tuple<string,string>> proteins;
		workspace_id workspace;
    } compute_domains_params;
16. add_feature_translation(add_feature_translation_params input) returns (object_metadata genomeMeta);
  * typedef structure {
		genome_id genome;
		workspace_id workspace;
		list<translation> translations;
		string id_type;
		string auth;
		bool overwrite;
    } add_feature_translation_params;
17. genome_to_fbamodel(genome_to_fbamodel_params input) returns (object_metadata modelMeta);
  * typedef structure {
		genome_id genome;
		workspace_id genome_workspace;
		template_id templatemodel;
		workspace_id templatemodel_workspace;
		fbamodel_id model;
		bool coremodel;
		workspace_id workspace;
		string auth;
		bool fulldb;
    } genome_to_fbamodel_params;
18. translate_fbamodel(translate_fbamodel_params input) returns (object_metadata modelMeta);
  * typedef structure {
		list<string> genomes;
		list<string> genome_workspace;
		workspace_id workspace;
    } build_pangenome_params;
19. build_pangenome(build_pangenome_params input) returns (object_metadata output);
  * typedef structure {
		list<string> genomes;
		list<string> genome_workspace;
		workspace_id workspace;
    } build_pangenome_params;
20. genome_heatmap_from_pangenome(genome_heatmap_from_pangenome_params input) returns (heat_map_matrix output);
  * typedef structure {
		string pangenome;
		string pangenome_workspace;
		string workspace;
    } genome_heatmap_from_pangenome_params;
21. ortholog_family_from_pangenome(ortholog_family_from_pangenome_params input) returns (ortholog_data output);
  * typedef structure {
		list<tuple<string,string,string,string,float>> gene_data;
		heat_map_matrix protein_heatmap;
    } ortholog_data;
  * typedef structure {
		string pangenome;
		string pangenome_workspace;
		string orthologid;
		string workspace;
    } ortholog_family_from_pangenome_params;
22. pangenome_to_proteome_comparison(pangenome_to_proteome_comparison_params input) returns (object_metadata output);
  * typedef structure {
		string pangenome;
		string pangenome_workspace;
		string outputid;
		string workspace;
    } pangenome_to_proteome_comparison_params;
23. import_fbamodel(import_fbamodel_params input) returns (object_metadata modelMeta);
  * typedef structure {
		genome_id genome;
		workspace_id genome_workspace;
		string biomass;
		list<tuple<string id,string direction,string compartment,string gpr>> reactions;
		fbamodel_id model;
		workspace_id workspace;
		bool ignore_errors;
		string auth;
		bool overwrite;
    } import_fbamodel_params;
24. export_object(export_object_params input) returns (string output);
  * typedef structure {
		workspace_ref reference;
		string type;
		string format;
    	string auth;
    } export_object_params;
25.





##Workspace with Data
?

##Workspace Module
KBaseFBA

##Types for FBAModel.spec
###FBA
####Description 

####Relationships

####Fields


###FBAModel
####Description 

####Relationships

####Fields


###FBAModelSet
####Description 

####Relationships

####Fields


###Classifier
####Description 

####Relationships

####Fields


###ClassifierResult
####Description 

####Relationships

####Fields


###ETC
####Description 

####Relationships

####Fields


###Gapfilling
####Description 

####Relationships

####Fields


###Gapgeneration
####Description 

####Relationships

####Fields


###ModelTemplate
####Description 

####Relationships

####Fields


###PromConstraint
####Description 

####Relationships

####Fields


###ReactionSensitivityAnalysis
####Description 

####Relationships

####Fields


-----BIOCHEM?
