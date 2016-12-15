**Important**: Dockbit API is under development and has not yet been officially released. The specification below might (and most probably will) change. Follow us on [Twitter](https://twitter.com/dockbit) to get notified about changes to our platform API.

## API format

The API fully follows version 1.0 of the [JSON API](http://jsonapi.org/) specificiation.

## Authorization

In order to authenticate your requests, log in to [Dockbit](https://dockbit.com), navigate to [Account Settings](https://dockbit.com/settings) and copy your personal _API key_. For convenience, let's export it as an environment variable:

```bash
export DOCKBIT_API_KEY=<Paste your API key here>
```

You can now pass the key in the Authorization header as `Authorization: Bearer $DOCKBIT_API_KEY`. See below for example requests.

## API endpoints

The following endpoints are available:

### Deployments

#### Create deployment

**```POST /api/v1/deployments```**

Example request:

```bash
curl -X POST https://dockbit.com/api/v1/deployments \
     -H "Accept: application/vnd.api+json" \
     -H "Authorization: Bearer $DOCKBIT_API_KEY" \
     -H "Content-Type: application/vnd.api+json" \
     -d '{"data":{"type":"deployments","attributes":{"ref":"master"},"relationships":{"pipeline":{"data":{"type":"pipelines","id":"1"}},"team":{"data":{"type":"teams","id":"1"}}}}}'
```

Example response:

```json
{
   "data":{
      "id":"1",
      "type":"deployments",
      "links":{
         "self":"https://dockbit.com/api/v1/deployments/1"
      },
      "attributes":{
         "created-at":"2016-12-15T14:12:07.186Z",
         "number":1,
         "ref":"master",
         "sha":"6e65482258ae81327eaea83ee31fd76a38301be6",
         "stage-ids":[
            "1"
         ]
      },
      "relationships":{
         "creator":{
            "links":{
               "self":"https://dockbit.com/api/v1/deployments/1/relationships/creator",
               "related":"https://dockbit.com/api/v1/deployments/1/creator"
            }
         },
         "pipeline":{
            "links":{
               "self":"https://dockbit.com/api/v1/deployments/1/relationships/pipeline",
               "related":"https://dockbit.com/api/v1/deployments/1/pipeline"
            }
         },
         "team":{
            "links":{
               "self":"https://dockbit.com/api/v1/deployments/1/relationships/team",
               "related":"https://dockbit.com/api/v1/deployments/1/team"
            }
         }
      }
   }
}
```

### Teams

#### List teams

**```GET /api/v1/teams```**

Example request:

```bash
curl https://dockbit.com/api/v1/teams \
     -H "Accept: application/vnd.api+json" \
     -H "Authorization: Bearer $DOCKBIT_API_KEY" \
     -H "Content-Type: application/vnd.api+json"
```

Example response:

```bash
{
   "data":[
      {
         "id":"1",
         "type":"teams",
         "links":{
            "self":"https://dockbit.com/api/v1/teams/1"
         },
         "attributes":{
            "name":"Dockbit"
         },
         "relationships":{
            "pipelines":{
               "links":{
                  "self":"https://dockbit.com/api/v1/teams/1/relationships/pipelines",
                  "related":"https://dockbit.com/api/v1/teams/1/pipelines"
               }
            }
         }
      }
   ]
}
```

#### List team's pipelines

**```GET /api/v1/teams/:team_id/pipelines```**

Example request:

```bash
curl https://dockbit.com/api/v1/teams/1/pipelines \
     -H "Accept: application/vnd.api+json" \
     -H "Authorization: Bearer $DOCKBIT_API_KEY" \
     -H "Content-Type: application/vnd.api+json"
```

Example response:

```bash
{
   "data":[
      {
         "id":"1",
         "type":"pipelines",
         "links":{
            "self":"https://dockbit.com/api/v1/pipelines/1"
         },
         "relationships":{
            "team":{
               "links":{
                  "self":"https://dockbit.com/api/v1/pipelines/1/relationships/team",
                  "related":"https://dockbit.com/api/v1/pipelines/1/team"
               }
            },
            "deployments":{
               "links":{
                  "self":"https://dockbit.com/api/v1/pipelines/1/relationships/deployments",
                  "related":"https://dockbit.com/api/v1/pipelines/1/deployments"
               }
            }
         }
      }
   ]
}
```

## Help

If you need any help, have a specific feature request in mind, or found a bug, please open an issue or [contact us](https://dockbit.com/site/contact). 🤗
