# Terraform Hybrid Connection Bug

The AzureRM Provider's implementation of App Service Hybrid Connection creates an invalid App Service Hybrid Connection. First and foremost, it does not set a necessary key at the App Service Plan level (notes below). Secondly, it tries to use the primary key of the provided shared access policy of the Relay, and not of the Hybrid Connection.

## Links

* Provider Repo= https://github.com/terraform-providers/terraform-provider-azurerm
* Empty SendKeyValue= https://github.com/terraform-providers/terraform-provider-azurerm/blob/master/azurerm/internal/services/web/app_service_hybrid_connection_resource.go#L145
* Original notes= https://raw.githubusercontent.com/JoshuaTheMiller/AzureExperiments/main/APIM/BugNotes.md

## Testing

### Manual Test Steps

*only until I can figure out if I'm correctly using the Acceptance Tests...

### Provider Tests

```sh
make acctests SERVICE='app_service_hybrid_connection_resource' TESTARGS='-run=TestAccAzureRMResourceGroup' TESTTIMEOUT='60m'
```