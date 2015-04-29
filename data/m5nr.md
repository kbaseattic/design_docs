##Description
The m5nr is a MD5 based non-redundant sequence database that includes both protein and rRNA sequences. The m5nr allows rapid lookup of annotations from different public sources.

##Owner/Author
Jared Bischof, Travis Harrison, Tobias Paczian, Andreas Wilke

##Workspace Module
none

##Workspace with Data
none

##Repo
https://github.com/kbase/m5nr

##Data Sources
not clear (since http://kbase.us/services/m5nr/sources returns empty list)

##Production URL
https://kbase.us/services/m5nr/

##Types
not clear

##REST API Methods
1. Method Name - info
  * Description - Returns description of parameters and attributes.
  * Url - http://kbase.us/services/m5nr
  * HTTP request type - GET
  * Input
    * none
  * Output
    * none
2. Method Name - ontology
  * Description - Return functional hierarchy
  * Url - http://kbase.us/services/m5nr/ontology
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/ontology?source=Subsystems&min_level=level3 (retrieve subsystems hierarchy for the top 3 levels)
  * Input
    * exact, boolean, (options)
    * filter, string, (options)
    * filter_level, cv, (options)
    * min_level, cv, (options)
    * source, cv, (options)
    * version, integer, (options)
  * Output
    * version, integer
    * url, uri
    * data, list
3. Method Name - taxonomy
  * Description - Return organism hierarchy
  * Url - http://kbase.us/services/m5nr/taxonomy
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/taxonomy?filter=Bacteroidetes&filter_level=phylum&min_level=genus (retrieve all class level taxa that belong to Bacteroidetes)
  * Input
    * exact, boolean, (options)
    * filter, string, (options)
    * filter_level, cv, (options)
    * min_level, cv, (options)
    * version, integer, (options)
  * Output
    * version, integer
    * url, uri
    * data, list
4. Method Name - sources
  * Description - Return all sources in M5NR
  * Url - http://kbase.us/services/m5nr/sources
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/sources (retrieve all data sources for M5NR)
  * Input
    * version, integer, (options)
  * Output
    * version, integer
    * url, uri
    * data, list
5. Method Name - accession
  * Description - Return annotation of given source protein ID
  * Url - http://kbase.us/services/m5nr/accession/{id}
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/accession/YP_003268079.1 (retrieve M5NR data for accession ID 'YP_003268079.1')
  * Input
    * id, string, (required)
    * limit, integer, (options)
    * offset, integer, (options)
    * order, string, (options)
    * version, integer, (options)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
6. Method Name - alias
  * Description - Return annotations for alias IDs containing the given text
  * Url - http://kbase.us/services/m5nr/alias/{text}
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/alias/IPR001478 (retrieve M5NR data for db_xref ID 'IPR001478')
  * Input
    * text, string, (required)
    * exact, boolean, (options)
    * limit, integer, (options)
    * offset, integer, (options)
    * order, string, (options)
    * source, string, (options)
    * version, integer, (options)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
7. Method Name - md5
  * Description - Return annotation(s) or sequence of given md5sum (M5NR ID)
  * Url - http://kbase.us/services/m5nr/md5/{id}
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/md5/000821a2e2f63df1a3873e4b280002a8?source=InterPro (retrieve InterPro M5NR data for md5sum '000821a2e2f63df1a3873e4b280002a8')
  * Input
    * id, string, (required)
    * format, cv, (options)
    * limit, integer, (options)
    * offset, integer, (options)
    * order, string, (options)
    * sequence, boolean, (options)
    * source, string, (options)
    * version, integer, (options)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
8. Method Name - function
  * Description - Return annotations for function names containing the given text
  * Url - http://kbase.us/services/m5nr/function/{text}
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/function/sulfatase?source=GenBank (retrieve GenBank M5NR data for function names containing string 'sulfatase')
  * Input
    * text, string, (required)
    * exact, boolean, (options)
    * inverse, boolean, (options)
    * limit, integer, (options)
    * offset, integer, (options)
    * order, string, (options)
    * source, string, (options)
    * version, integer, (options)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
9. Method Name - organism
  * Description - Return annotations for organism names containing the given text
  * Url - http://kbase.us/services/m5nr/organism/{text}
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/organism/akkermansia?source=KEGG (retrieve KEGG M5NR data for organism names containing string 'akkermansia')
  * Input
    * text, string, (required)
    * exact, boolean, (options)
    * inverse, boolean, (options)
    * limit, integer, (options)
    * offset, integer, (options)
    * order, string, (options)
    * source, string, (options)
    * tax_level, cv, (options)
    * version, integer, (options)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
10. Method Name - sequence
  * Description - Return annotation(s) for md5sum (M5NR ID) of given sequence
  * Url - http://kbase.us/services/m5nr/sequence/{text}
  * HTTP request type - GET
  * Example - http://kbase.us/services/m5nr/sequence/MAGENHQWQGSIL?source=TrEMBL (retrieve TrEMBL M5NR data for md5sum of sequence 'MAGENHQWQGSIL')
  * Input
    * text, string, (required)
    * limit, integer, (options)
    * offset, integer, (options)
    * order, string, (options)
    * source, string, (options)
    * version, integer, (options)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
11. Method Name - accession
  * Description - Return annotations of given source protein IDs
  * Url - http://kbase.us/services/m5nr/accession
  * HTTP request type - POST
  * Example - curl -X POST -d '{"order":"function","data":["YP_003268079.1","COG1764"]}' "http://kbase.us/services/m5nr/accession" (retrieve M5NR data for accession IDs 'YP_003268079.1' and 'COG1764' ordered by function)
  * Input
    * data, list, (body)
    * limit, integer, (body)
    * offset, integer, (body)
    * order, string, (body)
    * version, integer, (body)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
12. Method Name - alias
  * Description - Return annotations for aliases containing the given texts
  * Url - http://kbase.us/services/m5nr/alias
  * HTTP request type - POST
  * Example - curl -X POST -d '{"order":"function","data":["IPR001478","TIGR02124"]}' "http://kbase.us/services/m5nr/alias" (retrieve M5NR data for aliases containing string 'IPR001478' and 'TIGR02124')
  * Input
    * data, list, (body)
    * exact, boolean, (body)
    * limit, integer, (body)
    * offset, integer, (body)
    * order, string, (body)
    * source, string, (body)
    * version, integer, (body)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
13. Method Name - md5
  * Description - Return annotations or sequences of given md5sums (M5NR ID)
  * Url - http://kbase.us/services/m5nr/md5
  * HTTP request type - POST
  * Example - curl -X POST -d '{"source":"InterPro","data":["000821a2e2f63df1a3873e4b280002a8","15bf1950bd9867099e72ea6516e3d602"]}' "http://kbase.us/services/m5nr/md5" (retrieve InterPro M5NR data for md5s '000821a2e2f63df1a3873e4b280002a8' and '15bf1950bd9867099e72ea6516e3d602')
  * Input
    * data, list, (body)
    * limit, integer, (body)
    * offset, integer, (body)
    * order, string, (body)
    * sequence, boolean, (body)
    * source, string, (body)
    * version, integer, (body)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
14. Method Name - function
  * Description - Return annotations for function names containing the given texts
  * Url - http://kbase.us/services/m5nr/function
  * HTTP request type - POST
  * Example - curl -X POST -d '{"source":"GenBank","limit":50,"data":["sulfatase","phosphatase"]}' "http://kbase.us/services/m5nr/function" (retrieve top 50 GenBank M5NR data for function names containing string 'sulfatase' or 'phosphatase')
  * Input
    * data, list, (body)
    * exact, boolean, (body)
    * inverse, boolean, (body)
    * limit, integer, (body)
    * md5s, list, (body)
    * offset, integer, (body)
    * order, string, (body)
    * source, string, (body)
    * version, integer, (body)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
15. Method Name - organism
  * Description - Return annotations for organism names containing the given texts
  * Url - http://kbase.us/services/m5nr/organism
  * HTTP request type - POST
  * Example - curl -X POST -d '{"source":"KEGG","order":"accession","data":["akkermansia","yersinia"]}' "http://kbase.us/services/m5nr/organism" (retrieve KEGG M5NR data (ordered by accession ID) for organism names containing string 'akkermansia' or 'yersinia')
  * Input
    * data, list, (body)
    * exact, boolean, (body)
    * inverse, boolean, (body)
    * limit, integer, (body)
    * md5s, list, (body)
    * offset, integer, (body)
    * order, string, (body)
    * source, string, (body)
    * tax_level, cv, (body)
    * version, integer, (body)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
16. Method Name - sequence
  * Description - Return annotations for md5s (M5NR ID) of given sequences
  * Url - http://kbase.us/services/m5nr/sequence
  * HTTP request type - POST
  * Example - curl -X POST -d '{"source":"KEGG","order":"source","data":["MAGENHQWQGSIL","MAGENHQWQGSIL"]}' "http://kbase.us/services/m5nr/sequence" (retrieve M5NR data ordered by source for sequences 'MAGENHQWQGSIL' and 'MAGENHQWQGSIL')
  * Input
    * data, list, (body)
    * limit, integer, (body)
    * offset, integer, (body)
    * order, string, (body)
    * source, string, (body)
    * version, integer, (body)
  * Output
    * next, uri
    * prev, uri
    * version, integer
    * data, list
    * total_count, integer
    * url, uri
    * limit, integer
    * offset, integer
