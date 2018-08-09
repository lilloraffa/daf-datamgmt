# Ingestion Form DAF ocabularies
## New dataset creation nature
One of the first step of the ingestion form is to declare from which the new dataset will be created. In fact, a user
can create:

- **primitive** dataset: it is created by new external data from the system.
- **derived** dataset: it is created starting from already existing datasets in DAF. At the moment, we will support SQL 
created dataset, and dataset created by applying a Spark procedure.

The JSON schema here: 
