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
```6