#MEME  
  
##Are there any external data references outside of KBase?  
No  
  
##Are there any references to data in the central store  
No  
  
##Are there any calls out to shock data?   
No  
  
##Are there any workspace types being used?  
  
### all data types in MEME module  
gremlin> g.V('moduleName', 'MEME').has('nodeType','D').typeName  
==>MemeMotif  
==>MastHit  
==>MemeSite  
==>MastRunParameters  
==>MastRunResult  
==>MemeRunResult  
==>meme_run_result_ref  
==>MemeRunParameters  
==>MemePSPMCollection  
==>meme_pspm_collection_ref  
==>sequence_set_ref  
==>TomtomHit  
==>TomtomRunResult  
==>MemePSPM  
==>TomtomRunParameters  
  
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
  
  
  

