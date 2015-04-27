# Data types found in production service repos

---

#Expression
##Description this stores expression data of a variety of different types (microarray, RNA-Seq, Proteomics, q-PCR)

##Methods
These will need to be changed and rewritten.  Currently it is all written in Perl and acesses the data via direct SQL queries against the Central Store.Also many of the methods were geared for searching before search existed.  The search related methods will not be carried over and should be abandoned.  The current outdated methods exist here: https://github.com/kbase/expression/blob/master/lib/Bio/KBase/KBaseExpression/KBaseExpressionImpl.pm
The methonds with a * at the end are the ones that should be rewritten to work against the workspace.

1. Method Name - get_expression_samples_data
  * Description - Based on the list of sample ids it returns a map of samples and their corresponding complex information.  Note this method is the core called by anything that gets expression_samples_data.  The other methods call this method.
  * Inputs - List of SampleIds
  * Outputs - Complex data structure that has a map that goes to the information for each sample. expression_data_samples_map
  * Data hit : CS tables:
    * Sample
    * StrainWithSample 
    * Strain
    * GenomeParentOf
    * Genome
    * PlatformWithSamples
    * Platform
    * HasExpressionSample
    * ExperimentalUnit
    * HasExperimentalUnit
    * ExperimentMeta
    * IsContextOf
    * Environment
    * ProtocolForSample 
    * Protocol
    * SampleHasAnnotations
    * SampleAnnotation
    * OntologyForSample 
    * Ontology
    * SampleInSeries
    * Series
    * SampleAveragedFrom
    * SampleContactPerson
    * Person
    * SampleMeasurements
    * Measurement
    * FeatureMeasuredBy
    * Feature
2. Method Name - get_expression_data_by_samples_and_features *
  * Description - Based on the list of sample ids, list of feature ids and a numerical interpretation it generates a label_data_mapping. 
  * Inputs - List of SampleIds, List of FeatureIds, Numerical interpretation
  * Outputs - label_data_mapping 
    * mapping kbase feature id as the key and measurement as the value
      typedef mapping<feature_id featureID, measurement measurement> data_expression_levels_for_sample; 
    * Mapping from Label (often a sample id, but free text to identif) to DataExpressionLevelsForSample
      typedef mapping<string label, data_expression_levels_for_sample dataExpressionLevelsForSample> label_data_mapping;)
  * Data hit : CS tables:
    * Sample
    * SampleMeasurements
    * Measurement
    * FeatureMeasuredBy
    * Feature
3. Method Name - get_expression_samples_data_by_series_ids
  * Description - Gets the same thing as get_expression_samples_data but gets them by series ids, has an outer map of series ids to the map of corresponding samples.
  * Inputs - List of SeriesIds
  * Outputs - series_expression_data_samples_mapping : a mapping of series ids to their component expressions samples mapping
  * Data hit : CS tables: (SAME AS get_expression_samples_data)
4. Method Name - get_expression_sample_ids_by_series_ids
  * Description - Given a list of series it returns a list of samples associated with those series.
  * Inputs - List of SeriesIds
  * Outputs - List of SampleIds
  * Data hit : CS tables: 
    * Sample
    * SampleInSeries
    * Series
5. Method Name - get_expression_samples_data_by_experimental_unit_ids
  * Description - Gets the same thing as get_expression_samples_data but gets them by experimental unit ids, has an outer map of experimental unit ids to the map of corresponding samples.  This was designed to work with the Gavin's experiment data.  Which has been since scrapped.
  * Inputs - List of Experimental Unit Ids
  * Outputs - mapping of experimental_unit_ids and their corresponding samples data
  * Data hit : CS tables: (SAME AS get_expression_samples_data)
6. Method Name - get_expression_sample_ids_by_experimental_unit_ids
  * Description - Given a list of experimental_unit_ids it returns a list of samples associated with them. This was designed to work with the Gavin's experiment data.  Which has been since scrapped.
  * Inputs - List of ExperimentalUnitIds
  * Outputs - List of SampleIds
  * Data hit : CS tables: 
    * Sample
    * HasExpressionSample
    * ExperimentalUnit
7. Method Name - get_expression_samples_data_by_experimental_meta_ids
  * Description - Gets the same thing as get_expression_samples_data_by_experimental_unit_ids but gets them by experimental meta ids, has an outer map of experimental meta ids to the get_expression_samples_data_by_experimental_unit_ids return values .  This was designed to work with the Gavin's experiment data.  Which has been since scrapped.
  * Inputs - List of Experimental Meta Ids
  * Outputs - mapping of experimental_meta_ids to their corresponding experimental_unit_ids and in turn their corresponding samples data
  * Data hit : CS tables: (SAME AS get_expression_samples_data)
8. Method Name - get_expression_sample_ids_by_experimental_meta_ids
  * Description - Given a list of experimental_metat_ids it returns a list of samples associated with them. This was designed to work with the Gavin's experiment data.  Which has been since scrapped.
  * Inputs - List of ExperimentalMetaIds
  * Outputs - List of SampleIds
  * Data hit : CS tables: 
    * Sample
    * HasExpressionSample
    * ExperimentalUnit
    * HasExperimentalUnit
    * ExperimentMeta
9. Method Name - get_expression_samples_data_by_strain_ids
  * Description - Gets the same thing as get_expression_samples_data but gets them by strain ids, has an outer map of strain ids to the map of corresponding samples.  This was designed to work with the Gavin's strain tables.  Which has been since scrapped.
  * Inputs - List of StrainIds and Sample Type (Controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics)
  * Outputs - mapping of strain_ids and their corresponding samples data
  * Data hit : CS tables: (SAME AS get_expression_samples_data)
10. Method Name - get_expression_sample_ids_by_strain_ids
  * Description - Given a list of strain ids it returns a list of samples associated with them. This was designed to work with the Gavin's strain tables.  Which has been since scrapped.
  * Inputs - List of StrainIds and Sample Type (Controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics)
  * Outputs - List of SampleIds
  * Data hit : CS tables: 
    * Sample
    * StrainWithSample
    * Strain
11. Method Name - get_expression_samples_data_by_genome_ids
  * Description - Gets the same thing as get_expression_samples_data but gets them by genome ids, has an outer map of genome ids to the map of strain_ids, to the corresponding samples.  
  * Inputs - List of GenomeIds, Sample Type (Controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics) and WildTypeOnly (1 = true, 0 = false)
  * Outputs - map of genome ids to the map of strain_ids, to the corresponding samples.  
  * Data hit : CS tables: (SAME AS get_expression_samples_data)
12. Method Name - get_expression_sample_ids_by_genome_ids
  * Description - Given a list of genome ids it returns a list of samples associated with them. 
  * Inputs - List of GenomeIds, Sample Type (Controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics) and WildTypeOnly (1 = true, 0 = false)
  * Outputs - List of SampleIds
  * Data hit : CS tables: 
    * Sample
    * StrainWithSample
    * Strain
    * GenomeParentOf
    * Genome
13. Method Name - get_expression_samples_data_by_ontology_ids
  * Description - Gets the same thing as get_expression_samples_data : Given a list of ontologyIDs, AndOr operator (and requires sample to have all ontology IDs, or sample has to have any of the terms), GenomeId, SampleType ( controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics), wildTypeOnly returns OntologyID(concatenated if Anded) -> ExpressionDataSample
  * Inputs - list of ontologyIDs, AndOr operator (and requires sample to have all ontology IDs, or sample has to have any of the terms), GenomeId, SampleType ( controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics), wildTypeOnly
  * Outputs - map of ontologogy_ids to the corresponding samples.  
  * Data hit : CS tables: (SAME AS get_expression_samples_data)
14. Method Name - get_expression_sample_ids_by_ontology_ids
  * Description - list of ontologyIDs, AndOr operator (and requires sample to have all ontology IDs, or sample has to have any of the terms), GenomeId, SampleType ( controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics), wildTypeOnly returns list of sample_ids 
  * Inputs - list of ontologyIDs, AndOr operator (and requires sample to have all ontology IDs, or sample has to have any of the terms), GenomeId, SampleType ( controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics), wildTypeOnly
  * Outputs - List of SampleIds
  * Data hit : CS tables: 
    * Sample
    * StrainWithSample
    * Strain
    * GenomeParentOf
    * Genome
    * SampleHasAnnotations
    * OntologyForSample
    * Ontology
15. Method Name - get_expression_data_by_feature_ids *
  * Description - given a list of FeatureIDs, a SampleType ( controlled vocabulary : microarray, RNA-Seq, qPCR, or proteomics) and an int indicating WildType Only (1 = true, 0 = false) returns a FeatureSampleMeasurementMapping: {featureID->{sample_id->measurement}}
  * Inputs - List of feature_ids, sample_type, wild_type_only
  * Outputs - FeatureSampleMeasurementMapping: {featureID->{sample_id->measurement}}
  * Data hit : CS tables:
    * Sample
    * SampleMeasurements
    * Measurement
    * FeatureMeasuredBy
    * Feature
    * StrainWithSample
    * Strain
16. Method Name - compare_samples *
  * Description - compares to samples vs one another.  Returns only features shared across both samples.
  * Inputs - Compare samples takes two data structures labelDataMapping  {sampleID or label}->{featureId or label => value}}, the first labelDataMapping is the numerator, the 2nd is the denominator in the comparison. 
  * Outputs - returns a SampleComparisonMapping {numerator_sample_id(or label)->{denominator_sample_id(or label)->{feature_id(or label) -> value}}}
  * Data hit : All data is from the input data structures.
17. Method Name - compare_samples_vs_default_controls
  * Description -  Compares samples vs their default control if the default control is specified.  If the Default control is not specified for a sample, then nothing is returned for that sample.
  * Inputs - Takes a list of sampleIDs 
  * Outputs - SampleComparisonMapping {sample_id ->{denominator_default_control sample_id ->{feature_id -> log2Ratio}}} 
  * Data Hit : CS Tables : 
    * Sample
    * SampleMeasurements
    * Measurement
    * FeatureMeasuredBy
    * Feature
    * DefaultControlSample
18. Method Name - compare_samples_vs_the_average *
  * Description - Compares each numerator sample vs the average of all the denominator sampleIds.  
  * Inputs - Take a list of numerator sample IDs and a list of samples Ids to average for the denominator.
  * Outputs - SampleComparisonMapping {numerator_sample_id->{denominator_sample_id ->{feature_id -> log2Ratio}}}
  * Data Hit : CS Tables : 
    * Sample
    * SampleMeasurements
    * Measurement
    * FeatureMeasuredBy
    * Feature
19. Method Name - get_on_off_calls *
  * Description -  Takes in comparison results.  If the value is >= on_threshold it is deemed on (1), if < off_threshold it is off(-1).  Thresholds normally set to zero
  * Inputs - Takes in comparison results, off threshold, on threshold 
  * Outputs - SampleComparisonMapping {numerator_sample_id(or label)->{denominator_sample_id(or label)->{feature_id(or label) -> on_off_call (possible values 0,-1,1)}}}
20. Method Name - get_top_changers *
  * Description - Returns the top changers from a comparison.
  * Inputs - Takes in comparison results. Direction must equal 'up', 'down', or 'both'.  Count is the number of changers returned in each direction.
  * Outputs - SampleComparisonMapping {numerator_sample_id(or label)->{denominator_sample_id(or label)->{feature_id(or label) -> log2Ratio (note that the features listed will be limited to the top changers)}}}
21. Method Name - get_expression_samples_titles
  * Description - Gets samples titles
  * Inputs - List of Sample IDs.
  * Outputs - Hash (key : SampleID, value: Title of Sample) 
  * Data Hit : CS Tables : 
    * Sample
22. Method Name - get_expression_samples_descriptions
  * Description - Gets samples descriptions
  * Inputs - List of Sample IDs.
  * Outputs - Hash (key : SampleID, value: Description of Sample)
  * Data Hit : CS Tables : 
    * Sample
23. Method Name - get_expression_samples_molecules
  * Description - Gets samples molecules
  * Inputs - List of Sample IDs.
  * Outputs - Hash (key : SampleID, value: Molecules of the Sample) 
  * Data Hit : CS Tables : 
    * Sample
24. Method Name - get_expression_samples_types
  * Description - Gets samples types
  * Inputs - List of Sample IDs.
  * Outputs - Hash (key : SampleID, value: Type of Sample) 
  * Data Hit : CS Tables : 
    * Sample
25. Method Name - get_expression_samples_external_source_ids
  * Description - Gets samples External Source ID
  * Inputs - List of Sample IDs.
  * Outputs - Hash (key : SampleID, value: External Source ID of Sample) 
  * Data Hit : CS Tables : 
    * Sample
26. Method Name - get_expression_samples_original_log2_medians
  * Description - Gets samples original_log2_medians
  * Inputs - List of Sample IDs.
  * Outputs - Hash (key : SampleID, value: original_log2_medians of Sample) 
  * Data Hit : CS Tables : 
    * Sample
27. Method Name - get_expression_series_titles
  * Description - Get Series titles.
  * Inputs - List of SeriesIDs
  * Outputs - a Hash (key : SeriesID, value: Title of Series)
  * Data Hit : CS Tables : 
    * Series
28. Method Name - get_expression_series_summaries
  * Description - Get Series Summaries.
  * Inputs - List of SeriesIDs
  * Outputs - a Hash (key : SeriesID, value: Summary of Series)
  * Data Hit : CS Tables : 
    * Series
29. Method Name - get_expression_series_designs
  * Description - Get Series Summaries.
  * Inputs - List of SeriesIDs
  * Outputs - a Hash (key : SeriesID, value: Design of Series)
  * Data Hit : CS Tables : 
    * Series
30. Method Name - get_expression_series_external_source_ids
  * Description - Get Series External Source IDs.
  * Inputs - List of SeriesIDs
  * Outputs - a Hash (key : SeriesID, value: External Source ID of Series)
  * Data Hit : CS Tables : 
    * Series
31. Method Name - get_expression_sample_ids_by_sample_external_source_ids
  * Description - Gets a list of sample ids based on a list of external sample ids (typically GSMs)
  * Inputs - list of sample external source ids
  * Outputs - a list of sample ids
  * Data Hit : CS Tables : 
    * Sample
32. Method Name - get_expression_sample_ids_by_platform_external_source_ids
  * Description - get sample ids by the platform's external source id (typically GPLs)
  * Inputs - list of platform external source ids
  * Outputs - list of sample ids
  * Data Hit : CS Tables : 
    * Sample
    * PlatformWithSamples
    * Platform
33. Method Name - get_expression_series_ids_by_series_external_source_ids
  * Description - get series ids by the series's external source id (Typically GSEs)
  * Inputs - Takes a list of series external source ids
  * Outputs - a list of series ids
  * Data Hit : CS Tables : 
    * Series
34. Method Name - get_GEO_GSE  (NOT NEEDED ANYMORE)
  * Description - Based on the old uploader of GEO data.  Not used anymore.



I envision the following new methods being done and operating on the workspace objects:
* Visualize Sample
* Visualize Series
* Add annotation
* Get Data By SampleIDs and FeatureIDs
* Visualize ReplicateGroup?
* Not sure what the RNA-Seq people will need.  Currently there are no methods for them in this spec.
* Visualize the expression data for a genome (by samples)
* Visulaize the expression data for a list of features (by samples)
* Compare Samples (define denominator as specific sample or average of a group of samples)
* Average Samples together to make a representative Sample
* Compare Samples vs default controls?
* Determine ON and OFF calls
* Get Top Changers
* Make new sample with original values

##Data
The data is currently being stored in both the Central Store and the Workspace.  They are not dependent on one another.
However for uploading from GEO the current public data pipeline requires getting information from the Genomes and Features in the CS.

##Owner/Author
Jason Baumohl

##Workspace Module
KBaseExpression

##Workspace with Data
KBasePublicExpression

##Repo
https://github.com/kbase/expression

##Data Sources
* GEO : This is the primary source for our public data
* Private Data : Data from outside users
* RNA-Seq Data : Currently From Mike Schatz group
* Central Store : Used currently to upload the GEO data to map the data genomes and their corresponding CDS features.  Uses both direct SQL and CDMI methods.
* Ontologies : EO, PO and ENVO terms
* The plant group has added annotations for specific samples by hand for ontologies and replicate groups. They supply me with this file for uploading the GEO data.

##Module: KBaseExpression

##Types
###ExpressionSeries
####Description
The Expression Series is a collection of ExpressionSamples that are linked together in some sort of study. This maps to a GEO GSE.
####Relationships
It references Genomes and ExpressionSamples (both by ws reference)
####Fields:
* id : Id of the series usually gotten from the id-server for public data
* source_id : Some string representing the source, in the case of GEO it would be the GSE ID
* genome_expression_sample_ids_map : A map in which the Genome ID is the key and the values are an array of corresponding expression samples.
* title
* summary 
* design : Design of the study
* publication_id 
* external_source_date : Date associated with the external source.

###ExpressionSample
####Description
The core expression unit.  This is the data for an individual expression experiment.  This generally maps to a GEO GSM.
####Relationships
It references Genomes, ExpressionPlatforms and ExpressionSeries (although not by WS reference)
Also has ties to Features and Ontologies.
Referenced by ReplicateGroups and ExpressionSamples
####Fields:
* id : Id of the series usually gotten from the id-server for public data
* source_id : Some string representing the source, in the case of GEO it would be the GSM ID
* type : The type of sample.  Ideally a controlled vocabulary - microarray, RNA-Seq, qPCR, or proteomics 
* numerical_interpretation : The type of numerical data stored - Currently the types are Log2 level intensities, Log2 level ratios, Log2 level ratios genomic DNA control, FPKM.  Down the line we may have on off calls.
* description
* title
* data_quality_level : integer that represents how the data was mapped to CDS features.  
  * 1 : The platform ids were resolved using a custom mappings file
  * 2 : Probe sequences were resolved using Blat   (large genomes can not be done this way)
  * 3 : The platform ids were translated using feature aliases 
* original_median : The measurements for a non FPKM sample are normalized so that their median is zero.  This field keeps the orignal median value for the sample if the people want to be able to transform the data back to the original values. 
* external_source_date : Date associated with the external source.
* expression_levels : Map of Feature IDs and their measurement
* genome_id : WS reference to a genome object.
* expression_ontology_terms : a list of ontology objects (EO, PO or ENVO).  Probabyl needs to be changed in the future once ontologies get nailed down.
* platfrom_id : A WS reference to the ExpressionPlatform object (if it exists)
* default_control_sample : currently not being used.  If you want a particular sample as the default control
* averaged_from_samples : currently not being used.  If sample was averaged from other samples, this would be a list of the other samples.
* protocol : A protocol subtype that has a name and description.
* strain : A strain subtype (genome_id, reference_strain, wild_type, description, name)
* persons : a list of people subtypes associated with this sample (email, first_name, last_name, institution)
* molecule : the type of molecule being measured. (can have different values, but typically total RNA, total RNA/total RNA or total RNA/genomic DNA)
* data_source : Typically GEO for microarray data, but could be other places.
* shock_url : A shock url to the read files for RNA-Seq experiments (added by Sri)
* processing_comments : KBase's processing comments
* expression_series_ids : A list of expression series this sample belongs (NOTE not a WS reference, the WS reference is in the other direction)
* characteristics : Free text from GEO file.
* RMA_normalized : An integer if 1 means data was RMA normalized.

###ExpressionPlatform
####Description
The platform that the experiment was run on. Generally for microarray, but potentially some instrument information for other technology types could be stored in this.  This generally maps to a GEO GPL.
####Relationships
It references Genomes.
Referenced by ExpressionSamples
####Fields:
* id : Id of the series usually gotten from the id-server for public data
* source_id : Some string representing the source, in the case of GEO it would be the GPL ID
* genome_id : WS reference to a genome object.
* strain : A strain subtype (genome_id, reference_strain, wild_type, description, name)
* technology : The technology used
* title : If the platform/chip design was testing for a certain thing.

###ExpressionReplicateGroup
####Description
A simple object that stores ws references to Expression samples that are considered to be replicates of one another.
####Relationships
It references ExpressionSamples
####Fields:
* id : Id of the series usually gotten from the id-server for public data
* expression_sample_ids : A list of WS References to ExpressionSamples that are replicates of one another.

###RNASeqSample
####Description
Made by Sri.  An RNA-Seq Sample.
####Relationships
None of the references are WS references. It does have ref_genome, po_id, eo_id.
It does have a shock_url and shock_id, but these are only set up as strings.
####Fields:
* name  
* type
* created
* shock_ref (shock_id and shock_url)A shock url to the read files for RNA-Seq experiments
* metadata
  * paired
  * platform
  * sample_id
  * title
  * source
  * ext_source_date
  * domain
  * ref_genome
  * tissue - a list
  * condition - a list
  * po_id - a list of PO terms
  * eo_id - a list of EO terms

###RNASeqSampleAlignment
####Description
Made by Sri.  Alignment of the RNA-Seq Sample? Nearly identical to RNASeqSample.
####Relationships
None of the references are WS references. It does have ref_genome, po_id, eo_id.
It does have a shock_url and shock_id, but these are only set up as strings.
####Fields:
* name  
* paired
* created
* shock_ref (shock_id and shock_url) A shock url to the read files for RNA-Seq experiments
* metadata
  * paired
  * platform
  * sample_id
  * title
  * source
  * ext_source_date
  * domain
  * ref_genome
  * tissue - a list
  * condition - a list
  * po_id - a list of PO terms
  * eo_id - a list of EO terms

###RNASeqDifferentialExpression
####Description
Made by Sri.  Differential Expression
####Relationships
It does have a shock_url and shock_id, but these are only set up as strings.
####Fields:
* name  
* title
* created
* diff_expression
  *  RNASeqDifferentialExpressionSet - list of RNASeqDifferentialExpressionFiles (contains name, shock_ref(shock_url,shock_id) A shock url to the read files for RNA-Seq experiments

---
---
---
JUST A STARTING OF ASSEMBLY

#Assembly
##This service takes read files and assembles them into contigs.

##Methods

##Data Sources
The data I assume is coming from outside private sources.

##Repo
https://github.com/kbase/assembly

##Module: KbaseAssembly

##Types
###ExpressionSeries
####Description
The Expression Series is a collection of ExpressionSamples that are linked together in some sort of study. This maps to a GEO GSE.
####Relationships
It references Genomes and ExpressionSamples (both by ws reference)
####Fields:
* id : Id of the series usually gotten from the id-server for public data
* source_id : Some string representing the source, in the case of GEO it would be the GSE ID
* genome_expression_sample_ids_map : A map in which the Genome ID is the key and the values are an array of corresponding expression samples.
* title
* summary 
* design : Design of the study
* publication_id 
* external_source_date : Date associated with the external source.
