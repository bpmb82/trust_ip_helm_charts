# trust_ip_helm_charts
Helm charts to deploy trust_ip

## Usage

You should supply the following environment variables using a values.yml file:

```
environment:
  - name: WHITELIST
    value: "192.168.1.12,192.168.1.13"
  - name: ATLASSIAN_IP_URL
    value: "https://ip-ranges.atlassian.com"
```

Deploy the chart:

```
helm repo add trust-ip https://bpmb82.github.io/trust_ip_helm_charts
helm install trust-ip trust-ip/trust-ip -f values.yml
```