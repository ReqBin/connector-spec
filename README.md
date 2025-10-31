# ReqBin Connector Spec

This repository defines the HTTP API that the local ReqBin Connector (agent) exposes on localhost or a configured interface. Client (browser or app) calls the agent, and the agent makes HTTP/HTTPS requests to local/private resources and returns the response.

## Goals
- Unify request/response schema across languages (Node, Python, Go, Java).
- Keep the wire protocol stable (versioned under `spec/v1`).
- Security-first defaults (deny by default, explicit allowlist).

## Endpoints (v1)
- `GET /health` → `{ "status": "up" }`
- `GET /version` → `{ "name": "reqbin-connector", "version": "x.y.z" }`
- `POST /v1/fetch` → Performs a single HTTP/HTTPS request to a target URL the agent can reach.

See OpenAPI: `spec/v1/openapi.yaml`  
JSON Schemas: `spec/v1/request.schema.json`, `spec/v1/response.schema.json`

## Security model (summary)
- Only `http:` and `https:` targets.
- Mandatory host/IP validation (loopback, RFC1918, ULA by default; public hosts blocked unless explicitly allowed).
- Optional host/domain/IP allowlists.
- Request size/time limits.
- Response body may be returned as UTF-8 string or Base64 (for binary).

## Versioning
- `spec/v1` is stable once published.
- Backwards-compatible changes are additive only.
- Breaking changes → new `v2`.

## License
MIT
