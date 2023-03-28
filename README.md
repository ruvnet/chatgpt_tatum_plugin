## Tatum ChatGPT Plugin
The Tatum ChatGPT Plugin is an OpenAPI plugin that allows the user to interact with the Tatum API using ChatGPT, including ERC20 and NFT minting operations. It enables users to mint ERC20 tokens and NFTs on specified blockchains by sending requests to the Tatum API.

## Usage
The Tatum ChatGPT Plugin can be used by sending requests to the Tatum API using ChatGPT. The plugin supports two endpoints:

* /blockchain/token/mint: Mint a new ERC20 token on the specified blockchain
* /nft/mint: Mint a new NFT on the specified blockchain

## Authentication
The Tatum ChatGPT Plugin requires authentication to access the Tatum API. Authentication is done using the x-api-key header. The API key is obtained from Tatum and is stored securely in the plugin configuration file.

* url: This parameter specifies the URL of the API Yaml, hosted on your website to which the request is being sent. The URL needs to be updated based on the specific API endpoint being used.

* keys: This parameter refers to the API key used for authentication. The value for this parameter needs to be updated with the user's specific API key provided by Tatum.

* signature_id: This parameter refers to the KMS signature ID used for signing transactions. The value for this parameter needs to be updated with the user's specific signature ID provided by Tatum.

## OpenAPI Specification
The Tatum ChatGPT Plugin uses the OpenAPI 3.0.1 specification. The specification file openapi_tatum.yaml defines the endpoints and parameters for the plugin.

## Contact
For more information or support, please contact Tatum support at support@tatum.io.