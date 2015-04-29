#KBaseNetworks  
    
##Are there any external data references outside of KBase?    
No    
    
##Are there any references to data in the central store    
  
CS tables used in SQL queries:  
Association  
AssociationDataset  
AssociationFeature  
Feature  
IsDatasetFor  
IsGroupingOf  
IsInOperon  
IsRegulatorForRegulon  
Regulator  
Regulome  
RegulomeHasGenome  
RegulomeHasRegulon  
RegulomeSource  
Regulon  
RegulonHasOperon  
Source  
    
##Are there any calls out to shock data?     
No    
    
##Are there any workspace types being used?    
    
### all data types in Networks module    
gremlin> g.V('moduleName', 'KBaseNetworks').has('nodeType','D').typeName    
==>dataset_source_ref  
==>Edge  
==>node_type  
==>Interaction  
==>edge_type  
==>Dataset  
==>network_type  
==>boolean  
==>Node  
==>DatasetSource  
==>taxon  
==>InteractionSet  
==>Network  
    
### datatypes used in KBaseNetworks service from other modules    
    
gremlin> g.V('moduleName', 'KBaseNetworks').bothE.filter{it.moduleName == 'KBaseNetworks'}.bothV.filter{it.moduleName != 'KBaseNetworks'}.dedup.name    
gremlin>    
  
  
##Are there any other data types being used as an input or output?     
No    
    
    
## Methods and types used in methods    
    
gremlin> g.V('moduleName', 'KBaseNetworks').has('nodeType','M').each{println it.name + ":" ; it.in.dedup.each{println "\tparam: " + it.name}; it.out.dedup.each{println "\treturn: " + it.name}}  
M.KBaseNetworks.entity2datasets:  
	return: D.KBaseNetworks.Dataset  
M.KBaseNetworks.dataset_source2datasets:  
	param: D.KBaseNetworks.dataset_source_ref  
	return: D.KBaseNetworks.Dataset  
M.KBaseNetworks.build_first_neighbor_network_limted_by_strength:  
	param: D.KBaseNetworks.edge_type  
	return: D.KBaseNetworks.Network  
M.KBaseNetworks.all_network_types:  
	return: D.KBaseNetworks.network_type  
M.KBaseNetworks.build_internal_network:  
	param: D.KBaseNetworks.edge_type  
	return: D.KBaseNetworks.Network  
M.KBaseNetworks.build_internal_network_limited_by_strength:  
	param: D.KBaseNetworks.edge_type  
	return: D.KBaseNetworks.Network  
M.KBaseNetworks.all_dataset_sources:  
	return: D.KBaseNetworks.DatasetSource  
M.KBaseNetworks.build_first_neighbor_network:  
	param: D.KBaseNetworks.edge_type  
	return: D.KBaseNetworks.Network  
M.KBaseNetworks.all_datasets:  
	return: D.KBaseNetworks.Dataset  
M.KBaseNetworks.taxon2datasets:  
	param: D.KBaseNetworks.taxon  
	return: D.KBaseNetworks.Dataset  
M.KBaseNetworks.network_type2datasets:  
	param: D.KBaseNetworks.network_type  
	return: D.KBaseNetworks.Dataset    
    
  

