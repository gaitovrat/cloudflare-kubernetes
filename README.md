# Cloudflare tunnel in kubernetes
## Prerequesties
- Registred domain in cloudflare.
- Generated credentials.json (More info in values.yaml).

## Setup guide
1. Update values.yaml accroding to your needs.
2. Execute following helm command:
```sh
helm install \
    --set-file credentials="~/path/to/credentials.json" \
    --namespace cloudflare-tunnel --create-namespace \
    cloudflare-tunnel .
```

It will create `cloudflare-server` namespace with cloudflare deployment.
