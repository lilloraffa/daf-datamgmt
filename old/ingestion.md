# Ingestion logics in DAF

## Current Status
**Pipeline to be refined:**
- Insert Metadata in the system
- At the metadata level, the system check if a standard schema is associated, and if so it start the conversion check.
- Save the file in the ingestion folder
- (Here decision to take) Option1: an application listens to the folder, anytime there is a new file, it processes it, try to find metadata based on filename/owner. Option2: Use Kafka message to activate the consumer that will process/ingest the dataset.
- (Choosing Option2 from now on): The consumer sends information to the Ingestion application. It does the following:
  - Read the data structure from the input file
  - compare it with the metadata provided when the dataset has been created in the system.
  - If checks are correct, then it prepare the data in the format needed for the ingestion.
  - It saves the data in the path calculated based on the characteristics of the metadata.
  - Returns that the ingestion has been successfully completed, and store the log of the operation. If errors, it store the error info too.



## Phases
Ingestion phases to be translated into microservices.




### Insert the dataset info/metadata
The user send information about the dataset to the system, either via API or a form. The data get saved into the system and this tells DAF that a dataset exists and where it should expect data to be stored into the dataset.   

In this phase, the inclusion of the dataset into the Standard Dataset is managed. In this case, a check of the coherence of the mapping between the incoming dataset and the standard schema is performed.

**Activities:**
- Get metadata & dataset info and save it into DAF.
- Perform the check on the conversion into Standard Schema if needed.
- Save the file into the folder dedicated to the data ingestion. This folder will contain the original dataset as it arrives into the platform, organized into subfolders based on the owner (entity that send the dataset to DAF). Once the file has been sent to the ingestion procedure, the original one gets moved into a 'success' folder or a 'error' one depending on the fact that the ingestion procedure has been completed or not.
- It sends a message to Kafka to say that a new dataset has been created and is ready to be ingested. This activate a consumer that read the file and save it into HDFS (or other datastore) with the mechanism chosen on the basis of the metadata inserted. 2 alternatives: 1. the data are sent directly to Kafka as messages, 2. no Kafka is used, but Nifi directly read from a directory and start the saving procedures.

**Microservices:**
- Save DS Metadata in DAF
- Check if Standard Schema can be implemented (if required)
- Send message to Kafka about a ds that is ready to be inserted (if a file to be inserted is provided), and save the dataset to the input folder as described above.

### Insert the Data into DAF
There may be a number of entry points to ingest data into DAF, all of which have as pre-requisite the existence of DataSet Info in the system (i.e. the "Insert the dataset info/metadata" has been performed already).

As for batch ingestion, user can call a rest api that will manage the upload of the file into the entry point folder and send a Kafka message to tell the consumer that there is a dataset to ingest.
