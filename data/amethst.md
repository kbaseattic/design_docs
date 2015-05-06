Module: amethst

Description: This is a tool for running multiple pipelines and selecting the best result. The application is 
'analysis methods applied to annotation abundance data' so presumably something metagenomics related 
(hence not completely generic).

Data: Shock


Repo: https://github.com/kbase/amethst


Data Sources: ? MG-RAST?


Input Types:

? None in type spec
Inferred input type is a set of parameters for the analysis which operate on 'annotation abundance data'.
Potential types of 'matrix' and 'tree' are commented out in the service source code.

The source code refers to Shock nodes and presumably the code which would operate on specific data fields is e.g. compile_p-values-summary_files.pl,
but alas this code is not part of this module.


Output types:

? None in type spec
Inferred output is the analysis with best performance presumably along with 'annotation abundance' results

The source code refers to Shock nodes and presumably the code which would operate on specific data fields is e.g. compile_p-values-summary_files.pl,
but alas this code is not part of this module.


Methods:

Method Name - amethst
Description - 
Inputs - string commands_list, mapping<string, string> file2shock
Outputs - string job_id
Data hit - Shock

Method Name - status
Description - 
Inputs - string job_id
Outputs - string status
Data hit : Shock

Method Name - results
Description - 
Inputs - string job_id
Outputs - mapping<string, string>
Data hit - Shock

Method Name - delete_job
Description - 
Inputs - string job_id, string shocktoke
Outputs - string results
Data hit - Shock


Looked at:

README.md
amethst.spec
plbin/mg-amethst.pl 
lib/AMETHSTAWE.pm

