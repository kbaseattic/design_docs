#Trees Service (KBaseTrees)
##Description: This service provides a set of methods for querying, manipulating, and analyzing multiple sequence alignments and phylogenetic trees.  It also has functions to build alignments and trees.

Note that some of the methods are implemented in Java (where all
current development is taking place) and other methods are forwarded
to an older implementation of the service that's written in Perl.
I note which is which under each method, below.  Only a few of the
methods are currently accessible through the Narrative interface.

##Data
* Public genomes required for some methods to work are stored in the KBasePublicGenomesV3 workspace.
* Central Store data are used, through the CDMI and ERDB APIs
* Shock, through the MG-RAST REST API

##Owners/Authors
Michael Sneddon, Fangfang Xia, Keith Keller, Matt Henderson, Dylan Chivian, Roman Sutormin

##Workspace Module
KBaseTrees

##Workspace with Data
KBasePublicGenomesV3

##Repo
https://github.com/kbase/trees

##Data Sources
* Central Store Tables Used: Tree, HasTreeAttribute, IsBuiltFromAlignment, IsTreeFrom, Alignment, WasAlignedBy, HasAlignmentAttribute, IncludesAlignmentRow, AlignmentRow, ContainsAlignedProtein, Feature, IsProteinFor, Genome, IsOwnedBy, IsAlignmentRowIn, ProteinSequence, IsProteinFor, IsAlignedProteinComponentOf, IsUsedToBuildTree
* Shock - Sequences belonging to a given MG-RAST sample ID are needed for the compute_abundance_profile method

##Third Party Software used
* RPS-BLAST version 2.2.29, from the BLAST+ package at NCBI
* ClustalW version 2.1
* Muscle version 3.8.31
* T-coffee version 10.00.r1613
* Probcons version 1.12
* Mafft version 7.157
* Uclust, version not specified

##Dependencies
* Workspace
* Central Store, through CDMI and ERDB APIs
* MG-RAST REST API

##Module: KBaseTrees

##Types
###Tree
####Description
A Tree stores a single phylogenetic tree.  Could represent either a gene tree or species tree.
####Relationships
Can optionally contain references to all the following types of objects: Genome in workspace, Genome in CS, Feature in CS, Protein Sequence MD5 in CS
####Fields:
(not documented further; node_id is a string)
* string name;
* string description;
* string type;
* newick_tree tree;
* mapping \<string,string\> tree_attributes;
* mapping \<node_id,label\> default_node_labels;
* mapping \<node_id,mapping\<ref_type,list\<ws_obj_id\>\>\> ws_refs;
* mapping \<node_id,mapping\<ref_type,list\<kbase_id\>\>\> kb_refs;
* list \<node_id\> leaf_list;

###TreeDecoration
####Description
These data are used for drawing (visualizing) a tree.
####Relationships
Refers to a single Tree object in the workspace.
####Fields:
(not documented further)
* ws_tree_id tree_id;
* string viz_title;
* list\<string\> string_dataset_labels;
* list\<string\> string_dataset_viz_types;
* list\<string\> int_dataset_labels;
* list\<string\> int_dataset_viz_types;
* list\<string\> float_dataset_labels;
* list\<string\> float_dataset_viz_types;
* mapping\<tree_elt_id,list\<viz_val_string\>\> tree_val_list_string;
* mapping\<tree_elt_id,list\<viz_val_int\>\> tree_val_list_int;
* mapping\<tree_elt_id,list\<viz_val_float\>\> tree_val_list_float;
* mapping\<tree_node_id,collapsed_node_flag\> collapsed_by_node;
* mapping\<tree_node_id,substructure\> substructure_by_node;
* string rooted_flag;
* node_id alt_root_id;

###MSA
####Description
A multiple sequence alignment, either protein or DNA.
####Relationships
Can optionally contain references to all the following types of objects: Genome in workspace, Genome in CS, Feature in CS, Protein Sequence MD5 in CS
####Fields:
(some not documented, but may be evident based on the name)
* name
* description
* sequence_type : 'protein' in case sequences are amino acids, 'dna' in ca
se of nucleotides.
* int alignment_length : number of columns in alignment.
* mapping\<row_id, sequence\> alignment : mapping from sequence id to aligned sequence.
* mapping \<row_id, trim_info\> trim_info;
* mapping \<string,string\> alignment_attributes;
* list\<row_id\> row_order : list of sequence ids defining alignment order (optional). 
* mapping \<node_id,label\> default_row_labels;
* mapping \<node_id,mapping\<ref_type,list\<ws_obj_id\>\>\> ws_refs;
* mapping \<node_id,mapping\<ref_type,list\<kbase_id\>\>\> kb_refs;
* ws_alignment_id parent_msa_ref : reference to parental alignment object to which this object adds some new aligned sequences (it could be useful in case of profile alignments where you don't need to insert new gaps in or iginal msa).

###MSASetElement
####Description
An element in a collection of MSAs.  
####Relationships
Contains either (i.e., exclusively) a reference to a MSA in the WS, or an encapsulated MSA.
####Fields:
* mapping\<string, string\> metadata;
* ws_alignment_id : a reference to a MSA in the workspace, if data is null.
* MSA data : an encapsulated MSA, if ref is null.

###MSASet
####Description
A collection of MSAs.  
####Relationships
Contains list of MSASetElements
####Fields:
* string description;
* list\<MSASetElement\> elements;

###TreeMetaData
####Description
Metadata associated with a tree.
####Relationships
Optionally refers to an alignment in the CS
####Fields:
* kbase_id alignment_id : if this tree was built from an alignment, this provides that alignment id
* string type : the type of tree; possible values currently are "sequence_alignment" and "genome" for trees either built from a sequence alignment, or imported directly indexed to genomes.
* string status : set to 'active' if this is the latest built tree for a particular gene family
* timestamp date_created : time at which the tree was built/loaded in seconds since the epoch
* string tree_contruction_method : the name of the software used to construct the tree
* string tree_construction_parameters : any non-default parameters of the tree construction method
* string tree_protocol : simple free-form text which may provide additional details of how the tree was built
* int node_count : total number of nodes in the tree
* int leaf_count : total number of leaf nodes in the tree (generally this cooresponds to the number of sequences)
* string source_db : the source database where this tree originated, if one exists
* string source_id : the id of this tree in an external database, if one exists

###AlignmentMetaData
####Description
Metadata associated with an alignment
####Relationships
Optionally refers to trees in the CS
####Fields:
* list\<kbase_id\> tree_ids : the set of trees that were built from this alignment
* string status : set to 'active' if this is the latest alignment for a particular set of sequences
* string sequence_type : indicates what type of sequence is aligned (e.g. protein vs. dna)
* boolean is_concatenation : true if the alignment is based on the concatenation of multiple non-contiguous sequences, false if each row cooresponds to exactly one sequence (possibly with gaps)
* timestamp date_created : time at which the alignment was built/loaded in seconds since the epoch
* int n_rows : number of rows in the alignment
* int n_cols : number of columns in the alignment
* string alignment_construction_method : the name of the software tool used to build the alignment
* string alignment_construction_parameters : set of non-default parameters used to construct the alignment
* string alignment_protocol : simple free-form text which may provide additional details of how the alignment was built
* string source_db : the source database where this alignment originated, if one exists
* string source_id : the id of this alignment in an external database, if one exists


##Methods

1. Method Name - replace_node_names [Java]
  * Description - Given a tree in newick format, replace the node names indicated as keys in the 'replacements' mapping with new node names indicated as values in the 'replacements' mapping.  Matching is EXACT and will not handle regular expression patterns.
  * Inputs - a tree encoded as a string (Newick format), and a mapping of replacements
  * Outputs - a tree encoded as a string (Newick format)
  * Data hit : none

2. Method Name - remove_node_names_and_simplify [Java]
  * Description - Given a tree in newick format, remove the nodes with the given names indicated in the list, and simplify the tree.  Simplifying a tree involves removing unnamed internal nodes that have only one child, and removing unnamed leaf nodes.  During the removal process, edge lengths (if they exist) are conserved so that the summed end to end distance between any two nodes left in the tree will remain the same.
  * Inputs - a tree encoded as a string (Newick format), and a list of nodes to delete
  * Outputs - a tree encoded as a string (Newick format)
  * Data hit : none

3. Method Name - merge_zero_distance_leaves [Java]
  * Description - Some KBase trees keep information on canonical feature ids, even if they have the same protein sequence in an alignment.  In these cases, some leaves with identical sequences will have zero distance so that information on canonical features is maintained.  Often this information is not useful, and a single example feature or genome is sufficient.  This method will accept a tree in newick format (with distances) and merge all leaves that have zero distance between them (due to identical sequences), and keep arbitrarily only one of these leaves.
  * Inputs - a tree encoded as a string (Newick format)
  * Outputs - a tree encoded as a string (Newick format)
  * Data hit : none

4. Method Name - extract_leaf_node_names [Java]
  * Description - Given a tree in newick format, list the names of the leaf nodes.
  * Inputs - a tree encoded as a string (Newick format)
  * Outputs - a list of leaf node names
  * Data hit : none

5. Method Name - get_node_count [Java]
  * Description - Given a tree, return the total number of nodes, including internal nodes and the root node.
  * Inputs - a tree encoded as a string (Newick format)
  * Outputs - an integer with the number of nodes
  * Data hit : none

6. Method Name - get_leaf_count [Java]
  * Description - Given a tree, return the total number of leaf nodes, (internal and root nodes are ignored).  When the tree was based on a multiple sequence alignment, the number of leaves will match the number of sequences that were aligned.
  * Inputs - a tree encoded as a string (Newick format)
  * Outputs - an integer with the number of leaf nodes
  * Data hit : none

7. Method Name - get_tree [Perl]
  * Description - Returns a tree from the CS as a string (Newick format)
  * Inputs - an ID of a tree in the CS, and a list of options for how the metadata should be encoded
  * Outputs - a tree encoded as a string (Newick format)
  * Data hit : CS tables: Tree, IsBuiltFromAlignment, Alignment, IsAlignmentRowIn, AlignmentRow, ContainsAlignedProtein, ProteinSequence, IsProteinFor

8. Method Name - get_alignment [Perl]
  * Description - Returns an alignment from the CS as a string (FASTA format)
  * Inputs - an ID of an alignment in the CS, and a list of options for how the metadata should be encoded
  * Outputs - an alignment encoded as a string FASTA format)
  * Data hit : CS tables: AlignmentRow, IsAlignmentRowIn, ContainsAlignedProtein

9. Method Name - get_tree_data [Perl]
  * Description - gets metadata from the CS for a list of tree IDs.
  * Inputs - a list of CS Tree IDs
  * Outputs - a mapping of CS IDs to TreeMetaData objects
  * Data hit : CS tables: Treed, Tree, IsBuiltFromAlignment

10. Method Name - get_alignment_data [Perl]
  * Description - gets metadata from the CS for a list of alignment IDs.
  * Inputs - a list of CS Alignment IDs
  * Outputs - mapping of CS IDs to AlignmentMetaData objects
  * Data hit : CS tables: Alignment, WasAlignedBy, IsBuiltFromAlignment

11. Method Name - get_tree_ids_by_feature [Perl]
  * Description - Given a list of feature ids in kbase, the protein sequence of each feature (if the sequence exists) is identified and used to retrieve all trees by ID that were built using the given protein seqence.
  * Inputs - a list of CS Feature IDs
  * Outputs - a list of CS Tree IDs
  * Data hit : CS tables: IsBuiltFromAlignment, Alignment, IsAlignmentRowIn, AlignmentRow, ContainsAlignedProtein, ProteinSequence, IsProteinFor

12. Method Name - get_tree_ids_by_protein_sequence [Perl]
  * Description - Given a list of kbase ids of a protein sequences (their MD5s), retrieve the tree ids of trees that were built based on these sequences.
  * Inputs - a list of CS Protein Sequence (MD5) IDs
  * Outputs - a list of CS Tree IDs
  * Data hit : CS tables: IsBuiltFromAlignment, Alignment, IsAlignmentRowIn, AlignmentRow, ContainsAlignedProtein

13. Method Name - get_alignment_ids_by_feature [Perl]
  * Description - Given a list of feature ids in kbase, the protein sequence of each feature (if the sequence exists) is identified and used to retrieve all alignments by ID that were built using the given protein seqence.
  * Inputs - a list of CS Feature IDs
  * Outputs - a list of CS Alignment IDs
  * Data hit : CS tables: IncludesAlignmentRow, AlignmentRow, ContainsAlignedProtein, ProteinSequence, IsProteinFor

14. Method Name - get_alignment_ids_by_protein_sequence [Perl]
  * Description - Given a list of kbase ids of a protein sequences (their MD5s), retrieve the alignment ids of alignments that were built based on these sequences.
  * Inputs - a list of CS Protein Sequence (MD5) IDs
  * Outputs - a list of CS Alignment IDs
  * Data hit : CS tables: IncludesAlignmentRow, AlignmentRow, ContainsAlignedProtein

15. Method Name - get_tree_ids_by_source_id_pattern [Perl]
  * Description - This method searches for a tree having a source ID that matches the input pattern (regexp)
  * Inputs - a regexp string
  * Outputs - a list of lists of CS Tree ids
  * Data hit : CS tables: Tree

16. Method Name - import_tree_from_cds [Java]
  * Description - Import phylogenetic tree data from the Central Data Store to the Workspace (both tree and alignment data)
  * Inputs - a set of parameters:
    * kbase_id tree_id;
    * load_alignment_for_tree : if true, load the alignment that was used to build the tree (default = false)
    * string ws_tree_name;
    * mapping \<string,string\> additional_tree_ws_metadata;
    * string ws_alignment_name;
    * mapping \<string,string\> additional_alignment_ws_metadata;
    * boolean link_nodes_to_best_feature;
    * boolean link_nodes_to_best_genome;
    * boolean link_nodes_to_best_genome_name;
    * boolean link_nodes_to_all_features;
    * boolean link_nodes_to_all_genomes;
    * boolean link_nodes_to_all_genome_names;
    * default label : one of protein_md5, feature, genome, genome_species
  * Outputs - a list of metadata objects describing the WS objects created
  * Data hit : CS tables: Tree, HasTreeAttribute, IsBuiltFromAlignment, IsTreeFrom, Alignment, WasAlignedBy, HasAlignmentAttribute, IncludesAlignmentRow, AlignmentRow, ContainsAlignedProtein, Feature, IsProteinFor, Genome, IsOwnedBy; WS

17. Method Name - compute_abundance_profile [Perl]
  * Description - Given an input KBase tree built from a sequence alignment, a metagenomic sample, and a protein family, this method will tabulate the number of reads that match to every leaf of the input tree.  Uses MG-RAST.
  * Inputs - 
    * kbase_id tree_id;
    * string protein_family_name;
    * string protein_family_source;
    * string metagenomic_sample_id;
    * int percent_identity_threshold;
    * int match_length_threshold;
    * string mg_auth_key;
  * Outputs - 
    * mapping \<string,int\> abundances;
    * int n_hits;
    * int n_reads;
  * Data hit : gets MG sequences using the MG-RAST REST API.  CS Tables: ProteinSequence, IsAlignedProteinComponentOf, AlignmentRow, IsAlignmentRowIn, Alignment, IsUsedToBuildTree

18. Method Name - filter_abundance_profile [Perl]
  * Description - Filters one or more abundance profiles
  * Inputs - 
    * A mapping of strings (profile names) to profiles (a map of feature_ids to log2 normalized abundance values)
    * float cutoff_value;
    * boolean use_cutoff_value;
    * float cutoff_number_of_records;
    * boolean use_cutoff_number_of_records;
    * string normalization_scope;
    * string normalization_type;
    * string normalization_post_process;
  * Outputs - A mapping of strings (profile names) to profiles (a map of feature_ids to log2 normalized abundance values)
  * Data hit : none

19. Method Name - draw_html_tree [Perl]
  * Description - Given a tree in Newick format, render it in HTML/JAVASCRIPT and return the page as a string.
  * Inputs - a tree encoded as a string (Newick format)
  * Outputs - a HTML string used to draw the tree
  * Data hit : none

20. Method Name - construct_species_tree [Java, used in Methods insert_genomeset_into_species_tree_generic and insert_set_of_genomes_into_species_tree_generic]
  * Description - Builds a new species tree from Genome objects in the WS
  * Inputs - 
    * list\<genome_ref\> new_genomes : (optional) the list of genome references to use in constructing a tree; either new_genomes or genomeset_ref field should be defined.
    * ws_genomeset_id genomeset_ref : (optional) reference to genomeset object; either new_genomes or genomeset_ref field should be defined.
    * string out_workspace;
    * string out_tree_id;
    * int use_ribosomal_s9_only;
    * int nearest_genome_count;
  * Outputs - the job ID, a string.
  * Data hit : WS only

21. Method Name - construct_multiple_alignment [Java]
  * Description - Builds a new multiple alignment from sequences or from objects in the WS
  * Inputs - 
    * gene_sequences - (optional) the mapping from gene ids to their sequences; either gene_sequences or featureset_ref should be defined.
    * featureset_ref - (optional) reference to FeatureSet object; either gene_sequences or featureset_ref should be defined.
    * alignment_method - (optional) alignment program, one of: Muscle, Clustal, ProbCons, T-Coffee, Mafft (default is Clustal).
    * is_protein_mode - (optional) 1 in case sequences are amino acids, 0 in case of nucleotides (default value is 1).
    * out_workspace - (required) the workspace to deposit the completed alignment
    * out_msa_id - (optional) the name of the newly constructed msa (will be random if not present or null)
  * Outputs - the job ID, a string.
  * Data hit : WS only

22. Method Name - construct_tree_for_alignment [Java]
  * Description - Builds a tree from a MSA object
  * Inputs - 
    * msa_ref - (required) reference to MSA input object.
    * tree_method - (optional) tree construction program, one of 'Clustal' (Neighbor-joining approach) or 'FastTree' (where Maximum likelihood is used), (default is 'Clustal').
    * min_nongap_percentage_for_trim - (optional) minimum percentage of non-gapped positions in alignment column, if you define this parameter in 50, then columns having less than half non-gapped letters are trimmed (default value is 0 - it means no trimming at all). 
    * out_workspace - (required) the workspace to deposit the completed tree
    * out_tree_id - (optional) the name of the newly constructed tree (will be random if not present or null)
  * Outputs - the job ID, a string.
  * Data hit : WS only

23. Method Name - find_close_genomes [Java]
  * Description - Find list of references to public genomes similar to query.
  * Inputs - 
    * query_genome - (required) query genome reference
    * max_mismatch_percent - (optional) defines maximum mismatch percentage when compare aminoacids from user genome with public genomes (defualt value is 5).
  * Outputs - a list of Genome WS references
  * Data hit : WS only

24. Method Name - guess_taxonomy_path [Java]
  * Description - Search for taxonomy path from closely related public genomes (approach similar to find_close_genomes).
  * Inputs - query genome reference
  * Outputs - a string with the taxonomy path
  * Data hit : WS only

25. Method Name - build_genome_set_from_tree [Java, used in Method build_genome_set_from_tree_generic]
  * Description - Build a GenomeSet object from a tree
  * Inputs - tree_ref, a reference to a Tree in the WS
  * Outputs - a GenomeSet WS ref
  * Data hit : WS only
