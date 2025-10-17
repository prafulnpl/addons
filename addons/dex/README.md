# DEX Addon for KubeVela

This addon provides DEX OIDC Identity Provider integration for KubeVela SSO authentication.

## Features

- OIDC connector for Keycloak integration
- LDAP connector support
- Configurable client settings
- Ingress support with TLS
- KubeVela native integration

## Installation

1. Add the addon registry:
```bash
vela addon registry add dlytica-addons \
  --type git \
  --endpoint=https://github.com/dlytica-gcp/datanature-addons \
  --gitToken=<your-github-token>
```

2. Install the addon:
```bash
vela addon enable dex
```

## Configuration

The addon can be configured using the `values.yaml` file or by passing parameters during installation.

### Key Configuration Options

- `dex.issuer`: DEX issuer URL
- `dex.clientId`: OAuth2 client ID for VelaUX
- `dex.clientSecret`: OAuth2 client secret
- `dex.redirectURI`: Callback URL for OAuth2 flow
- `dex.connectors.oidc`: Keycloak OIDC connector configuration
- `ingress.host`: Ingress hostname for DEX

### Example Installation with Custom Values

```bash
vela addon enable dex --set dex.issuer=https://dex.example.com
```

## Integration with VelaUX

After installing the DEX addon, configure VelaUX to use DEX for SSO:

1. Set the following environment variables in VelaUX:
   - `DEX_SERVER`: DEX issuer URL
   - `DEX_CLIENT_ID`: OAuth2 client ID
   - `DEX_CLIENT_SECRET`: OAuth2 client secret
   - `CALLBACK_URL`: OAuth2 callback URL

2. Enable SSO in VelaUX settings

## Troubleshooting

- Check DEX logs: `kubectl logs -n vela-system -l app=dex`
- Verify configuration: `kubectl get configmap dex-config -n vela-system -o yaml`
- Test OIDC discovery: `curl https://dex.example.com/.well-known/openid-configuration`
