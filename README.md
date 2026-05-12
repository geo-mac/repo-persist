# Scholarly repository persistence experiments
This repo includes scripts used to query several APIs ,in order to generate data underpinning analyses published in the following forthcoming research paper:

* Macgregor, G. & Davidson, J. (2026) **Examining the persistence of European open repository infrastructure and its diffusion in the scholarly record**. [Journal of publication TBC]. Preprint available: https://doi.org/10.48550/arXiv.2601.04015

Data arising from this work has been deposited in an appropriate research data repository and is available for inspection:

* Macgregor, G. (2025). **Repository persistence data and results of text mining scholarly literature**. University of Glasgow. Available: https://doi.org/10.5525/gla.researchdata.2101

Several machine interfaces were interrogated to gather data. This was performed using a number scripts, all of which are reproduced here and are available for reuse and/or adaptation. All scripts were deployed within [Google Apps Scripts](ttps://developers.google.com/apps-script), writing response data to [Google Sheets](https://support.google.com/docs/topic/9054603), which were then exported as .csv for merging, cleaning, and analysis. An explanation of the methodological motivations for deploying these data sources is provided [in the associated research paper](https://doi.org/10.48550/arXiv.2601.04015). 

## OpenDOAR registry
Three scholarly repository registries were interrogated to generate data, one of which (OpenDOAR) supports a RESTful API. [OpenDOAR](https://opendoar.ac.uk/) data are exposed as JSON objects via the Jisc [Open Policy Finder API](https://openpolicyfinder.jisc.ac.uk/). The script (opendoar-registry) assists in querying and extracting registry data pertaining to European repositories, including key registry data, such as repository name, home URL, OAI-PMH endpoint location, and country code.

Details of data extracted from the remaining two repository registries is described in registry-response-data.csv below.

## HTTP response check
Repository locations identified through registry interrogation had their HTTP status verified. This script (http-response-check)gathers HTTP status request codes for every repository domain URL and its associated OAI-PMH endpoint. [Common HTTP response codes are widely documented by the IETF and IANA](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml). 

## Wayback Machine
A script (wayback-machine) used to query the [Wayback Availability JSON API](https://archive.org/help/wayback_api.php). Used to capture an approximate 'date of decease' for repositories found to be returning unsatisfactory HTTP response codes (gathered using http-response-check). Archived snapshot data on the last available website archive, including archived_snapshot_URL and associated timestamp. 

## Text mining the CORE aggregator
Script written to query the CORE 'Works' API to mine scholarly literature for specific URIs (https://api.core.ac.uk/docs/v3#tag/Works). This script (core-tdm) was deployed to query version 3.0 of the CORE API (using the CORE API Query Language). This script seeks to mine CORE's bibliographic corpus for scholarly works that cite, refer to, or actively use specified repository URIs. Script processes JSON responses from the 'Works' API, logging key bibliographic data elements. This includes work title, authors, documentType, doi, identifiers, id (an internal CORE identifier), oaiIds (OAI identifiers associated with repositories), yearPublished, and depositedDate. Script also processes any full text arising from the fullText element, parsing and extracting in-text references to specified repository URIs, using the URL prefix of repositories with a wildcard. It should be noted that not all works in CORE have full text available for TDM.

UNDER CONSTRUCTION
