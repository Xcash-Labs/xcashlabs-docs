---
description: This page contains every Wallet RPC call related to DPoPS
  functions.
title: DPoPS Wallet RPC Calls
---

# DPoPS Wallet RPC Calls

## vote

Place your vote for a delegate.

**Alias:** `vote`

### Inputs

-   **delegate_data** --- String\
    Name or public address of the delegate to receive the vote.

-   **amount** --- String\
    The amount or `all`.

### Outputs

-   **vote_status** --- String\
    Status of the vote call.

### Example

``` bash
curl -X POST http://localhost:18285/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"vote","params":{"delegate_data":"DELEGATES_NAME_OR_PUBLIC_ADDRESS","amount":"all"}}' -H 'Content-Type: application/json'
```

``` json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "vote_status": "success"
  }
}
```

------------------------------------------------------------------------

## delegate_register

Register a delegate.

**Alias:** `delegate_register`

### Inputs

-   **delegate_name** --- String\
    Name of the delegate to register.

-   **delegate_IP_address** --- String\
    IP address or domain name of the delegate.

### Outputs

-   **delegate_register_status** --- String\
    Status of the delegate registration call.

### Example

``` bash
curl -X POST http://localhost:18285/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"delegate_register","params":{"delegate_name":"delegate_name_1","delegate_IP_address":"delegate_IP_address_or_domain_name"}}' -H 'Content-Type: application/json'
```

``` json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "delegate_register_status": "success"
  }
}
```

------------------------------------------------------------------------

## delegate_update

Update delegate information.

**Alias:** `delegate_update`

### Inputs

-   **item** --- String\
    Field to update:

    -   `IP_address` --- Delegate IP address\
    -   `about` --- Delegate description\
    -   `website` --- Delegate website\
    -   `team` --- Team information\
    -   `pool_mode` --- Pool mode setting\
    -   `fee_structure` --- Fee structure description\
    -   `server_settings` --- Server configuration details

-   **value** --- String\
    Value of the field to update.

### Outputs

-   **delegate_update_status** --- String\
    Status of the delegate update call.

### Example

``` bash
curl -X POST http://localhost:18285/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"delegate_update","params":{"item":"ITEM","value":"VALUE"}}' -H 'Content-Type: application/json'
```

``` json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "delegate_update_status": "success"
  }
}
```

------------------------------------------------------------------------

## revote

Revote for a delegate.

**Alias:** `revote`

### Inputs

-   **amount** --- String\
    The amount or `all`.

### Outputs

-   **status** --- String\
    Status of the revote call.

### Example

``` bash
curl -X POST http://localhost:18285/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"revote","params":{"amount":"all"}}' -H 'Content-Type: application/json'
```

``` json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "status": "success"
  }
}
```

------------------------------------------------------------------------

## vote_status

Get who the user has voted for.

**Alias:** `vote_status`

### Outputs

-   **status** --- String\
    Delegate the user has voted for.

### Example

``` bash
curl -X POST http://localhost:18285/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"vote_status"}' -H 'Content-Type: application/json'
```

``` json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "status": "success"
  }
}
```
