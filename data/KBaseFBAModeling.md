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
11. import_probanno(import_probanno_params input) returns (object_metadata probannoMeta);
12. genome_to_workspace(genome_to_workspace_params input) returns (object_metadata genomeMeta);




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
