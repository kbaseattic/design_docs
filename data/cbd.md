Module: cbd


Description: The Compression-Based Distance service allows to compute a relative compression based distance between sequences found in different microbial communities.


Data: Shock


Repo: https://github.com/kbase/cbd


Data Sources: Shock/MG-RAST ?


Input Types:

? None in type spec 
Inferred input type is sets of environmental sequences. Sequences are allowed in different formats (including FASTQ).


Output types:

? None in type spec 
Inferred output type is a relative compression-based distance matrix for a set of microbial communities.


Methods:

Method Name - build_matrix 
Description - 
Inputs - BuildMatrixParams input
Outputs - string job_id


Looked at:

README.md
CompressionBasedDistance.spec
cbd-buildmatrix.py
cbd-buildmatrixlocal.py
cbd-filtermatrix.py
cbd-getmatrix.py
cbd-plotmatrix.py
cbd-runjob.py
cbd-url.py
