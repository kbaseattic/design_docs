#Assembly
##Description 
This service deals with Assembly inputs (Read Files), ReferenceAssembly and output of the assembly process.
I think the data is assumed to be primarliy private data brought into the system.
This is a service to assemble genomes and metagenomes with user's choice of assembly software. 
It currently supports more than 20 assemblers and processing modules.
The Assembly process generates KBaseGenomes.ContigSet and an AssemblyReport

##Data
The data is currently being stored in both Shock the Workspace.  

##Owner/Author
Fangfang, Chris Bun

##Repo
https://github.com/kbase/assembly

##Data Sources
* Private Data : Data from outside users.  Read files from potentially different sequencing platforms.
* Workspace
* Assembly service uses Shock as its blob storage appliance
  * see https://github.com/MG-RAST/Shock
  * see https://github.com/MG-RAST/Shock/wiki/API
* Note this has an install of SQL but I do not see it being used anywhere. (no select or insert statements)(So i do not think this is actually used)
  * https://github.com/kbase/assembly/blob/3818c1e6e7efe70d77e9916559b61b57c66f43f4/tools/add-comp.pl (line 276 and 348)
* Mongo - references Mongo in 13 places in the repo.  
  * Keith suspects this may be used for job management.  - see https://github.com/kbase/assembly/blob/4e518dc3611294d0be1824ef3a5db5b9d0ee632c/lib/assembly/metadata.py
  * mongo.db = arast
  * mongo.collection = jobs

##Dependencies
The current deployment first invokes scripts/install_dependencies.sh. 
This will be no longer necessary once a kbase image is built with these dependencies.

##Workspace with Data
Unknown

##Workspace Module
KBaseAssembly

##Types
###Handle
####Description 
A type for storing files in Shock.
####Relationships

####Fields
* hid - handle id
* file_name 
* id - Shock node id?
* type - mime type? sequencing technology?
* url - shock url
* remote_md5 - md5 of the file on shock
* remote_sha1 - unknown

###SingleEndLibrary
####Description
Very basic type that holds a handle to shock.  The single end library reads file is located on shock.
####Relationships
Handle to shock. @metadata ws handle.file_name  @metadata ws handle.type
####Fields 
handle - The Handle object.

###PairedEndLibrary
####Description
Basic type that holds two handles to shock.  The paired end library reads file are located on shock.
####Relationships
Handles to shock. handle_1 and optional handle_2 (if interleaved it will be one file) 
####Fields 
* handle_1 - shock handle to first reads file
* handle_2 - shock handle to second reads file (only filled if the paired end library is interleaved. 
* insert_size_mean - unknown
* insert_size_std_dev - unknown
* interleaved - boolean to indicated if the paired library has its read interleaved in the same file
* read_orientation_outward - boolean to indicate the directionality of the paired end library

###ReferenceAssembly
####Description
Very basic type that holds a handle to shock and the name of the reference assembly.
####Relationships
Handle to shock. @metadata ws handle.file_name  @metadata ws handle.type
####Fields 
handle - The Handle object.
reference_name - name of reference assembly.

###AssemblyReport
####Description
Report of the assembly process.  Generated when assembly is run.
####Fields 
* report - actual reporting string?
* log - running log?
* server_url - the url for the server th job ran on?
* user - user running the job
* job_id - job id of the assembly process

###AssemblyInput
####Description
An object that stores all the input to the assembly job.  It appears to be a top level container object.
####Fields 
* paired_end_libs - list of paired end libraries
* single_end_libs - list of single end libraries
* references - list of reference assemblies
* expected_coverage - float with estimated coverage.  Depth of coverage or a percent of genome coverage?
* estimated_genome_size - in estimated size of the genome
* dataset_prefix
* dataset_description

