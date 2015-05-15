Module: genome_annotation

Description: Provides support for gene calling, functional annotation, re-annotation. Use to extract annotation information about an existing genome, or to create new annotations.

Data: 

Repo: https://github.com/kbase/genome_annotation

Data Sources: CS, user uploads through handle object (?)

Input Types: genome_id, genome_metadata (internal to service), genomeTO (internal to service, all info about a genome)

Output types: contig (internal to service), feature (internal to service), genomeTO (internal to service, all info about a genome), reconstructionTO (set of SEED subsystems found in genome), tuple<> cdd_hit



Methods:

Method name - genome_ids_to_genomes(list<genome_id> ids) returns (list<genomeTO> genomes);
Description - Given one or more Central Store genome IDs, convert them into genome objects.
Inputs - list<genome_id> ids
Outputs - list<genomeTO> genomes

Method name - create_genome(genome_metadata metadata) returns (genomeTO genome);
Description - Create a new genome object and assign metadata.
Inputs - genome_metadata metadata
Outputs - genomeTO genome

Method name - create_genome_from_SEED(string genome_id) returns (genomeTO genome);
Description - Create a new genome object based on data from the SEED project.
Inputs - string genome_id
Outputs - (genomeTO genome

Method name - create_genome_from_RAST(string genome_or_job_id) returns (genomeTO genome); /*  authentication optional; */
Description - Create a new genome object based on a RAST genome.
Inputs - string genome_or_job_id
Outputs - genomeTO genome

Method name - set_metadata(genomeTO genome_in, genome_metadata metadata) returns (genomeTO genome_out);
Description - Modify genome metadata.
Inputs - genomeTO genome_in, genome_metadata metadata
Outputs - genomeTO genome_out

Method name - add_contigs(genomeTO genome_in, list<contig> contigs) returns (genomeTO genome_out);
Description - Add a set of contigs to the genome object.
Inputs - genomeTO genome_in, list<contig> contigs
Outputs - genomeTO genome_out

Method name - add_contigs_from_handle(genomeTO genome_in, list<contig> contigs) returns (genomeTO genome_out);
Description - Add a set of contigs to the genome object, loading the contigs from the given handle service handle.
Inputs - genomeTO genome_in, list<contig> contigs
Outputs - genomeTO genome_out

Method name - add_features(genomeTO genome_in, list<compact_feature> features) returns (genomeTO genome_out);
Description - Add a set of features in tabular form.
Inputs - genomeTO genome_in, list<compact_feature> features
Outputs - genomeTO genome_out

Method name - genomeTO_to_reconstructionTO (genomeTO) returns (reconstructionTO);
Description -
Inputs - genomeTO
Outputs - reconstructionTO

Method name - genomeTO_to_feature_data (genomeTO) returns (fid_data_tuples);
Description -
Inputs - genomeTO
Outputs - fid_data_tuples

Method name - reconstructionTO_to_roles (reconstructionTO) returns (list<role>);
Description -
Inputs - reconstructionTO
Outputs - list<role>

Method name - reconstructionTO_to_subsystems(reconstructionTO) returns (variant_subsystem_pairs);
Description -
Inputs - reconstructionTO
Outputs - variant_subsystem_pairs

Method name - assign_functions_to_CDSs(genomeTO) returns (genomeTO);
Description - Given a genome object populated with contig data, perform gene calling and functional annotation and return the annotated genome.
Inputs - genomeTO
Outputs - genomeTO

Method name - annotate_genome(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_selenoproteins(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_pyrrolysoproteins(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_selenoprotein(genomeTO) returns (genomeTO);
Description - Given a genome typed object, call selenoprotein features.
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_pyrrolysoprotein(genomeTO) returns (genomeTO);
Description - Given a genome typed object, call pyrrolysoprotein features.
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_insertion_sequences(genomeTO) returns (genomeTO);
Description - Given a genome typed object, call insertion sequences.
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_rRNA_SEED(genomeTO genome_in, list<rna_type> types) returns (genomeTO genome_out);
Description - Given a genome typed object, find instances of ribosomal RNAs in the genome.
Inputs - genomeTO genome_in, list<rna_type> types
Outputs - genomeTO

Method name - call_features_tRNA_trnascan(genomeTO genome_in) returns (genomeTO genome_out);
Description - Given a genome typed object, find instances of tRNAs in the genome.
Inputs - genomeTO
Outputs - genomeTO

Method name - call_RNAs(genomeTO genome_in) returns (genomeTO genome_out);
Description - Given a genome typed object, find instances of all RNAs we currently have support for detecting.
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_CDS_glimmer3(genomeTO, glimmer3_parameters params) returns (genomeTO);
Description -
Inputs - genomeTO, glimmer3_parameters params
Outputs - genomeTO

Method name - call_features_CDS_prodigal(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_CDS_genemark(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_CDS_SEED_projection(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_CDS_FragGeneScan(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_repeat_region_SEED(genomeTO genome_in, repeat_region_SEED_parameters params) returns (genomeTO genome_out);
Description -
Inputs - genomeTO genome_in, repeat_region_SEED_parameters params
Outputs - genomeTO

Method name - call_features_prophage_phispy(genomeTO genome_in) returns (genomeTO genome_out);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_scan_for_matches(genomeTO genome_in, string pattern, string feature_type) returns (genomeTO genome_out);
Description -
Inputs - genomeTO genome_in, string pattern, string feature_type
Outputs - genomeTO

Method name - annotate_proteins_similarity(genomeTO, similarity_parameters params) returns (genomeTO);
Description - Annotate based on similarity to annotation databases.
Inputs - genomeTO, similarity_parameters params
Outputs - genomeTO

Method name - annotate_proteins_kmer_v1(genomeTO, kmer_v1_parameters params) returns (genomeTO);
Description -
Inputs - genomeTO, kmer_v1_parameters params
Outputs - genomeTO

Method name - annotate_proteins_kmer_v2(genomeTO genome_in, kmer_v2_parameters params) returns (genomeTO genome_out);
Description -
Inputs - genomeTO genome_in, kmer_v2_parameters params
Outputs - genomeTO

Method name - resolve_overlapping_features(genomeTO genome_in, resolve_overlapping_features_parameters params) returns (genomeTO genome_out);
Description -
Inputs - genomeTO genome_in, resolve_overlapping_features_parameters params
Outputs - genomeTO

Method name - call_features_ProtoCDS_kmer_v1(genomeTO, kmer_v1_parameters params) returns (genomeTO);
Description -
Inputs - genomeTO, kmer_v1_parameters params
Outputs - genomeTO

Method name - call_features_ProtoCDS_kmer_v2(genomeTO genome_in, kmer_v2_parameters params) returns (genomeTO genome_out);
Description -
Inputs - genomeTO genome_in, kmer_v2_parameters params
Outputs - genomeTO

Method name - enumerate_special_protein_databases() returns (list<string> database_names);
Description -
Inputs -
Outputs - list<string> database_names

Method name - compute_special_proteins(genomeTO genome_in, list<string> database_names) returns (list<special_protein_hit> results);
Description -
Inputs - genomeTO genome_in, list<string> database_names
Outputs - list<special_protein_hit> results

Method name - compute_cdd(genomeTO genome_in) returns (list<cdd_hit>);
Description -
Inputs - genomeTO genome_in
Outputs - list<cdd_hit>

Method name - annotate_proteins(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - estimate_crude_phylogenetic_position_kmer(genomeTO) returns (string position_estimate);
Description - Determine close genomes
Inputs - genomeTO
Outputs - string position_estimate

Method name - find_close_neighbors(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_strep_suis_repeat(genomeTO) returns (genomeTO);
Description - Interface to Strep repeats and "boxes" tools
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_strep_pneumo_repeat(genomeTO) returns (genomeTO);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - call_features_crispr(genomeTO genome_in) returns (genomeTO genome_out);
Description -
Inputs - genomeTO
Outputs - genomeTO

Method name - update_functions(genomeTO genome_in, list<tuple<feature_id, string function>> functions, analysis_event event)
Description -
Inputs - genomeTO genome_in, list<tuple<feature_id, string function>> functions, analysis_event event
Outputs - genomeTO

Method name - renumber_features(genomeTO genome_in) returns (genomeTO genome_out);
Description - Renumber features such that their identifiers are contiguous along contigs.
Inputs - genomeTO
Outputs - genomeTO

Method name - export_genome(genomeTO genome_in, string format, list<string> feature_types) returns (string exported_data);
Description - Export genome typed object to one of the supported output formats: genbank, embl, or gff.
Inputs - genomeTO genome_in, string format, list<string> feature_types
Outputs - string exported_data

Method name - enumerate_classifiers() returns (list<string>);
Description - Enumerate the available classifiers. Returns the list of identifiers for the classifiers.
Inputs -
Outputs - list<string>

Method name - query_classifier_groups(string classifier) returns(mapping<string group_id, list<genome_id>>);
Description - Query the groups included in the given classifier. This is a mapping from the group name to the list of genome IDs included in the group.
Inputs - string classifier)
Outputs - mapping<string group_id, list<genome_id>>

Method name - query_classifier_taxonomies(string classifier) returns(mapping<string group_id, string taxonomy>);
Description - Query the taxonomy strings that this classifier maps.
Inputs - string classifier
Outputs - mapping<string group_id, string taxonomy>

Method name - classify_into_bins(string classifier, list<tuple<string id, string dna_data>> dna_input) returns(mapping<string group_id, int count>);
Description - Classify a dataset, returning only the binned output.
Inputs - string classifier, list<tuple<string id, string dna_data>> dna_input
Outputs - mapping<string group_id, int count>

Method name - classify_full(string classifier, list<tuple<string id, string dna_data>> dna_input) returns(mapping<string group_id, int count>, string raw_output, list<string> unassigned);
Description - Classify a dataset, returning the binned output along with the raw assignments and the list of sequences that were not assigned.
Inputs - string classifier, list<tuple<string id, string dna_data>> dna_input
Outputs - mapping<string group_id, int count>, string raw_output, list<string> unassigned)

Method name - default_workflow() returns ( workflow);
Description -
Inputs -
Outputs - workflow

Method name - complete_workflow_template() returns (workflow);
Description - Return a workflow that includes all available stages. Not meant (necessarily) for actual execution, but as a comprehensive list of parts for users to use in assembling their own workflows.
Inputs -
Outputs - workflow

Method name - run_pipeline(genomeTO genome_in, workflow workflow) returns (genomeTO genome_out);
Description -
Inputs - genomeTO genome_in, workflow workflow
Outputs - genomeTO

Method name - pipeline_batch_start(list<pipeline_batch_input> genomes, workflow workflow) returns (string batch_id) authentication required;
Description -
Inputs - list<pipeline_batch_input> genomes, workflow workflow
Outputs - string batch_id

Method name - pipeline_batch_status(string batch_id) returns (pipeline_batch_status status) authentication required;
Description -
Inputs - string batch_id
Outputs - pipeline_batch_status status

Method name - pipeline_batch_enumerate_batches() returns (list<tuple<string batch_id, string submit_time>> batches) authentication required;
Description -
Inputs -
Outputs - list<tuple<string batch_id, string submit_time>> batches

Looked at:

README.md 
GenomeAnnotation.spec
genome_annotation/t/script-tests/*
