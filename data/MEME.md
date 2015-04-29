#MEME  
  
##Are there any external data references outside of KBase?  
No  
  
##Are there any references to data in the central store  
No  
  
##Are there any calls out to shock data?   
No  
  
##Are there any workspace types being used?  
  
### all data types in MEME module  
gremlin> g.V('moduleName', 'MEME').has('nodeType','D').each{ println "* " + it.typeName; println "  * " + it.comment }
* MemeMotif
  * Represents a particular motif found by MEME
string id - KBase ID of MemeMotif
string description - name of motif or number of motif in collection or anything else
int width - width of motif
int sites - number of sites
float llr - log likelihood ratio of motif
float evalue - E-value of motif
string raw_output - part of MEME output file with data about this motif
list<MemeSite> sites - list of sites

@optional description width llr evalue raw_output
* MastHit
  * Represents a particluar MAST hit
string seq_id - name of sequence
string strand - strand ("+" or "-")
string pspm_id - id of MemePSPM
int hit_start - start position of hit
int hit_end - end position of hit
float score - hit score
float hitPvalue - hit p-value

@optional strand hit_start hit_end score hit_pvalue
* MemeSite
  * Represents a particular site from MEME motif description 
string source_sequence_id - ID of sequence where the site was found
int start - position of site start 
float pvalue - site P-value
string left_flank - sequence of left flank
string sequence - sequence of site
string right_flank - sequence of right flank

@optional start pvalue left_flank right_flank
* MastRunParameters
  * Contains parameters of a MAST run
meme_pspm_collection_ref query_ref - query motifs for MAST run
sequence_set_ref target_ref - target sequences for MAST run
string pspm_id - KBase ID of a MemePSPM from the query collection that will be used. When empty string provided, all motifs in the query collection will be used
float mt - value of mt parameter for MAST run

@optional query_ref target_ref pspm_id mt
* MastRunResult
  * Represents result of a single MAST run
string id - KBase ID of MastRunResult
string timestamp - timestamp for creation time of MastRunResult
MastRunParameters params - run parameters
list<MastHit> hits - A list of all hits found by MAST

@optional timestamp hits
* MemeRunResult
  * Represents results of a single MEME run
string id - KBase ID of MemeRunResult
string source_ref - WS reference to source SequenceSet object
string source_id - id of source SequenceSet object
string timestamp - timestamp for creation time of collection
string version - version of MEME like "MEME version 4.9.0 (Release date: Wed Oct  3 11:07:26 EST 2012)"
string input_file_name - name of input file, DATAFILE field of MEME output
string alphabet - ALPHABET field of MEME output (like "ACGT")
string training_set - strings from TRAINING SET section, except DATAFILE and ALPHABET fields
string command_line - command line of MEME run 
string mod - value of mod parameter of MEME run
int nmotifs - value of nmotifs parameter of MEME run
string evt - value of evt parameter of MEME run
string object_function - value of object function parameter of MEME run
int minw - value of minw parameter of MEME run
int maxw - value of maxw parameter of MEME run
float minic - value of minic parameter of MEME run
int wg - value of wg parameter of MEME run
int ws - value of wc parameter of MEME run
string endgaps - value of endgaps parameter of MEME run
int minsites - value of minsites parameter of MEME run
int maxsites - value of maxsites parameter of MEME run
float wnsites - value of wnsites parameter of MEME run
int prob - value of prob parameter of MEME run
string spmap - value of spmsp parameter of MEME run
float spfuzz - value of spfuzz parameter of MEME run
string substring - value of substring parameter of MEME run
string branching - value of branching parameter of MEME run
string wbranch - value of wbranch parameter of MEME run
string prior - value of prior parameter of MEME run
float b - value of b parameter of MEME run
int maxiter - value of maxiter parameter of MEME run
float distance - value of distance parameter of MEME run
int n - value of n parameter of MEME run
int n_cap - value of N parameter of MEME run
string strands - value of strands parameter of MEME run
int seed - value of seed parameter of MEME run
int seqfrac - value of seqfrac parameter of MEME run
string letter_freq - letter frequencies in dataset
string bg_freq - background letter frequencies
list<MemeMotif> motifs - A list of all motifs in a collection
string raw_output - section of MEME output text file (all before motif data)
MemeRunParameters params

@optional source_ref source_id timestamp meme_version input_file_name alphabet training_set command_line mod nmotifs evt object_function minw maxw minic wg ws endgaps minsites maxsites wnsites prob spmap spfuzz substring branching wbranch prior b maxiter distance n n_cap strands seed seqfrac letter_freq bg_freq motifs raw_output
* meme_run_result_ref
  * Represents WS MemeRunResult identifier
@id ws MEME.MemeRunResult
* MemeRunParameters
  * Contains parameters of a MEME run
string mod - distribution of motifs, acceptable values are "oops", "zoops", "anr"
int nmotifs - maximum number of motifs to find
int minw - minumum motif width
int maxw - maximum motif width
int nsites - number of sites for each motif
int minsites - minimum number of sites for each motif
int maxsites - maximum number of sites for each motif
int pal - force palindromes, acceptable values are 0 and 1
int revcomp - allow sites on + or - DNA strands, acceptable values are 0 and 1
sequence_set_ref source_ref - WS reference to source SequenceSet object
string source_id - id of source SequenceSet object

@optional nmotifs minw maxw nsites minsites maxsites pal revcomp source_ref source_id
* MemePSPMCollection
  * Represents collection of MemePSPMs
string id - KBase ID of MotifPSPMMeme
meme_run_result_ref source_ref - WS reference of source object
string timestamp - timestamp for creation time of collection
string description - user's description of the collection
string alphabet - ALPHABET field of MEME output ("ACGT" for nucleotide motifs)
list<MemeMotif> pspms - A list of all MemePSPMs in a collection

@optional source_ref timestamp description
* meme_pspm_collection_ref
  * Represents WS MemePSPMCollection identifier
@id ws MEME.MemePSPMCollection
* sequence_set_ref
  * Represents WS KBaseSequences.SequenceSet identifier
@id ws KBaseSequences.SequenceSet
* TomtomHit
  * Represents a particluar TOMTOM hit
string query_pspm_id - id of query MemePSPM
string target_pspm_id - id of target MemePSPM
int optimal_offset - Optimal offset: the offset between the query and the target motif
float pvalue - p-value
float evalue - E-value
float qvalue - q-value
int overlap - Overlap: the number of positions of overlap between the two motifs.
string query_consensus - Query consensus sequence.
string target_consensus - Target consensus sequence.
string strand - Orientation: Orientation of target motif with respect to query motif.

@optional optimal_offset pvalue evalue qvalue overlap query_consensus target_consensus strand
* TomtomRunResult
  * Represents result of a single TOMTOM run
string id - KBase ID of TomtomRunResult
string timestamp - timestamp for creation time of TomtomRunResult
TomtomRunParameters params - run parameters
list<TomtomHit> hits - A list of all hits found by TOMTOM

@optional timestamp hits
* MemePSPM
  * Represents a position-specific probability matrix fot MEME motif
string id - KBase ID of the matrix object
string source_id - KBase ID of source object
string description - description of motif
string alphabet - ALPHABET field of MEME output ("ACGT" for nucleotide motifs)
int width - width of motif
int nsites - number of sites
float evalue - E-value of motif
list<list<float>> matrix - The letter probability matrix is a table of probabilities where the rows are positions in the motif and the columns are letters in the alphabet. The columns are ordered alphabetically so for DNA the first column is A, the second is C, the third is G and the last is T.

@optional source_id description width nsites evalue
* TomtomRunParameters
  * Contains parameters of a TOMTOM run
meme_pspm_collection_ref query_ref - query motifs for TOMTOM run
meme_pspm_collection_ref target_ref - target motifs for TOMTOM run
string pspm_id - KBase ID of a MemePSPM from the query collection that will be used. When empty string provided, all motifs in the query collection will be used
float thresh - thresh parameter of TOMTOM run, must be smaller than or equal to 1.0 unless evalueTomtom == 1
int evalue - evalue parameter of TOMTOM run (accepable values are "0" and "1")
string dist - value of dist parameter of TOMTOM run (accepable values are "allr", "ed", "kullback", "pearson", "sandelin")
int internal - internal parameter of TOMTOM run (accepable values are "0" and "1")
int min_overlap - value of min-overlap parameter of TOMTOM run. In case a query motif is smaller than minOverlapTomtom specified, then the motif's width is used as the minimum overlap for that query.

@optional query_ref target_ref pspm_id thresh evalue dist internal min_overlap




  
### datatypes used in MEME service from other modules  
  
gremlin> g.V('moduleName', 'MEME').bothE.filter{it.moduleName == 'MEME'}.bothV.filter{it.moduleName != 'MEME'}.dedup.name  
==>D.KBaseSequences.SequenceSet  
  
  
##Are there any other data types being used as an input or output?   
No  
  
  
## Methods and types used in methods  
  
gremlin> g.V('moduleName', 'MEME').has('nodeType','M').each{println it.name + ":" ; it.in.dedup.each{println "\tparam: " + it.name}; it.out.dedup.each{println "\treturn: " + it.name}}  
M.MEME.find_motifs_with_meme_from_ws:  
	param: D.MEME.MemeRunParameters  
M.MEME.compare_motifs_with_tomtom_by_collection:  
	param: D.MEME.MemePSPMCollection  
	param: D.MEME.TomtomRunParameters  
	return: D.MEME.TomtomRunResult  
M.MEME.find_sites_with_mast_by_collection:  
	param: D.MEME.MastRunParameters  
	param: D.MEME.MemePSPMCollection  
	param: D.KBaseSequences.SequenceSet  
	return: D.MEME.MastRunResult  
M.MEME.get_pspm_collection_from_meme_result_from_ws:  
M.MEME.compare_motifs_with_tomtom_job_by_collection_from_ws:  
	param: D.MEME.TomtomRunParameters  
M.MEME.find_motifs_with_meme_job_from_ws:  
	param: D.MEME.MemeRunParameters  
M.MEME.compare_motifs_with_tomtom:  
	param: D.MEME.MemePSPMCollection  
	param: D.MEME.MemePSPM  
	param: D.MEME.TomtomRunParameters  
	return: D.MEME.TomtomRunResult  
M.MEME.find_motifs_with_meme:  
	param: D.MEME.MemeRunParameters  
	param: D.KBaseSequences.SequenceSet  
	return: D.MEME.MemeRunResult  
M.MEME.compare_motifs_with_tomtom_by_collection_from_ws:  
	param: D.MEME.TomtomRunParameters  
M.MEME.get_pspm_collection_from_meme_result_job_from_ws:  
	param: D.MEME.meme_run_result_ref  
M.MEME.find_sites_with_mast_by_collection_from_ws:  
	param: D.MEME.MastRunParameters  
M.MEME.find_sites_with_mast_job_by_collection_from_ws:  
	param: D.MEME.MastRunParameters  
M.MEME.find_sites_with_mast:  
	param: D.MEME.MastRunParameters  
	param: D.KBaseSequences.SequenceSet  
	param: D.MEME.MemePSPM  
	return: D.MEME.MastRunResult  
M.MEME.get_pspm_collection_from_meme_result:  
	param: D.MEME.MemeRunResult  
	return: D.MEME.MemePSPMCollection  
  
  
  

