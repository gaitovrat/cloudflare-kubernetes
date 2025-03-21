# Cloudflare tunnel in kubernetes
## Prerequesties
- Registred domain on kubernetes (in `README.md` we will use example.com)

## Setup guide
1. Create tunnel using `cloudflared` cli:
```sh
cloudflared tunnel login
cloudflared tunnel create tunnel-name
```
2. In the output you will see generated id like `aaaaaaaa-bbbb-cccc-dddd-ffffffffffff`. Create secret from generated properties:
```sh
ID="aaaaaaaa-bbbb-cccc-dddd-ffffffffffff"
kubectl create secret generic tunnel-credentials --from-literal="credentials.json"="$(cat ~/.cloudflared/$ID.json | tr -d '\n')"
```
3. Create DNS record in [cloudflare dashboard](https://dash.cloudflare.com) like that:
```
CNAME example.com aaaaaaaa-bbbb-cccc-dddd-ffffffffffff.cfargotunnel.com
```
4. Change `ingress[0].hostname` in the file `cloudflare-config.yaml` to your registred cloudflare hostname.
5. Change `ingress[0].service` in the file `cloudflare-config.yaml` to your registred cloudflare hostname
5. Apply manifest using following command:
```sh
kubectl apply -k .
```
It will create `cloudflare-server` namespace with cloudflare deployment.
