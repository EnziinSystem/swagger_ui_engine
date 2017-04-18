# SwaggerUiEngine

Include [swagger-ui](https://github.com/swagger-api/swagger-ui) as Rails engine and document your API with simple YAML files.

## Problem

Working on a Rails API, I've wanted to document my endpoints in the clearest and easiest way possible. My goal was to have the documentation separated from the actual code base and to have a web UI version of Swagger for testing and reading it. Using Rails 5 default API, I didn't need to include Grape, so I took a look into some other existing solutions. Most of them were no longer supported (e.g. [swagger_engine](https://github.com/batdevis/swagger_engine) and [swagger-ui_rails](https://github.com/d4be4st/swagger-ui_rails)) or required adding some extra code for the actual documentation (e.g. [swagger-docs](https://github.com/richhollis/swagger-docs)). Also, none of them supported Swagger web UI configuration, so I decided to write and maintain a gem on my own that would allow others to include Swagger web UI as Rails engine and support writing simple documentation in YAML files.

## Swagger UI Version

Swagger UI Version |
------------------ |
2.2.10             |

## Swagger specifications

https://github.com/swagger-api/swagger-spec/blob/master/versions/2.0.md

## Install

Add to Gemfile

```gem 'swagger_ui_engine'```

Add to your config/routes.rb

```mount SwaggerUiEngine::Engine, at: "/api_docs"```

You can place this route under `admin_constraint` or other restricted path.

## Configure

### Swagger URL

Set the path of your json/yaml files in a initializer:

```
#config/initializers/swagger_ui_engine.rb

SwaggerUiEngine.configure do |config|
  config.swagger_url = 'api_docs/swagger.yaml'
end
```

and place your main documentation file under `/public/api_docs` path.

### Config options
Config Name | Swagger parameter name | Description
--- | --- | ---
config.swagger_url | url | The url pointing to `swagger.json` (Swagger 2.0) or the resource listing (earlier versions) as per [OpenAPI Spec](https://github.com/OAI/OpenAPI-Specification/).
config.doc_expansion | docExpansion | Controls how the API listing is displayed. It can be set to 'none' (default), 'list' (shows operations for each resource), or 'full' (fully expanded: shows operations and their details).
config.model_rendering | defaultModelRendering | Controls how models are shown when the API is first rendered. (The user can always switch the rendering for a given model by clicking the 'Model' and 'Model Schema' links.) It can be set to 'model' or 'schema', and the default is 'schema'.
config.request_headers | showRequestHeaders | Whether or not to show the headers that were sent when making a request via the 'Try it out!' option. Defaults to `false`.
config.json_editor | jsonEditor | Enables a graphical view for editing complex bodies.  Defaults to `false`.

### Edit your json/yaml files

You can use [Swagger editor](https://github.com/swagger-api/swagger-editor) to write and validate your Swagger docs.

## License

This project rocks and uses MIT-LICENSE.
