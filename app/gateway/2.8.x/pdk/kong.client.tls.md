---
#
#  WARNING: this file was auto-generated by a script.
#  DO NOT edit this file directly. Instead, send a pull request to change
#  https://github.com/Kong/kong/tree/master/autodoc/pdk/ldoc/ldoc.ltp
#  or its associated files
#
title: kong.client.tls
pdk: true
toc: true
---

Client TLS connection module.

 A set of functions for interacting with TLS connections from the client.




## kong.client.tls.request_client_certificate()

Requests the client to present its client-side certificate to initiate mutual
 TLS authentication between server and client.

 This function *requests*, but does not *require* the client to start
 the mTLS process. The TLS handshake can still complete even if the client
 doesn't present a client certificate. However, in that case, it becomes a
 TLS connection instead of an mTLS connection, as there is no mutual
 authentication.

 To find out whether the client honored the request, use
 `get_full_client_certificate_chain` in later phases.


**Phases**

* certificate

**Returns**

1.  `true|nil`:  Returns `true` if request is received, or `nil` if
 request fails.

1.  `nil|err`:   Returns `nil` if the handshake is successful, or an error
 message if it fails.



**Usage**

``` lua
local res, err = kong.client.tls.request_client_certificate()
if not res then
  -- do something with err
end
```



## kong.client.tls.disable_session_reuse()

Prevents the TLS session for the current connection from being reused
 by disabling the session ticket and session ID for the current TLS connection.

**Phases**

* certificate

**Returns**

1.  `true|nil`:  Returns `true` if successful, `nil` if it fails.

1.  `nil|err`:  Returns `nil` if successful, or an error message if it fails.


**Usage**

``` lua
local res, err = kong.client.tls.disable_session_reuse()
if not res then
  -- do something with err
end
```



## kong.client.tls.get_full_client_certificate_chain()

Returns the PEM encoded downstream client certificate chain with the
 client certificate at the top and intermediate certificates
 (if any) at the bottom.

**Phases**

* rewrite, access, balancer, header_filter, body_filter, log

**Returns**

1.  `string|nil`:   Returns a PEM-encoded client certificate if the mTLS
 handshake was completed, or `nil` if an error occurred or the client did
 not present its certificate.

1.  `nil|err`:  Returns `nil` if successful, or an error message if it fails.


**Usage**

``` lua
local cert, err = kong.client.get_full_client_certificate_chain()
if err then
  -- do something with err
end

if not cert then
  -- client did not complete mTLS
end

-- do something with cert
```



## kong.client.tls.set_client_verify()

Overrides the client's verification result generated by the log serializer.

 By default, the `request.tls.client_verify` field inside the log
 generated by Kong's log serializer is the same as the
 [$ssl_client_verify](https://nginx.org/en/docs/http/ngx_http_ssl_module.html#var_ssl_client_verify)
 Nginx variable.

 Only `"SUCCESS"`, `"NONE"`, or `"FAILED:<reason>"` are accepted values.

 This function does not return anything on success, and throws a Lua error
 in case of a failure.


**Phases**

* rewrite, access, balancer

**Usage**

``` lua
kong.client.tls.set_client_verify("FAILED:unknown CA")
```


