# dapr-redis-state-query
sample project for Dapr Redis state query running on kind

# prepare

```bash
# prepare kind cluster and deploy resources
$ kind create cluster
$ skaffold run
```

# usage
## use (ordinary) state API

```bash
# port-forward to sidecar HTTP port
$ kubectl port-forward nodeapp-5ddb7b795f-g544s 3500:3500
Forwarding from 127.0.0.1:3500 -> 3500
Forwarding from [::1]:3500 -> 3500
Handling connection for 3500

# request state APIs
$ curl -i -X POST http://localhost:3500/v1.0/state/statestore -H "Content-Type: application/json" -d '[{"key": "hello", "value": {"msg": "Hello, world!"}}]'
HTTP/1.1 204 No Content
Server: fasthttp
Date: Sat, 16 Apr 2022 04:59:54 GMT
Traceparent: 00-7f1acc1a247db2a551fcc80eadce6464-1f83aa42f5a03d2a-00

$ curl -i http://localhost:3500/v1.0/state/statestore/hello
HTTP/1.1 200 OK
Server: fasthttp
Date: Sat, 16 Apr 2022 05:00:26 GMT
Content-Type: application/json
Content-Length: 23
Etag: 1
Traceparent: 00-96ab0b33092966afe851e0555ef0c098-7269c649184081ee-00

{"msg":"Hello, world!"}
```

## use query state API
