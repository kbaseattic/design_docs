Module: cbd

Description: The Compression-Based Distance service uses the relative compression of combined and individual datasets to quantify overlaps between microbial communities and builds a distance matrix of the results.

Data: Shock

Repo: https://github.com/kbase/cbd

Data Sources: Shock

Input Types: A set of sequence files for the microbial community. Sequences are allowed in multiple formats (including FASTQ).

Output types: A CSV file with the distance matrix.

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
