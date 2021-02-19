# nginx

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/nginx/status.svg)](https://drone.osshelp.ru/ansible/nginx)

Installs Nginx plus configuration management.

## Usage

### Common example

```yaml
    - role: nginx
```

### Disabling ssl

```yaml
    - role: nginx
      nginx_ssl: false
```

### Nginx + VTS module

```yaml
    - role: nginx
      vts_module: true
```

### Nginx + pagespeed module

```yaml
    - role: nginx
      pagespeed_module: true
```

### Nginx + dhparam, trusted and snakeoil key/cert from vault

```yaml
# vault

dhparam_variable_name_from_vault: |
  -----BEGIN DH PARAMETERS-----
  MIIBCAKCAQEA30ek//56sa1NPOlK5/VsWXTZyc0ZT0i4VuC7+UxO27TBI0xp4XSR
  ...
  7VFhr7dducVP1VUekzy2cLtMsLLgPAWaywIBAg==
  -----END DH PARAMETERS-----

trusted_variable_name_from_vault: |
  -----BEGIN CERTIFICATE-----
  (Your Primary SSL certificate: your_domain_name.crt)
  -----END CERTIFICATE-----
  -----BEGIN CERTIFICATE-----
  (Your Intermediate certificate: Intermediate.crt)
  -----END CERTIFICATE-----
  -----BEGIN CERTIFICATE-----
  (Your Root certificate: TrustedRoot.crt)
  -----END CERTIFICATE-----

snakeoil_key_variable_name_from_vault: |
  -----BEGIN RSA PRIVATE KEY-----
  MIIJKAIBAAKCAgEAz6bULWBxgOtsbGrFcJDyvTubGh6PnJ2Ha+rqlZWnK7PotoEq
  ...
  cCAUe3/NK1+Zt9DemqSi6Ivatp+YvRycfJZofaXDfnvGHBP58WvOBSQPpHM=
  -----END RSA PRIVATE KEY-----

snakeoil_crt_variable_name_from_vault: |
  -----BEGIN CERTIFICATE-----
  MIIE8jCCAtqgAwIBAgIUI0y/ZO7S6vkp+7f/SLKNldQ6ZcgwDQYJKoZIhvcNAQEL
  ...
  mGbKLWiVGeH4si6xaNCfxAl3enVgIg==
  -----END CERTIFICATE-----

# playbook

    - role: nginx
      nginx_ssl_configuration:
        dhparam: "{{ dhparam_variable_name_from_vault }}"
        trusted: "{{ trusted_variable_name_from_vault }}"
        snakeoil_key: "{{ snakeoil_key_variable_name_from_vault }}"
        snakeoil_crt: "{{ snakeoil_crt_variable_name_from_vault }}"
```

## Available parameters

### Main

Short description here.

| Param | Default | Description |
| -------- | -------- | -------- |
| `vts_module` | not defined | Installs vts module |
| `pagespeed_module` | not defined | Install pagespeed module |
| `snakeoil.common_name` | `localhost.localdomain` | Common name for snakeoil cert. |
| `snakeoil.disable_validation` | `false` | Set this to `true` to disable snakeoil cert/key validation. |
| `geoip2_module` | not defined | Install geoip2 module (you should already have GeoIP2 databases before installation) |

### SSL configuration dictionary (nginx_ssl_configuration)

| Param | Description |
| -------- | -------- |
| `dhparam` | dhparam |
| `trusted` | Trusted CA certificates in the PEM format used to verify client certificates and OCSP responses if ssl_stapling is enabled |
| `snakeoil_key` | Snakeoil key for default host |
| `snakeoil_crt` | Snakeoil cert for default host |

## Useful links

- [Official documentation](https://nginx.org/en/docs/)

## TODO

- simplify config generation
- more examples
- review params description
- proper tests for geoip2

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
