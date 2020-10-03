# korgn-proto

Specification of [korgn]'s protocol with [protobuf].


[korgn]: https://github.com/moreal/korgn
[protobuf]: https://github.com/protocolbuffers/protobuf

## Protocol Support

- TCP

## Protocol

### TCP

1. *Client* sends [`RequestTCPTunnel`](#RequestTCPTunnel) message with required parameters to *Server*.
1. *Server* checks that the `RequestTCPTunnel.auth` parameter is valid.
  - If it is invalid, it will send [`ResponseTCPTunnel`](#ResponseTCPTunnel) with and close the connection.
  - If it is valid, then it will open the connection and continue to send received bytes to the *Client*

## Messages 

The all implementations *MUST* encode messages with *[JSON]*.

[JSON]: https://en.wikipedia.org/wiki/JSON

### RequestTCPTunnel

```json
{
    "hostname": "<string>",
    "port": "<uint16>",
    "auth": "<string>"
}
```

### ResponseTCPTunnel

The response of [`RequestTCPTunnel`](#RequestTCPTunnel). See also [ResultCode](#ResultCode)

```json
{
    "result_code": "<enum: ResultCode>",
    "hostname": "<string>",
    "port": "<uint16>"
}
```

### ResultCode

- SUCCESS = 0;
- INVALID_AUTHENTICATION = 1;