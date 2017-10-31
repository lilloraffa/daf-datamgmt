# Programming Note - Migration Ingestion Module

## To Do
- Put in ConvSchema (and in the operational) the indication on how you want to partition data. For now I'm partitioning for TS.
- Make one unique function for saving DS parametrically. In DataInjCsv.
- Add a check on the uri wrt the info inserted.
- When saving the dataset, manage the logging so we can have the full history of what happens
- Fix/expand the data type manager. For now it does not manage complex datatype in avro.


## SchemaMgmt Class
It will manage the coherence check and design the final schema that will be used to perform schema checks and manage info needed to create the final dataframe and save the ds into the right location.

**Strategy:**
Let's keep it as it is for now, so it will still expect the same info as input (convSchema). --> Change ConvSchemaGetter and StdSchemaGetter.

## SchemaGetter
It gets schema information from the corresponding API.
