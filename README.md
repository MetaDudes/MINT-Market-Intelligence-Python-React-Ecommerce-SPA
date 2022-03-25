# MINT-Market-Intelligence-Python-React-Ecommerce-SPA

## Documentation

### Introduction
Welcome to Mint, the Market Intelligence API! This documentation should help you familiarize yourself with the resources available and how to consume them with HTTP requests. Read through the getting started section before you dive in. Most of your problems should be solved just by reading through it.


### Getting started
Let's make our first API request to the Market Intelligence API!

Open up a terminal and use curl or httpie to make an API request for a resource. In the example below, we're trying to get the first user:

http mint.me/api/users/1/
We'll use httpie for our examples as it displays responses nicely and gives us a whole lot more useful information. If you don't want to download httpie, just use the curl command instead.

Here is the response we get:

HTTP/1.0 200 OK
Content-Type: application/json
{
    "name": "Example User 1",
    "tasks": [
        "https://mint.com/api/tasks/1/",
        "https://mint.com/api/tasks/2/",
        ...
    ],
    "wallets": [
        "https://mint.com/api/wallets/1/",
        "https://mint.com/api/wallets/2/",
        ...
    ],
    "transactions": [
        "https://mint.com/api/transactions/1/",
        "https://mint.com/api/transactions/2/",
        ...
    ],
    "settings": [],
    "url": "https://mint.com/api/users/1/"
}
If your response looks slightly different don't panic. This is probably because more data has been added to Mint since we made this documentation.


### Base URL
The Base URL is the root URL for all of the API, if you ever make a request to Mint and you get back a 404 NOT FOUND response then check the Base URL first.

The Base URL for MINT is:

https://mint.com/api/
The documentation below assumes you are prepending the Base URL to the endpoints in order to make requests.


### Rate limiting
MINT has rate limiting to prevent malicious abuse (as if anyone would abuse Market Intelligence data!) and to make sure our service can handle a potentially large amount of traffic. Rate limiting is done via IP address and is currently limited to 10,000 API request per day. This is enough to request all the data on the website at least ten times over. There should be no reason for hitting the rate limit.


### Authentication
Mint is a completely open API. No authentication is required to query and get data. This also means that we've limited what you can do to just GET-ing the data. If you find a mistake in the data, then tweet the author or email him.


### JSON Schema
All resources support JSON Schema. Making a request to /api/<resource>/schema will give you the details of that resource. This will allow you to programmatically inspect the attributes of that resource and their types.


### Searching
All resources support a search parameter that filters the set of resources returned. This allows you to make queries like:

https://mint.com/api/users/?search=r2

All searches will use case-insensitive partial matches on the set of search fields. To see the set of search fields for each resource, check out the individual resource documentation. For more information on advanced search terms see here.

### Encodings
JSON is the standard data format provided by Mint by default.


### Resources

### Root
The Root resource provides information on all available resources within the API.

Example request:

http https://mint.com/api/
Example response:

HTTP/1.0 200 OK
Content-Type: application/json
{
    "users": "https://mint.com/api/users/",
    "tasks": "https://mint.com/api/tasks/",
    "wallets": "https://mint.com/api/wallets/",
    "transactions": "https://mint.com/api/transactions/",
}
Attributes:

users string -- The URL root for User resources
tasks string -- The URL root for Task resources
wallets string -- The URL root for Wallet resources
transactions string -- The URL root for Transaction resources

People
A User resource is an individual user of the application.

Endpoints

/users/ -- get all the User resources
/users/:id/ -- get a specific User resource
/users/schema/ -- view the JSON schema for this resource
Example request:

http https://mint.com/api/users/1/
Example response:

HTTP/1.0 200 OK
Content-Type: application/json
{
    "name": "Example User 1",
    "tasks": [
        "https://mint.com/api/tasks/1/",
        "https://mint.com/api/tasks/2/",
        ...
    ],
    "wallets": [
        "https://mint.com/api/wallets/1/",
        "https://mint.com/api/wallets/2/",
        ...
    ],
    "transactions": [
        "https://mint.com/api/transactions/1/",
        "https://mint.com/api/transactions/2/",
        ...
    ],
    "settings": [[insert settings attributes here]],
    "url": "https://mint.com/api/users/1/"
}
Attributes:

name string -- The name of this user.
email string -- The email address of this user.
tasks array -- An array of resource URLs for tasks that belong to this user.
wallets array -- An array of resource URLs for wallets that belong to this user.
transactions array -- An array of resource URLs for transactions that belong to this user.
settings array -- An array of settings that belong to this user.
url string -- the hypermedia URL of this resource.
created string -- the ISO 8601 date format of the time that this resource was created.
edited string -- the ISO 8601 date format of the time that this resource was edited.
Search Fields:

name

### Tasks
A Task resource is a single task.

Endpoints

/tasks/ -- get all the Task resources
/tasks/:id/ -- get a specific Task resource
/tasks/schema/ -- view the JSON schema for this resource
Example request:

http https://mint.com/api/tasks/1/
Example response:

HTTP/1.0 200 OK
Content-Type: application/json
{
    "name": "Example Task 1",
    "wallet": "https://mint.com/api/wallets/1/",
    "transaction_network": "Flashbots",
    "transaction_cost": 1.0,
    "contract_address": "insert_contract_address_here",
    "function_name": "insert_function_name_here",
    "function_params": "insert_function_params_here",
    "gas_price_method": "rapid_price",
    "gas_limit_method": "auto",
    "url": "https://mint.com/api/tasks/1/"
}
Attributes:

name string -- The name of this task.
wallet string -- The resource URL of the wallet that belongs to this task.
transaction_network string --  The transaction network for this task: Flashbots or Mainnet.
transaction_cost float -- The amount of ETH sent in the transaction. The cost of mint price of the NFT.
contract_address string -- The contract destination address where transactions will be sent.
function_name string -- This is the function that is going to be called for minting through the contract (ex: mintAll, mint, etc.).
function_params string -- The parameters provided within the mint function (does not include the payable amount of ether).
gas_price_method string -- The price setting method for gas related to this task's transactions: Rapid, Base, or Manual. 
gas_limit_method string -- The price limit setting method for gas: Auto or Manual.
url string -- the hypermedia URL of this resource.
created string -- the ISO 8601 date format of the time that this resource was created.
edited string -- the ISO 8601 date format of the time that this resource was edited.
Search Fields:

name

### Wallets
A Wallet resource is a single wallet.

Endpoints

/wallets/ -- get all the Wallet resources
/wallets/:id/ -- get a specific Wallet resource
/wallets/schema/ -- view the JSON schema for this resource
Example request:

http https://mint.dev/api/wallets/1/
Example response:

HTTP/1.0 200 OK
Content-Type: application/json
{
    "name": "Example Wallet 1",
    "wallet_address": "insert_wallet_address_here",
    "wallet_private_key": "insert_MetaMask_wallet_private_key",
    "balance": 10.0,
    "status": "idle",
    "url": "https://mint.com/api/wallets/1/"
}
Attributes:

name string -- The name of this wallet.
wallet_address string -- The address of this wallet.
wallet_private_key string -- The MetaMask private key for this wallet.
balance float -- The balance of this wallet in ETH.
status string -- The status of this wallet.
url string -- the hypermedia URL of this resource.
created string -- the ISO 8601 date format of the time that this resource was created.
edited string -- the ISO 8601 date format of the time that this resource was edited.
Search Fields:

name

### Transactions
A Transaction resource is a single transaction invoice.

Endpoints

/transactions/ -- get all the Transaction resources
/transactions/:id/ -- get a specific Transaction resource
/transactions/schema/ -- view the JSON schema for this resource
Example request:

http https://mint.com/api/transactions/1/
Example response:

HTTP/1.0 200 OK
Content-Type: application/json

{
    "transaction_id": "insert_uniquely_generated_transaction_id_here",
    "task": "https://mint.com/api/tasks/1/",
    "wallet": "https://mint.com/api/wallets/1/",
    "transaction_network": "Flashbots",
    "transaction_cost": 1.0,
    "contract_address": "insert_contract_address_here",
    "function_name": "insert_function_name_here",
    "function_params": "insert_function_params_here",
    "gas_price_method": "rapid_price",
    "gas_limit_method": "auto",
    "created_at": "insert_datetime_here",
    "updated_at": "insert_datetime_here",
    "url": "https://mint.com/api/transactions/1/"
}
Attributes:

id string -- The uniquely generated id of this transaction.
task string -- Resource URL for the task which this transaction belongs to.
wallet string -- Resource URL for the wallet which this transaction belongs to.
transaction_network string --  The transaction network for this task: Flashbots or Mainnet.
transaction_cost float -- The amount of ETH sent in the transaction. The cost of mint price of the NFT.
contract_address string -- The contract destination address where transactions will be sent.
function_name string -- This is the function that is going to be called for minting through the contract (ex: mintAll, mint, etc.).
function_params string -- The parameters provided within the mint function (does not include the payable amount of ether).
gas_price_method string -- The price setting method for gas related to this task's transactions: Rapid, Base, or Manual. 
gas_limit_method string -- The price limit setting method for gas: Auto or Manual.
created string -- the ISO 8601 date format of the time that this resource was created.
edited string -- the ISO 8601 date format of the time that this resource was edited.
url string -- the hypermedia URL of this resource.
Search Fields:

transaction_id
