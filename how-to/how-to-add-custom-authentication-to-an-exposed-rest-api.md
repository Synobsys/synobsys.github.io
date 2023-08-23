---
title: How to Add Custom Authentication to an Exposed REST API
---
# {{page.title}}

    This page is under construction

See [Add Custom Authentication to an Exposed REST API](https://success.outsystems.com/documentation/11/extensibility_and_integration/rest/expose_rest_apis/add_custom_authentication_to_an_exposed_rest_api/)

## API Token

When using api token for authentication you need a method to associate api-keys with a consumer user. For this you can create a api key management solution.

To keep the example simple we use site properties to store the api key and the associated user. It is recommended that you create your own api key management solution based on your business needs.

### API Key validation

1. Create a site property:
    * Name: API_Key
    * Description: The "secret" x-api-key that is shared with the api consumer.
    * Data type: Text
1. Create another site property:
    * Name: APIServiceAccountUserName
    * Description: The username that's associated with the API Key
    * Data type: Text
1. Create a Service Action
    * Name: APIKeyValidate
    * Description: Checks if the API Key is valid and retrieves the associated userid when valid.
    * Add an input parameter: APIKey, Data type: Text
    * Add an Output parameter: IsValid Data type: Boolean
    * Add an Output parameter: ConsumerUserId, Data type: User Identifier
1. Add the logic
    * Trim the APIKey
    * Add an if: `APIKey <> "" and APIKey=Site.APIKey`
    * In the false branch set isvalid = false
    * In the true branch add an agregate
    * Add the user entity to the aggregate
    * Add a filter to the aggregate: `User.Username = Site.APIServiceAccountUserName`
    * Add an If `GetUserByUsername.List.Empty`
    * In the true branch set IsValid=False and end
    * In the false branch add an assign
    * Set ConsumerUserId = GetUserByUsername.List.Current.User.Id
    * Set Isvalid = True
    * End

Your action flow should now look like this [APIKeyValidate](#api-key-validation)

### Custom Authentication

Set the API authentication property to custom.
Now the 

## OAuth tokem

    TODO
