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
  * /* Input parameters for the "get_models" function.
	
		list<fbamodel_id> models - a list of the model IDs for the models to be returned (a required argument)
		list<workspace_id> workspaces - a list of the workspaces contianing the models to be returned (a required argument)
        string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
		string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)*/
  * typedef structure {
		list<fbamodel_id> models;
		list<workspace_id> workspaces;
		string auth;
        string id_type;
    } get_models_params
2. get_fbas(get_fbas_params input) returns (list<FBA> out_fbas);
  * /* Input parameters for the "get_fbas" function.
	
		list<fba_id> fbas - a list of the FBA study IDs for the FBA studies to be returned (a required argument)
		list<workspace_id> workspaces - a list of the workspaces contianing the FBA studies to be returned (a required argument)
        string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
		string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)*/
  * typedef structure {
		list<fba_id> fbas;
		list<workspace_id> workspaces; 
		string auth;
        string id_type;
    } get_fbas_params
3. get_gapfills(get_gapfills_params input) returns (list<GapFill> out_gapfills);
  * /* Input parameters for the "get_gapfills" function.
	
		list<gapfill_id> gapfills - a list of the gapfill study IDs for the gapfill studies to be returned (a required argument)
		list<workspace_id> workspaces - a list of the workspaces contianing the gapfill studies to be returned (a required argument)
        string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
		string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)*/
  * typedef structure {
		list<gapfill_id> gapfills;
		list<workspace_id> workspaces; 
		string auth;
        string id_type;
    } get_gapfills_params;
4. get_gapgens(get_gapgens_params input) returns (list<GapGen> out_gapgens);
  * /* Input parameters for the "get_gapgens" function.
	
		list<gapgen_id> gapgens - a list of the gapgen study IDs for the gapgen studies to be returned (a required argument)
		list<workspace_id> workspaces - a list of the workspaces contianing the gapgen studies to be returned (a required argument)
        string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
		string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)*/
  * typedef structure {
		list<gapgen_id> gapgens;
		list<workspace_id> workspaces;
		string auth;
        string id_type;
    } get_gapgens_params;
5. get_reactions(get_reactions_params input) returns (list<Reaction> out_reactions);
  * /* Input parameters for the "get_reactions" function.
	
		list<reaction_id> reactions - a list of the reaction IDs for the reactions to be returned (a required argument)
		string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
		string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)*/
  * typedef structure {
		list<reaction_id> reactions;
		string auth;
        string id_type;
    } get_reactions_params;
6. get_compounds(get_compounds_params input) returns (list<Compound> out_compounds);
  * /* 
	        Input parameters for the "get_compounds" function.	
		list<compound_id> compounds - a list of the compound IDs for the compounds to be returned (a required argument)
		string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
		string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)*/
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
25. export_object(export_object_params input) returns (string output);
  * typedef structure {
		workspace_ref reference;
		string type;
		string format;
    	string auth;
    } export_object_params;
26. export_genome(export_genome_params input) returns (string output);
  * typedef structure {
		genome_id genome;
		workspace_id workspace;
		string format;
		string auth;
    } export_genome_params;
27. adjust_model_reaction(adjust_model_reaction_params input) returns (object_metadata modelMeta);
  * typedef structure {
		fbamodel_id model;
		workspace_id workspace;
		list<reaction_id> reaction;
		list<string> direction;
		list<compartment_id> compartment;
		list<int> compartmentIndex;
		list<string> gpr;
		bool removeReaction;
		bool addReaction;
		bool overwrite;
		string auth;
    } adjust_model_reaction_params;
28. adjust_biomass_reaction(adjust_biomass_reaction_params input) returns (object_metadata modelMeta);
  * typedef structure {
		fbamodel_id model;
		workspace_id workspace;
		biomass_id biomass;
		list<float> coefficients;
		list<compound_id> compounds;
		list<compartment_id> compartments;
		list<int> compartmentIndecies;
		string auth;
    } adjust_biomass_reaction_params;
29. addmedia(addmedia_params input) returns (object_metadata mediaMeta);
  * typedef structure {
		media_id media;
		workspace_id workspace;
		string name;
		bool isDefined;
		bool isMinimal;
		string type;
		list<string> compounds;
		list<float> concentrations;
		list<float> maxflux;
		list<float> minflux;
		bool overwrite;
		string auth;
    } addmedia_params;
30. export_media(export_media_params input) returns (string output);
  * typedef structure {
		media_id media;
		workspace_id workspace;
		string format;
		string auth;
    } export_media_params;
31. runfba(runfba_params input) returns (object_metadata fbaMeta);
  * typedef structure {
    	fbamodel_id model;
		workspace_id model_workspace;
		FBAFormulation formulation;
		bool fva;
		bool simulateko;
		bool minimizeflux;
		bool findminmedia;
		string notes;
		fba_id fba;
		workspace_id workspace;
		string auth;
		bool overwrite;
		bool add_to_model;
    } runfba_params;
32. quantitative_optimization(quantitative_optimization_params input) returns (object_metadata output);
  * typedef structure {
    	fbamodel_id model;
		workspace_id model_workspace;
		FBAFormulation formulation;
		fbamodel_id outputid;
		workspace_id workspace;
		string biomass;		
    } quantitative_optimization_params;
33. generate_model_stats(generate_model_stats_params input) returns (model_statistics output);
  * typedef structure {
    	fbamodel_id model;
		workspace_id model_workspace;
    } generate_model_stats_params;
  * typedef structure {
    	string name;
    	string class;
    	string subclass;
    	int genes;
    	int reactions;
    	int model_genes;
    	int minimal_essential_genes;
    	int complete_essential_genes;
		int minimal_essential_reactions;
    	int complete_essential_reactions;
    	int minimal_blocked_reactions;
    	int complete_blocked_reactions;
    	int minimal_variable_reactions;
    	int complete_variable_reactions;
    } subsystem_statistics;
  * typedef structure {
    	int total_reactions;
    	int total_genes;
    	int total_compounds;
    	int extracellular_compounds;
    	int intracellular_compounds;
    	int transport_reactions;
    	int subsystem_reactions;
    	int subsystem_genes;
    	int spontaneous_reactions;
    	int reactions_with_genes;
    	int gapfilled_reactions;
    	int model_genes;
    	int minimal_essential_genes;
    	int complete_essential_genes;
		int minimal_essential_reactions;
    	int complete_essential_reactions;
    	int minimal_blocked_reactions;
    	int complete_blocked_reactions;
    	int minimal_variable_reactions;
    	int complete_variable_reactions;
    	
    	bool growth_complete_media;
    	bool growth_minimal_media;
    	
    	list<subsystem_statistics> subsystems;
    } model_statistics;
34. minimize_reactions(minimize_reactions_params input) returns (object_metadata fbaMeta);
  * typedef structure {
    	fbamodel_id model;
		workspace_id model_workspace;
		workspace_id workspace;
		FBAFormulation formulation;
		list<string> reactions;
		bool all_model_reactions;
		mapping<string,float> reaction_costs;
		fba_id output_id;
    } minimize_reactions_params;
35. funcdef export_fba(export_fba_params input) returns (string output);
  * typedef structure {
		fba_id fba;
		workspace_id workspace;
		string format;
		string auth;
    } export_fba_params;
36. import_phenotypes(import_phenotypes_params input) returns (object_metadata output);
  * typedef structure {
		phenotype_set_id phenotypeSet;
		workspace_id workspace;
		genome_id genome;
		workspace_id genome_workspace;
		list<Phenotype> phenotypes;
		string name;
		string source;
		bool ignore_errors;
		string auth;
    } import_phenotypes_params;
37. simulate_phenotypes (simulate_phenotypes_params input) returns (object_metadata output);
  * typedef structure {
		fbamodel_id model;
		workspace_id model_workspace;
		phenotype_set_id phenotypeSet;
		workspace_id phenotypeSet_workspace;
		FBAFormulation formulation;
		string notes;
		phenotypeSimulationSet_id phenotypeSimulationSet;
		workspace_id workspace;
		bool overwrite;
		string auth;
		bool all_transporters;
		bool positive_transporters;
    } simulate_phenotypes_params;
38. add_media_transporters (add_media_transporters_params input) returns (object_metadata output);
  * typedef structure {
		phenotype_set_id phenotypeSet;
		workspace_id phenotypeSet_workspace;
		fbamodel_id model;
		workspace_id model_workspace;
		fbamodel_id outmodel;
		workspace_id workspace;
		bool overwrite;
		string auth;
		bool all_transporters;
		bool positive_transporters;
    } add_media_transporters_params;
39. export_phenotypeSimulationSet (export_phenotypeSimulationSet_params input) returns (string output);
  * typedef structure {
		phenotypeSimulationSet_id phenotypeSimulationSet;
		workspace_id workspace;
		string format;
		string auth;
    } export_phenotypeSimulationSet_params;
40. integrate_reconciliation_solutions(integrate_reconciliation_solutions_params input) returns (object_metadata modelMeta);
  * typedef structure {
		fbamodel_id model;
		workspace_id model_workspace;
		list<gapfillsolution_id> gapfillSolutions;
		list<gapgensolution_id> gapgenSolutions;
		fbamodel_id out_model;
		workspace_id workspace;
		string auth;
		bool overwrite;
    } integrate_reconciliation_solutions_params;
41. 






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
