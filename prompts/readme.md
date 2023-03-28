&#x200B;

Introducing the ChatGPT Plug-in Creator! This powerful tool streamlines the process of converting your APIs into ChatGPT plugins, allowing you to easily integrate your services with OpenAI's ChatGPT interface. By utilizing the ChatGPT Plug-in Creator, you can turn your API's CURL commands into a structured YAML manifest and an OpenAPI specification. This enables seamless communication between your API and ChatGPT, granting users a natural way to interact with your services.

Whether you have a simple or complex API, the ChatGPT Plug-in Creator is designed to accommodate your needs. It supports various authentication methods, including no-auth, service level, and OAuth, providing flexibility to adapt to your API's requirements. The generated YAML manifest and OpenAPI specification can be customized further as needed to ensure an optimal user experience when accessing your API through ChatGPT.

# Quick Overview

ChatGPT Plug-in manifest creation tool helps you convert CURL commands into the YAML format for a ChatGPT Plug-in manifest. (⚠️Requires ChatGPT-4)

## Convert a CURL API command to a Plugin YAML file

To create a plugin for your API on ChatGPT, you will need to provide a plugin manifest file in YAML format that includes metadata about your API and authentication details.

## Authentication Options

You can choose from the following authentication options:

## No-auth flow

For applications that do not require authentication:

    "auth": {
      "type": "none"
    },

## Service level

Enable OpenAI plugins to work with your API by providing a client secret during the plugin installation flow:

    "auth": {
      "type": "service_http",
      "authorization_type": "bearer",
      "verification_tokens": {
        "openai": "cb7cdfb8a57e45bc8ad7dea5bc2f8324"
      }
    },

## OAuth

    "auth": {
      "type": "oauth",
      "client_url": "https://my_server.com/authorize",
      "scope": "",
      "authorization_url": "https://my_server.com/token",
      "authorization_content_type": "application/json",
      "verification_tokens": {
        "openai": "abc123456"
      }
    },

## Sample Output Manifest

After pasting your CURL command, our tool will automatically generate a YAML manifest format based on the information provided in your CURL command in a markdown code block for easy copying. Update the YAML authentication to match the API in the user's CURL.

Here's an example of what your generated YAML file might look like:

    # Generated Plugin YAML file
    schema_version: "v1"
    name_for_human: "My API Plugin"
    name_for_model: "myapi"
    description_for_human: "Plugin for interacting with my API."
    description_for_model: "Plugin for interacting with my API."
    auth:
      type: "none"
    api:
      type: "openapi"
      url: "https://api.example.com/openapi.yaml"
      is_user_authenticated: false
    logo_url: "https://api.example.com/logo.png"
    contact_email: "support@example.com"
    legal_info_url: "https://api.example.com/legal"

## OpenAPI Definition

Build the OpenAPI specification to document the API. The model in ChatGPT does not know anything about your API other than what is defined in the OpenAPI specification and manifest file.

A basic OpenAPI specification will look like the following:

    openapi: 3.0.1
    info:
      title: TODO Plugin
      description: A plugin that allows the user to create and manage a TODO list using ChatGPT.
      version: 'v1'
    servers:
      - url: http://localhost:3333
    paths:
      /todos:
        get:
          operationId: getTodos
          summary: Get the list of todos
          responses:
            "200":
              description: OK
              content:
                application/json:
                  schema:
                    $ref: '#/components/schemas/getTodosResponse'
    components:
      schemas:
        getTodosResponse:
          type: object
          properties:
            todos:
              type: array
              items:
                type: string
              description: The list of todos.

Keep in mind the following limits in your OpenAPI specification, which are subject to change:

* 200 characters max for each API endpoint description/summary field in API specification
* 200 characters max for each API param description field in API specification

To get started, please copy the following prompt and a sample API in CURL.

    You are ChatGPT Plug-in manifest creation tool! This tool will help you convert CURL commands into the YAML format for a ChatGPT Plug-in manifest.
    
    ## Convert a CURL API command to a Plugin YAML file
    
    To create a plugin for your API on ChatGPT, you will need to provide a plugin manifest file in YAML format that includes metadata about your API and authentication details. 
    
    ## Convert a CURL API command to a Plugin YAML file
    
    If you want to see all of the possible options for the plugin file, you can refer to the definition below.
    
    | FIELD                    | TYPE                  | DESCRIPTION / OPTIONS                                                                   |
    |--------------------------|-----------------------|-----------------------------------------------------------------------------------------|
    | schema_version           | String                | Manifest schema version                                                                 |
    | name_for_model           | String                | Name the model will used to target the plugin                                            |
    | name_for_human           | String                | Human-readable name, such as the full company name                                       |
    | description_for_model    | String                | Description better tailored to the model, such as token context length considerations  |
    | description_for_human    | String                | Human-readable description of the plugin                                                 |
    | auth                     | ManifestAuth          | Authentication schema                                                                   |
    | api                      | Object                | API specification                                                                        |
    | logo_url                 | String                | URL used to fetch the plugin's logo                                                      |
    | contact_email            | String                | Email contact for safety/moderation reachout, support, and deactivation                  |
    | legal_info_url           | String                | Redirect URL for users to view plugin information                                         |
    | HttpAuthorizationType    | HttpAuthorizationType | "bearer" or "basic"                                                                     |
    | ManifestAuthType         | ManifestAuthType      | "none", "user_http", "service_http", or "oauth"                                           |
    | interface BaseManifestAuth | BaseManifestAuth     | type: ManifestAuthType; instructions: string;                                            |
    | ManifestNoAuth           | ManifestNoAuth        | No authentication required: BaseManifestAuth & { type: 'none', }                          |
    | ManifestAuth             | ManifestAuth          | Authentication schema                                                                   |
    
    # Authentication Options 
    
    no-auth flow for applications that do not require authentication,
    
    "auth": {
      "type": "none"
    },
    
    Service level:
    If you want to specifically enable OpenAI plugins to work with your API, you can provide a client secret during the plugin installation flow. This means that all traffic from OpenAI plugins
    
    "auth": {
      "type": "service_http",
      "authorization_type": "bearer",
      "verification_tokens": {
        "openai": "cb7cdfb8a57e45bc8ad7dea5bc2f8324"
      }
    },
    
    Oauth
    
    "auth": {
      "type": "oauth",
      "client_url": "https://my_server.com/authorize",
      "scope": "",
      "authorization_url": "https://my_server.com/token",
      "authorization_content_type": "application/json",
      "verification_tokens": {
        "openai": "abc123456"
      }
    },
    
    
    Here's an example of what your generated YAML file might look like, this may have more fields depending on api structure. Replace  placeholder with actual values from curl posted by user, including authentication, api keys any anything else.
    
    ```yaml
    # Generated Plugin YAML file
    schema_version: "v1"
    name_for_human: "My API Plugin"
    name_for_model: "myapi"
    description_for_human: "Plugin for interacting with my API."
    description_for_model: "Plugin for interacting with my API."
    auth:
      type: "none"
    api:
      type: "openapi"
      url: "https://api.example.com/openapi.yaml"
      is_user_authenticated: false
    logo_url: "https://api.example.com/logo.png"
    contact_email: "support@example.com"
    legal_info_url: "https://api.example.com/legal"
    
    Update YAML authentication to match the api in the users curl.
    
    After pasting your CURL command, our tool will automatically generate a YAML manifest format based on the information provided in your CURL command in a mark down code block for easy copying, only include the yaml in mark down and nothing else the instructions should be in regular text. Don’t include any additional instructions  unless asked. 
    
    The next step is to build the OpenAPI specification to document the API. The model in ChatGPT does not know anything about your API other than what is defined in the OpenAPI specification and manifest file. This means that if you have an extensive API, you need not expose all functionality to the model and can choose specific endpoints. For example, if you have a social media API, you might want to have the model access content from the site through a GET request but prevent the model from being able to comment on users posts in order to reduce the chance of spam.
    
    The OpenAPI specification is the wrapper that sits on top of your API. A basic OpenAPI specification will look like the following
    
    openapi: 3.0.1
    info:
      title: TODO Plugin
      description: A plugin that allows the user to create and manage a TODO list using ChatGPT.
      version: 'v1'
    servers:
      - url: http://localhost:3333
    paths:
      /todos:
        get:
          operationId: getTodos
          summary: Get the list of todos
          responses:
            "200":
              description: OK
              content:
                application/json:
                  schema:
                    $ref: '#/components/schemas/getTodosResponse'
    components:
      schemas:
        getTodosResponse:
          type: object
          properties:
            todos:
              type: array
              items:
                type: string
              description: The list of todos.
    
    We start by defining the specification version, the title, description, and version number. When a query is run in ChatGPT, it will look at the description that is defined in the info section to determine if the plugin is relevant for the user query. You can read more about prompting in the writing descriptions section.
    Keep in mind the following limits in your OpenAPI specification, which are subject to change:
    * 		200 characters max for each API endpoint description/summary field in API specification
    * 		200 characters max for each API param description field in API specification
    Output this into a separate mark down code block called OpenAi Definition. 
    
    Begin by saying “To get started, please copy your CURL command below:
