# Data Workflow
Moving data from source to the final HD5 file.

## Table of contents:
1. [General workflow from source to data servers](#general-workflow-from-source-to-data-servers)
2. [Workflow from EDW to CSV files](#workflow-from-edw-to-csv-files)
3. [Worflow from MAD3 to MAT files](#worflow-from-mad3-to-mat-files)
4. [Cross-Referencing Bedmaster data with EDW data](#cross-referencing-bedmaster-data-with-edw-data)

### General workflow from source to data servers
The diagram shown below represents the main data flow from source (ICU patients) to data servers (EDW and MAD3).
Bedside monitors record all patient's data (EMR) and send them to both Bedmaster and EPIC. Data is sent to EPIC
with nurse approval, and also, stored in the Electronic Data Warehouse (EDW). 

On the other hand, Bedmaster stores all the continuous information during three months, which can be visualized through Bedmaster App. 
Research CDAC has a server (MAD3) where all Bedmaster data is stored perpetually.

![](https://github.com/mit-ccrg/icu/blob/14-document-how-bedmaster-and-edw-data-move-from-source-to-hd5/images/mad3_workflow.png)

### Workflow from EDW to CSV files
EDW contains all the information from EPIC and other storage sources. Accessing only to the EPIC source is enough to get
all the necessary EMR. Note that data have different formats, from numerical values to images, strings or physician notes. 
One important feature to consider is that numerical data is not continuous (it is not sampled in a high frequency rate),
since the values stored have been previously approved by a nurse or measured by a physician.

The attached diagram shows a general procedure to obtain data from a group of patients. The steps are:

* Obtain the MRN or CSN of those patients. If not known, the information related to their beds and time period of stay can also be used. 

* Build an ADT table by querying its information.

* Cross-reference ADT information with EDW and obtain other patients' data.

![](https://github.com/mit-ccrg/icu/blob/14-document-how-bedmaster-and-edw-data-move-from-source-to-hd5/images/edw_workflow.png?raw=true&s=100)

### Worflow from MAD3 to MAT files
MAD3 contains all the information that Bedmaster stores. In this case, all data is numerical and can be found in a continuous format. 
There exist two types of information: vital signs (`vs`), sampled every two seconds; and waveforms (`wv`), sampled at 240Hz.

The diagram presented below shows an intuitive workflow to get the files with the desired patients' data. The steps are:

* Obtain the MRN or CSN of those patients.

* Query the ADT table or the Patient Bedmaster table. This second table is the important one, as it pairs patients with Bedmaster data.

* Cross-reference Patient Bedmaster table to get the desired files from Bedmaster. 

* Optional: there are files that are not yet converted to `.mat` extension, but they are still in `.stp` format. Thus, process 
those files with the conversion service to obtain `.mat` files. 


![](https://github.com/mit-ccrg/icu/blob/14-document-how-bedmaster-and-edw-data-move-from-source-to-hd5/images/mad3_workflow.png?raw=true&s=100)

### Cross-Referencing Bedmaster data with EDW data
The easiest way to cross-reference both types of data is by patient identification (MRN or CSN). However, Bedmaster 
files in `.mat` format are freed of any PHI. Thereby, the procedure to cross-reference both data-sets is by time period
and bed. The steps are:

* Get time period and bed information from `.mat` Bedmaster files.

* Build an ADT table from EDW by cross-referencing the time period and bed.

* Cross-reference ADT information with EDW and obtain other data from the same patients.

* Create `hd5` file with the whole data.
