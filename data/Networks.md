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
gremlin> g.V('moduleName', 'KBaseNetworks').has('nodeType','D').each{ println "* " + it.typeName; println "  * " + it.comment.split("\n")[0] }  
* dataset_source_ref  
  * The name of a dataset that can be accessed as a source for creating a network  
* Edge  
  * Represents an edge in a network.  
* node_type  
  * Type of node in a network  
* Interaction  
  * Represents a single entity-entity interaction  
* edge_type  
  * Type of edge in a network  
* Dataset  
  * Represents a particular dataset.  
* network_type  
  * Type of network that can be created from a dataset  
* boolean  
  * A boolean. 0 = false, other = true.  
* Node  
  * Represents a node in a network.  
* DatasetSource  
  * Provides detailed information about the source of a dataset.  
* taxon  
  * NCBI taxonomy id  
* InteractionSet  
  * Represents a set of interactions  
* Network  
  * Represents a network  
  
    
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
    
## SQL tables used in methods  
  
### loadDatasets  
select \   
	r.id as DATASET_ID \   
	, r.id as DATASET_NAME \  
	, r.description as DATASET_DESCRIPTION \   
	, "REGULATORY_NETWORK" as DATASET_NETWORKTYPE \  
	, s.id as DATASET_SOURCEREFERENCE \  
	, rhs.to_link as DATASET_TAXONS \  
from Regulome r \  
	join RegulomeSource rs on rs.from_link = r.id \  
	join Source s on rs.to_link = s.id \  
	join RegulomeHasGenome rhs on rhs.from_link = r.id \  
order by DATASET_ID  
  
select id DATASET_ID, id DATASET_NAME, \  
        description DATASET_DESCRIPTION, \  
        association_type DATASET_NETWORKTYPE,  \  
        data_source DATASET_SOURCEREFERENCE, \  
        to_link DATASET_TAXONS \  
from AssociationDataset ds, IsDatasetFor d4 \  
where id = from_link \  
group by id  
  
### getDatasets  
  
select \  
	distinct rhs.from_link as regulomeId \  
from \  
	RegulomeHasRegulon rhs \   
	join RegulonHasOperon rho on rho.from_link = rhs.to_link \  
	join IsInOperon iio on iio.to_link = rho.to_link \  
where \   
	iio.from_link = ?   
  
  
select \  
	distinct rhs.from_link as regulomeId \  
from \   
	RegulomeHasRegulon rhs \   
where \  
	rhs.to_link = ?  
  
  
SELECT distinct ig.from_link \  
FROM AssociationFeature af, IsGroupingOf ig  \  
WHERE ig.to_link = af.from_link and af.to_link = ?  
  
SELECT distinct ig.from_link \  
FROM IsGroupingOf ig  \  
WHERE ig.to_link = ?  
  
  
  
### buildFirstNeighborNetwork  
  
select \  
	iio1.from_link as entityId1 \  
	, iio2.from_link as entityId2 \  
	, iio1.from_link as nodeName1 \  
	, iio2.from_link as nodeName2 \  
	, concat("Co-regulated by ", r.name) as edgeName \   
	, r.type as regulationType \  
from \  
	RegulomeHasRegulon rr \  
	join IsRegulatorForRegulon irfr on irfr.to_link = rr.to_link \  
	join Regulator r on r.id = irfr.from_link \  
	join RegulonHasOperon rho1 on rho1.from_link = rr.to_link \  
	join RegulonHasOperon rho2 on rho2.from_link = rr.to_link \  
	join IsInOperon iio1 on iio1.to_link = rho1.to_link \  
	join IsInOperon iio2 on iio2.to_link = rho2.to_link \  
where \  
	iio1.from_link = ? \  
	and rr.from_link = ? \  
	and iio1.from_link <> iio2.from_link  
  
select \  
	iio1.from_link as entityId1 \  
	, rn.id as entityId2 \  
	, iio1.from_link as nodeName1 \  
	, concat(r.name, " regulon") as nodeName2 \  
	, "regulated by "as edgeName \  
	, 1 as directed \  
from \  
	RegulomeHasRegulon rr \  
	join Regulon rn on rn.id = rr.to_link \  
	join IsRegulatorForRegulon irfr on irfr.to_link = rr.to_link \  
	join Regulator r on r.id = irfr.from_link \  
	join RegulonHasOperon rho1 on rho1.from_link = rr.to_link \  
	join IsInOperon iio1 on iio1.to_link = rho1.to_link \  
where \  
	iio1.from_link = ? \  
	and rr.from_link = ?  
  
select \  
	iio1.from_link as entityId1 \  
	, rn.id as entityId2 \  
	, iio1.from_link as nodeName1 \  
	, concat(r.name, " regulon") as nodeName2 \  
	, "regulated by "as edgeName \  
	, 1 as directed \  
from \  
	RegulomeHasRegulon rr \  
	join Regulon rn on rn.id = rr.to_link \  
	join IsRegulatorForRegulon irfr on irfr.to_link = rr.to_link \  
	join Regulator r on r.id = irfr.from_link \  
	join RegulonHasOperon rho1 on rho1.from_link = rr.to_link \  
	join IsInOperon iio1 on iio1.to_link = rho1.to_link \  
where \  
	rn.id = ? \   
	and rr.from_link = ?  
  
  
SELECT DISTINCT af1.to_link, af2.to_link, f1.source_id, f2.source_id, 'is interact with', af1.strength \  
FROM IsGroupingOf ig, AssociationFeature af1, AssociationFeature af2, Feature f1, Feature f2 \  
WHERE ig.from_link = ? and ig.to_link = af1.from_link and af1.from_link = af2.from_link and (af1.to_link = ? OR af2.to_link = ?) AND af1.to_link <> af2.to_link AND f1.id = af1.to_link AND f2.id = af2.to_link  
  
SELECT DISTINCT af1.to_link, a1.id, f1.source_id, a1.name, 'is member of', af1.strength  \  
FROM IsGroupingOf ig, AssociationFeature af1, Association a1, Feature f1  \  
WHERE ig.from_link = ? and ig.to_link = af1.from_link and af1.to_link = ? AND f1.id = af1.to_link AND af1.from_link = a1.id  
  
SELECT DISTINCT af1.to_link, a1.id, f1.source_id, a1.name, 'is member of', af1.strength  \  
FROM IsGroupingOf ig, AssociationFeature af1, Association a1, Feature f1  \  
WHERE ig.from_link = ? and ig.to_link = af1.from_link and a1.id = ? AND f1.id = af1.to_link AND af1.from_link = a1.id  
  
  
### buildInternalNetwork  
  
select \  
	iio1.from_link as entityId1 \  
	, iio2.from_link as entityId2 \  
	, iio1.from_link as nodeName1 \  
	, iio2.from_link as nodeName2 \  
	, concat("Co-regulated by ", r.name) as edgeName \   
from \  
	RegulomeHasRegulon rr \  
	join IsRegulatorForRegulon irfr on irfr.to_link = rr.to_link \  
	join Regulator r on r.id = irfr.from_link \  
	join RegulonHasOperon rho1 on rho1.from_link = rr.to_link \  
	join RegulonHasOperon rho2 on rho2.from_link = rr.to_link \  
	join IsInOperon iio1 on iio1.to_link = rho1.to_link \  
	join IsInOperon iio2 on iio2.to_link = rho2.to_link \  
where \  
	iio1.from_link in (%s) \  
	and iio2.from_link in (%s) \  
	and rr.from_link = ? \  
	and iio1.from_link < iio2.from_link  
  
  
select \  
	iio1.from_link as entityId1 \  
	, rn.id as entityId2 \  
	, iio1.from_link as nodeName1 \  
	, concat(r.name, " regulon") as nodeName2 \  
	, "regulated by "as edgeName \  
	, 1 as directed \  
from \  
	RegulomeHasRegulon rr \  
	join Regulon rn on rn.id = rr.to_link \  
	join IsRegulatorForRegulon irfr on irfr.to_link = rr.to_link \  
	join Regulator r on r.id = irfr.from_link \  
	join RegulonHasOperon rho1 on rho1.from_link = rr.to_link \  
	join IsInOperon iio1 on iio1.to_link = rho1.to_link \  
where \  
	iio1.from_link in (%s) \  
	and rn.id in (%s) \  
	and rr.from_link = ?  
  
  
SELECT DISTINCT af1.to_link, af2.to_link, f1.source_id, f2.source_id, 'is interact with', af1.strength \  
FROM IsGroupingOf ig, AssociationFeature af1, AssociationFeature af2, Feature f1, Feature f2 \  
WHERE ig.from_link = ? and ig.to_link =  af1.from_link and af1.from_link = af2.from_link and (af1.to_link IN (%s) AND af2.to_link IN (%s) ) AND af1.to_link < af2.to_link AND f1.id = af1.to_link AND f2.id = af2.to_link  
  
SELECT DISTINCT af1.to_link, a1.id, f1.source_id, a1.name, 'is member of', af1.strength  \  
FROM IsGroupingOf ig, AssociationFeature af1, Association a1, Feature f1  \  
WHERE ig.from_link = ? and ig.to_link = af1.from_link and af1.to_link IN (%s) AND a1.id IN (%s) AND f1.id = af1.to_link AND af1.from_link = a1.id  
  
### buildNetwork  
  
select \  
	iio1.from_link as entityId1 \  
	, iio2.from_link as entityId2 \  
	, iio1.from_link as nodeName1 \  
	, iio2.from_link as nodeName2 \  
	, concat("Co-regulated by ", r.name) as edgeName \   
from \  
	RegulomeHasRegulon rr \  
	join IsRegulatorForRegulon irfr on irfr.to_link = rr.to_link \  
	join Regulator r on r.id = irfr.from_link \  
	join RegulonHasOperon rho1 on rho1.from_link = rr.to_link \  
	join RegulonHasOperon rho2 on rho2.from_link = rr.to_link \  
	join IsInOperon iio1 on iio1.to_link = rho1.to_link \  
	join IsInOperon iio2 on iio2.to_link = rho2.to_link \  
where \  
	rr.from_link = ? \  
	iio1.from_link < iio2.from_link  
  
select \   
	iio1.from_link as entityId1 \  
	, rn.id as entityId2 \  
	, iio1.from_link as nodeName1 \  
	, concat(r.name, " regulon") as nodeName2 \  
	, "regulated by "as edgeName \  
	, 1 as directed \  
from \  
	RegulomeHasRegulon rr \  
	join Regulon rn on rn.id = rr.to_link \  
	join IsRegulatorForRegulon irfr on irfr.to_link = rr.to_link \  
	join Regulator r on r.id = irfr.from_link \  
	join RegulonHasOperon rho1 on rho1.from_link = rr.to_link \  
	join IsInOperon iio1 on iio1.to_link = rho1.to_link \  
where \  
	rr.from_link = ?  
  
  
  
SELECT DISTINCT af1.to_link, af2.to_link, f1.source_id, f2.source_id, 'is interact with', af1.strength \  
FROM IsGroupingOf ig, AssociationFeature af1, AssociationFeature af2, Feature f1, Feature f2 \  
WHERE ig.from_link = ? and ig.to_link =  af1.from_link and af1.from_link = af2.from_link AND af1.to_link < af2.to_link AND f1.id = af1.to_link AND f2.id = af2.to_link order by af1.strength desc limit 500000  
  
  
SELECT DISTINCT af1.to_link, a1.id, f1.source_id, a1.name, 'is member of', af1.strength  \  
FROM IsGroupingOf ig, AssociationFeature af1, Association a1, Feature f1  \  
WHERE ig.from_link = ? and ig.to_link = af1.from_link AND f1.id = af1.to_link AND af1.from_link = a1.id order by af1.strength desc limit 500000  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

