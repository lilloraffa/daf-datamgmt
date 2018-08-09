# DAF vocabularies management
DAF makes heavy use of vocabularies. Vocabularies are tables containing terms and, mostly for internal purposes, 
instructions that are standardized and codified. This may seem too abstract at the moment, but should be clarified as 
you read though.

## DAF controlled vocabularies
Controlled vocabularies are denormalized tables that contains information to control the terms used to express a well 
determined phenomena. Exemples goes from gender ('male', 'female'), to more complex and hierarchically built vocabulary
of territorial classification ('state' -> 'region'-> 'province', etc.)

## DAF internal vocabularies
Internal vocabularies are data structures that DAF needs to works internally. They typically describe a prefixed set of 
choices the user can make, and control what happen after these choices. They are mostly used to control the behavior of
ingestion form, and provide pre-configured templates.

