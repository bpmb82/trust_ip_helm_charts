# trust_ip_helm_charts
Helm charts to deploy [tRust_ip](https://github.com/bpmb82/trust_ip)

## Usage

You should supply the following environment variables and namespace using a values.yml file:

```
namespace: default
environment:
  - name: WHITELIST
    value: "192.168.1.12,192.168.1.13"
  - name: ATLASSIAN_IP_URL
    value: "https://ip-ranges.atlassian.com"
```

Deploy the chart as follows:

```
helm repo add trust-ip https://bpmb82.github.io/trust_ip_helm_charts
helm install trust-ip trust-ip/trust-ip --values=values.yml
```

You can then define the middleware in an ingress route:

```
apiVersion: traefik.io/v1alpha1
kind: IngressRoute
metadata:
  name: example-gui
  namespace: default
spec:
  entryPoints:
    - websecure
  routes:
  - match: Host(`service.example.com`)
    kind: Rule
    middlewares:
      - name: trust-ip-middleware
    services:
      - name: example-service
        port: 80
```