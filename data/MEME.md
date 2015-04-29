#MEME  
  
##Are there any external data references outside of KBase?  
No  
  
##Are there any references to data in the central store  
No  
  
##Are there any calls out to shock data?   
No  
  
##Are there any workspace types being used?  
  
### all data types in MEME module  
gremlin> g.V('moduleName', 'MEME').has('nodeType','D').each{ println "* " + it.typeName; println "  * " + it.comment.split("\n")[0] }  
* MemeMotif  
  * Represents a particular motif found by MEME  
* MastHit  
  * Represents a particluar MAST hit  
* MemeSite  
  * Represents a particular site from MEME motif description   
* MastRunParameters  
  * Contains parameters of a MAST run  
* MastRunResult  
  * Represents result of a single MAST run  
* MemeRunResult  
  * Represents results of a single MEME run  
* meme_run_result_ref  
  * Represents WS MemeRunResult identifier  
* MemeRunParameters  
  * Contains parameters of a MEME run  
* MemePSPMCollection  
  * Represents collection of MemePSPMs  
* meme_pspm_collection_ref  
  * Represents WS MemePSPMCollection identifier  
* sequence_set_ref  
  * Represents WS KBaseSequences.SequenceSet identifier  
* TomtomHit  
  * Represents a particluar TOMTOM hit  
* TomtomRunResult  
  * Represents result of a single TOMTOM run  
* MemePSPM  
  * Represents a position-specific probability matrix fot MEME motif  
* TomtomRunParameters  
  * Contains parameters of a TOMTOM run  
  
  
  
### datatypes used in MEME service from other modules  
  
gremlin> g.V('moduleName', 'MEME').bothE.filter{it.moduleName == 'MEME'}.bothV.filter{it.moduleName != 'MEME'}.dedup.each{ println "* " + it.name; println "  * " + it.comment.split("\n")[0] }    
* D.KBaseSequences.SequenceSet  
  * Represents set of sequences  
  
##Are there any other data types being used as an input or output?   
No  
  
  
## Methods and types used in methods  

gremlin> g.V('moduleName', 'MEME').has('nodeType','M').each{println "* " + it.name + ":" ; it.in.dedup.each{println "  * param: " + it.name}; it.out.dedup.each{println "  * return: " + it.name}}
* M.MEME.find_motifs_with_meme_from_ws:
  * param: D.MEME.MemeRunParameters
* M.MEME.compare_motifs_with_tomtom_by_collection:
  * param: D.MEME.MemePSPMCollection
  * param: D.MEME.TomtomRunParameters
  * return: D.MEME.TomtomRunResult
* M.MEME.find_sites_with_mast_by_collection:
  * param: D.MEME.MastRunParameters
  * param: D.MEME.MemePSPMCollection
  * param: D.KBaseSequences.SequenceSet
  * return: D.MEME.MastRunResult
* M.MEME.get_pspm_collection_from_meme_result_from_ws:
* M.MEME.compare_motifs_with_tomtom_job_by_collection_from_ws:
  * param: D.MEME.TomtomRunParameters
* M.MEME.find_motifs_with_meme_job_from_ws:
  * param: D.MEME.MemeRunParameters
* M.MEME.compare_motifs_with_tomtom:
  * param: D.MEME.MemePSPMCollection
  * param: D.MEME.MemePSPM
  * param: D.MEME.TomtomRunParameters
  * return: D.MEME.TomtomRunResult
* M.MEME.find_motifs_with_meme:
  * param: D.MEME.MemeRunParameters
  * param: D.KBaseSequences.SequenceSet
  * return: D.MEME.MemeRunResult
* M.MEME.compare_motifs_with_tomtom_by_collection_from_ws:
  * param: D.MEME.TomtomRunParameters
* M.MEME.get_pspm_collection_from_meme_result_job_from_ws:
  * param: D.MEME.meme_run_result_ref
* M.MEME.find_sites_with_mast_by_collection_from_ws:
  * param: D.MEME.MastRunParameters
* M.MEME.find_sites_with_mast_job_by_collection_from_ws:
  * param: D.MEME.MastRunParameters
* M.MEME.find_sites_with_mast:
  * param: D.MEME.MastRunParameters
  * param: D.KBaseSequences.SequenceSet
  * param: D.MEME.MemePSPM
  * return: D.MEME.MastRunResult
* M.MEME.get_pspm_collection_from_meme_result:
  * param: D.MEME.MemeRunResult
  * return: D.MEME.MemePSPMCollection
  
  
  
  
  

