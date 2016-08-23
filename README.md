**Important**: Dockbit API is under development and has not yet been officially released. The specification below might (and most probably will) change. Follow us on [Twitter](https://twitter.com/dockbit) to get notified about changes to our platform API.

## Authentication

In order to authenticate your requests, log in to [Dockbit](https://dockbit.com), navigate to [Account Settings](https://dockbit.com/settings) and copy your personal _API key_. For convenience, let's export it as the environment variable:

    export DOCKBIT_API_KEY=<Paste your API key>

You can now pass the Authorization header with the variable. For example, to test you can successfully authenticate, let's play a bit of 🏓

    curl https://dockbit.com/api/ping \
         -H "Accept: application/vnd.dockbit+json; version=1" \
         -H "Authorization: Bearer $DOCKBIT_API_KEY"

```
=> pong
```

## API version

As you might have noticed earlier, the API version was provided as the _Accept_ request-header in this format:

    Accept: application/vnd.dockbit+json; version=1


## JSON format

The API data is formatted as JSON. There is no root element and we use ```snake_case``` for all object keys. For every _POST_ and _PUT_ request, you will need to send the _Content-Type_ header in this format:

    Content-Type: application/json

## API endpoints

The following endpoints are available:

### Deployments

#### Create deployment

**```POST /api/<team_name>/<pipeline_name>/deployments.json```**

Example request:

    curl -X POST https://dockbit.com/api/SpaceCo/rocket-app/deployments.json \
         -H "Accept: application/vnd.dockbit+json; version=1" \
         -H "Authorization: Bearer $DOCKBIT_API_KEY" \
         -H "Content-Type: application/json" \
         -d "{\"ref\":\"master\"}"

Example response:

    {  
       "number":50,
       "ref":"master",
       "sha":"7e73e7bd9bc32e7a2b23a24b084e22325f577743",
       "stage_ids":[  
          "58",
          "62",
          "65",
          "68"
       ],
       "created_at":"2016-08-23T21:31:19.722Z",
       "pipeline_name":"rocket-app",
       "creator_name":"steve"
    }


## Help

If you need help, have a specific feature request or found a bug, please open an issue or [contact us](https://dockbit.com/site/contact). 🤗



