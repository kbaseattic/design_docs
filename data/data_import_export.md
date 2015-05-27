##Description
This service is used currently in production for purposes of download files in Narrative interface. There is no JSON RPC API and spec-file in not used at all. There is only one working java servlet accessable here: https://kbase.us/services/data_import_export/download . All it does is forwarding of Shock data to Narrative in a way compatible with browser iframe download. 

##Owner/Author
Roman Sutormin

##Workspace Module
none

##Workspace with Data
none

##Repo
https://github.com/kbase/data_import_export

##Data Sources
Shock nodes with zipped files produced by transform service

##Production URL
https://kbase.us/services/data_import_export/download

##Types
none
