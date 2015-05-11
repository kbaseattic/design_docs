#Protein Info Service (ProteinInfoService)
##Description: The protein info service returns certain protein
annotations about fids, such as domain assignments, operons, and
orthologs.

Note that none these methods are available through the Narrative
interface, and that they depend on a legacy MySQL database from
Microbes Online.  Some of the data (e.g., domains) are available via
other services, such as Gene Families, although the latter service
does not have precalculated domains for public genomes like MO does.

##Data
* Uses the MicrobesOnline MySQL database
* Central Store data are used, through the CDMI API
* Does not use Workspace
* Does not use Shock

##Owners/Authors
Not documented; Steve Chan appears in several comments

##Workspace Module
None

##Workspace with Data
None

##Repo
https://github.com/kbase/protein_info_service

##Data Sources
* MicrobesOnline MySQL database (which has many undocumented third party dependencies)

##Third Party Software used
None

##Dependencies
* Central Store, through CDMI API.  However, it does not actually depend on any CS data; instead, it uses fids_to_genomes, which assumes the CS Feature identifiers given to it are valid and encapsulate valid Genome identifiers.
* MicrobesOnline MySQL direct access
* MO Translation Service, to translate MO locus IDs to/from KBase CS Feature IDs

##Module: ProteinInfoService

##Types
None

##Methods

1. Method Name - fids_to_operons
  * Description - fids_to_operons takes as input a list of feature ids and returns a mapping of each fid to the operon in which it is found. The list of fids in the operon is not necessarily in the order that the fids are found on the genome.  (fids_to_operons is currently not properly implemented.)
  * Inputs - List of CS Feature IDs
  * Outputs - A mapping of Feature IDs to operons (an operon is defined as a list of Feature IDs)
  * Data hit : MO table Locus2Operon

2. Method Name - fids_to_domains
  * Description - fids_to_domains takes as input a list of feature ids, and returns a mapping of each fid to its domains. (This includes COG, even though COG is not part of InterProScan.) 
  * Inputs - List of CS Feature IDs
  * Outputs - A mapping of Feature IDs to domains (domains are defined as IDs in external databases such as COGs that MO has pre-calculated)
  * Data hit : MO tables Fid2Domain, Fid2COG, Locus2Domain, DomainInfo

3. Method Name - fids_to_domain_hits
  * Description - fids_to_domain_hits takes as input a list of feature ids, and returns a mapping of each fid to a list of hits. (This includes COG, even though COG is not part of InterProScan.)
  * Inputs - List of CS Feature IDs
  * Outputs - A mapping of Feature IDs to domain hits (hits are defined as a structure that stores data about the location of the domain in a feature, and the confidence in the annotation)
  * Data hit : MO tables Fid2Domain, Fid2COG, Fid2COGrpsblast, Locus2Domain, DomainInfo

4. Method Name - domains_to_fids
  * Description - domains_to_fids takes as input a list of domain_ids, and returns a mapping of each domain_id to the fids which have that domain. (This includes COG, even though COG is not part of InterProScan.)
  * Inputs - A list of domain IDs from external databases that MO stores annotations to, such as COGs
  * Outputs - A mapping of each domain ID to a list of CS Feature IDs that contain that domain
  * Data hit : MO tables Fid2Domain, Fid2COG, Locus2Domain, DomainInfo

5. Method Name - domains_to_domain_annotations
  * Description - domains_to_domain_annotations takes as input a list of domain_ids, and returns a mapping of each domain_id to its text annotation as provided by its maintainer (usually retrieved from InterProScan, or from NCBI for COG).
  * Inputs - A list of domain IDs from external databases that MO stores annotations to, such as COGs
  * Outputs - A mapping of each domain ID to its description, obtained from an external domain library and stored in MO
  * Data hit : MO tables DomainInfo, COGInfo

6. Method Name - fids_to_ipr
  * Description - fids_to_ipr takes as input a list of feature ids, and returns a mapping of each fid to its IPR assignments. These can come from HMMER or from non-HMM-based InterProScan results.
  * Inputs - List of CS Feature IDs
  * Outputs - A mapping of Feature IDs to domains in Interpro (appears to be a subset of fids_to_domains)
  * Data hit : MO table Locus2Ipr

7. Method Name - fids_to_orthologs
  * Description - fids_to_orthologs takes as input a list of feature ids, and returns a mapping of each fid to its orthologous fids in all genomes.
  * Inputs - List of CS Feature IDs
  * Outputs - A mapping of Feature IDs to a list of orthologous Feature IDs for each one
  * Data hit : MO tables Locus, MOGMember, Position, COG

8. Method Name - fids_to_ec
  * Description - fids_to_ec takes as input a list of feature ids, and returns a mapping of each fid to its Enzyme Commission numbers (EC).
  * Inputs - List of CS Feature IDs
  * Outputs - A mapping of Feature IDs to a list of EC annotations for each one
  * Data hit : MO table Locus2Ec

9. Method Name - fids_to_go
  * Description - fids_to_go takes as input a list of feature ids, and returns a mapping of each fid to its Gene Ontology assignments (GO).
  * Inputs - List of CS Feature IDs
  * Outputs - A mapping of Feature IDs to a list of GO annotations for each one
  * Data hit : MO table Locus2Go

10. Method Name - fid_to_neighbors
  * Description - fid_to_neighbor takes as input a single feature id, and a neighbor score threshold and returns a list of neighbors
  * Inputs - A CS Feature ID, threshold score (float)
  * Outputs - A mapping of neighboring Feature IDs to their neighbor scores.
  * Data hit : MO tables MOGMember, MOGNeighborScores

11. Method Name - fidlist_to_neighbors
  * Description - fidlist_to_neighbors takes as input a list of feature ids, and a minimal neighbor score, and returns a mapping of each fid to its neighbors, based on neighbor score >= threshold
  * Inputs - List of CS Feature IDs, Threshold score
  * Outputs - A mapping of Feature IDs to neighbors (each neighbor is defined as a mapping of neighboring Feature IDs to their neighbor scores)
  * Data hit : MO tables MOGMember, MOGNeighborScores

12. Method Name - fids_to_eukaryotic_orthologs
  * Description - fids_to_eukaryotic_orthologs takes as input a list of feature ids, and returns a mapping of each fid to its orthologous fids.
  * Inputs - List of CS Feature IDs
  * Outputs - A mapping of Feature IDs to a list of orthologous eukaryotic Feature IDs for each one
  * Data hit : MO table FidOrthologs
