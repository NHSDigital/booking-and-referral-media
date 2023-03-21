# RAP repository template

:exclamation: Warning: this repository may contain references internal to NHS England that cannot be accessed publicly

> Describe your project in 1-3 sentences.

This repository contains media for use in the BaRS Implementation guidance. Providing guidance on how to implement BaRS and gain accreditation. The guide is designed for developers, business analysts, product owners and anyone involved at any stage of going live with BaRS.

## Link to publication

[Booking and Referrals Standard Implementation Guidance](https://simplifier.net/guide/nhsbookingandreferralstandard/home)

## Contact
**This repository is maintained by [NHS England Booking and Referral Team](bookingandreferralstandard@nhs.net)**.

## Description

Images and other media is held in this repository to be referenced by other publications for documentation purposes..


You can learn more about project structure and why it's important in the ['project structure and packaging guide'](https://nhsdigital.github.io/rap-community-of-practice/training_resources/python/project-structure-and-packaging/) of the RAP community of practice Github repo, a central source of RAP knowledge.

_You can edit any part of this document. The licence section **must be edited** before publishing this repository publicly. For more information about publishing your project please see the ['how to publish your code in the open' guide](https://nhsdigital.github.io/rap-community-of-practice/implementing_RAP/how-to-publish-your-code-in-the-open/)._


## Project structure

```text
|   .gitignore                        <- Files (& file types) automatically removed from version control for security purposes
|   config.toml                       <- Configuration file with parameters we want to be able to change (e.g. date)
|   environment.yml                   <- Conda equivalent of requirements file
|   requirements.txt                  <- Requirements for reproducing the analysis environment 
|   pyproject.toml                    <- Configuration file containing package build information
|   LICENCE                           <- License info for public distribution
|   README.md                         <- Quick start guide / explanation of your project
|
|   create_publication.py             <- Runs the overall pipeline to produce the publication     
|
+---src                               <- Scripts with functions for use in 'create_publication.py'. Contains project's codebase.
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |
|   +---utils                     <- Scripts relating to configuration and handling data connections e.g. importing data, writing to a database etc.
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       file_paths.py             <- Configures file paths for the package
|   |       logging_config.py         <- Configures logging
|   |       data_connections.py       <- Handles data connections i.e. reading/writing dataframes from SQL Server
|   | 
|   +---processing                    <- Scripts with modules containing functions to process data i.e. clean and derive new fields
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       clean.py                  <- Perform cleaning and wrangling processes 
|   |       derive_fields.py          <- Create new field definitions, columns, derivations.
|   | 
|   +---data_ingestion                <- Scripts with modules containing functions to preprocess read data i.e. perform validation/data quality checks, other preprocessing etc.
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       preprocessing.py          <- Perform preprocessing, for example preparing your data for metadata or data quality checks.
|   |       validation_checks.py      <- Perform validation checks e.g. a field has acceptable values.
|   |
|   +---data_exports
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       write_excel.py            <- Populates an excel .xlsx template with values from your CSV output.
|   |
|
+---templates                         <- Templates for output files
|       publication_template.xlsx
```
