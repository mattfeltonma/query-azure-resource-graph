# Microsoft Azure Resource Graph Query
This Python script is used to interact with the [Microsoft Azure Resource Graph](https://docs.microsoft.com/en-us/azure/governance/resource-graph/) service to query [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) for information on Azure resources.  It is written using Python 3.6.

## What problem does this solve?
Retrieving information about Azure resources typically involves creating separate resource queries to each [resource provider](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-supported-services) such as storage, network, and compute.  By using the Microsoft Azure Resource Graph queries for properties of resources can be performed without having to make them individually to each resource provider.  The service also supports complex queries using the [Resource Graph query language](https://docs.microsoft.com/en-us/azure/governance/resource-graph/concepts/query-language).

## Requirements

* [Python 3.7](https://www.python.org/downloads/release/python-368/)
* [Microsoft Azure Python SDK](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk)
* [Microsoft Authentication Library (MSAL)](https://docs.microsoft.com/en-us/azure/active-directory/develop/reference-v2-libraries)
* [Pandas](https://pandas.pydata.org/)

## Setup
Clone the repository.

Install the required modules referenced above.

Prior to running the script you will need to create the Azure Active Directory security principal that the script will use.  The script uses the [OAuth 2.0 Client Credentrial Grant flow](https://oauth.net/2/grant-types/client-credentials/) to acquire an OAuth token to access the Resource Graph.  The security principal needs to be granted the permission to access the Resource Graph and have the appropriate RBAC role over the subscription you plan to query.  See the following [Microsoft documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-api-authentication) for instructions.

The script logs to standard output by default and can additionally be configured to write the log to a file.

The results of the query are stored in JSON format in a file with a filename specified by the user at runtime.  This can be imported into a business intelligence tool such as PowerBI for further analysis.  The query must use the [Resource Graph query language](https://docs.microsoft.com/en-us/azure/governance/resource-graph/concepts/query-language).

The Resource Graph is configured to page results if more than 100 records are returned.  The script is configured to handle these paged records and will write the records to the file after all of the returned records have been retrieved.

## Execution
The script requires a parameters file and a filename for the export file be provided as arguments at runtime.  A sample parameters file is included in the repository.

Example: python3 azure-inventory.py --parameterfile parameters.json --exportfile resources.json \[--logfile query.log]


