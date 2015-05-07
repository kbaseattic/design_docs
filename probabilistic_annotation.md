Module: probabilistic_annotation

Description: TThe purpose of the Probabilistic Annotation service is to provide users with
alternative annotations for genes, each attached to a likelihood score, and to
translate these likelihood scores into likelihood scores for the existence of
reactions in metabolic models.

Data: WS, Shock, CDS, local

Repo: https://github.com/kbase/probabilistic_annotation

Data Sources: SEED, literature?, CDS, KEGG

Input Types:

This service implements an algorithm from this publication:
[Likelihood-Based Gene Annotations
for Gap Filling and Quality Assessment in Genome-Scale Metabolic
Models](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003882)

Many different data types from different sources are used.

from ProbabilisticAnnotation.spec -

genome_id
feature_id
reaction_id

This implies these data types: genome, genome feature (protein?), chemical reaction

from DataExtractor.py -

# Call the CDMI API to get data needed to run the autorecon algorithm
# Needed data includes:
#
# For likelihood computations:
# - List of substems and the sequences of their members
# - List of OTU organisms
# - Gene neighborhoods for OTU organisms
#
# For optimization:
# - Reactions [only want mass/charge-balanced ones]
# - Metabolites
# -[Growth data? ]

This implies these data types: protein sequence, SEED subsystems, organism/species/taxonomy, OTU, genomic context for gene

from DataParser.py -

# Exception thrown when makeblastdb command failed
# Exception thrown when static database file is missing from Shock.
 # The direct literature-supported feature ID file is a list of feature IDs identified in the
    # literature. 
    
This implies these data types: protein sequence, BLAST db, BLAST output, gene-to-literature mapping


from Imply.py -

# Exception thrown when role not found in roleToTotalProb dictionary

This seems to refer to protein complexes but its unclear what the source of that data is.

# Iterate over complexes and compute complex probabilities from role probabilities.
# Separate out cases where no genes seem to exist in the organism for the reaction
# from cases where there is a database deficiency.

This implies these data types: SEED subsystem, protein sequence, taxonomy, chemical reaction, 'database' in 'database deficiency'?


It is also probable that some form of 'metabolic model' object is used, however its unclear whether this is just the list of molecules and reactions or something more.


from test-python-client.py:

# We also need to put in a mapping and a biochemistry object somewhere.
# To do this, I just create a "dependency workspace" and pull them from there.
 
Based on probabilistic_annotation/client-tests the biochemistry and mapping data is provided locally after a precomputation step (upon deploy?) which generates static local files.

E.g.:
testdefault.biochemistry
testdefault.mapping

Although I don't see where in the client tests these objects get uploaded to a WS.

The input genome data goes to a WS:
wsClient.save_objects( { 'workspace': self._config['test_ws'], 'objects': [ genomeSaveData, contigSetSaveData ] } )




Output types:

for annotate() = ProbAnno object in WS

for calculate() = RxnProbs object in WS



Methods:

Method Name - annotate
Description - Generate alternative annotations for every gene in a genome together with their likelihoods.
Inputs - AnnotateParams input
Outputs - job_id jobid
Data hit - CDS, WS, local?

Method Name - calculate
Description -  Calculate reaction likelihoods from a probabilistic annotation and a template model.
Inputs - CalculateParams input
Outputs - object_metadata output
Data hit - WS, local?

Method Name - get_rxnprobs
Description - Convert a reaction probability object into a human-readable table.
Inputs - GetRxnprobsParams input
Outputs - reaction_probability_list output
Data hit - WS, local?

Method Name - get_probanno
Description - Convert a ProbAnno object into a human-readbale table
Inputs - GetProbannoParams input 
Outputs - roleset_probabilities output
Data hit - WS, local?


Looked at:

README.md 
ProbabilisticAnnotation.spec 
probabilistic_annotation/lib/biokbase/probabilistic_annotation/*
client-tests/*
scripts/*
lib/Bio/KBase/*
