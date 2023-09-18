---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "courier_deployment Resource - terraform-provider-courier"
subcategory: ""
description: |-
  Specify how to deploy.
---

# courier_deployment (Resource)

Specify how to deploy.

## Example Usage

```terraform
resource "courier_deployment" "example" {
  artifact = {
    id    = "..."
    refer = {
      uri = "..."
    }
    runtime = "tomcat"
  }

  targets = [
    {
      id   = "..."
      host = {
        address = "..."
        authn   = {
          type   = "ssh"
          user   = "root"
          secret = "..."
        }
        insecure = true
        proxies  = [
          {
            address = "..."
            authn   = {
              type   = "ssh"
              user   = "root"
              secret = "..."
            }
          }
        ]
      }
    }
  ]

  strategy = {
    type    = "rolling"
    rolling = {
      max_surge = 0.3
    }
  }

  timeouts = {
    create = "5m"
    update = "5m"
    delete = "5m"
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `artifact` (Attributes) The artifact of the deployment. (see [below for nested schema](#nestedatt--artifact))
- `targets` (Attributes List) The targets of the deployment. (see [below for nested schema](#nestedatt--targets))

### Optional

- `strategy` (Attributes) Specify the strategy of the deployment. (see [below for nested schema](#nestedatt--strategy))
- `timeouts` (Attributes) (see [below for nested schema](#nestedatt--timeouts))

### Read-Only

- `id` (String) The ID of the deployment.

<a id="nestedatt--artifact"></a>
### Nested Schema for `artifact`

Required:

- `id` (String) The ID of the artifact.
- `refer` (Attributes) The reference of the artifact. (see [below for nested schema](#nestedatt--artifact--refer))
- `runtime` (String) The runtime of the artifact.

Optional:

- `command` (String) The command to start the artifact.
- `digest` (String) The digest of the artifact, in form of algorithm:checksum.
- `envs` (Map of String) The environment variables of the artifact.
- `ports` (List of Number) The ports of the artifact.
- `volumes` (List of String) The volumes of the artifact.

<a id="nestedatt--artifact--refer"></a>
### Nested Schema for `artifact.refer`

Required:

- `uri` (String) The reference to pull the artifact.

Optional:

- `authn` (Attributes) The authentication for pulling the artifact. (see [below for nested schema](#nestedatt--artifact--refer--authn))
- `insecure` (Boolean) Specify to pull the artifact with insecure mode.

<a id="nestedatt--artifact--refer--authn"></a>
### Nested Schema for `artifact.refer.authn`

Required:

- `secret` (String, Sensitive) The secret for authentication, either password or token.

Optional:

- `type` (String) The type for authentication, either "basic" or "bearer".
- `user` (String) The user for authentication.




<a id="nestedatt--targets"></a>
### Nested Schema for `targets`

Required:

- `arch` (String) The architecture of the target.
- `host` (Attributes) Specify the target to access. (see [below for nested schema](#nestedatt--targets--host))
- `id` (String) The ID of the target.
- `os` (String) The operating system of the target.

<a id="nestedatt--targets--host"></a>
### Nested Schema for `targets.host`

Required:

- `address` (String) The address to access the target, 
in the form of [schema://](ip|dns)[:port].
- `authn` (Attributes) The authentication for accessing the host. (see [below for nested schema](#nestedatt--targets--host--authn))

Optional:

- `insecure` (Boolean) Specify to access the target with insecure mode.
- `proxies` (Attributes List) The proxies before accessing the target, 
either a bastion host or a jump host. (see [below for nested schema](#nestedatt--targets--host--proxies))

<a id="nestedatt--targets--host--authn"></a>
### Nested Schema for `targets.host.authn`

Optional:

- `agent` (Boolean) Specify to access the target with agent,
either SSH agent if type is "ssh" or NTLM if type is "winrm".
- `secret` (String, Sensitive) The secret to authenticate when accessing the target, 
either password or private key.
- `type` (String) The type to access the target, either "ssh" or "winrm".
- `user` (String) The user to authenticate when accessing the target.


<a id="nestedatt--targets--host--proxies"></a>
### Nested Schema for `targets.host.proxies`

Required:

- `address` (String) The address to access the proxy, 
in the form of [schema://](ip|dns)[:port].
- `authn` (Attributes) The authentication for accessing the proxy. (see [below for nested schema](#nestedatt--targets--host--proxies--authn))

Optional:

- `insecure` (Boolean) Specify to access the target with insecure mode.

<a id="nestedatt--targets--host--proxies--authn"></a>
### Nested Schema for `targets.host.proxies.insecure`

Optional:

- `secret` (String, Sensitive) The secret to authenticate 
when accessing the proxy, either password or private key.
- `type` (String) The type to access the proxy, 
either "ssh" or "proxy".
- `user` (String) The user to authenticate 
when accessing the proxy.





<a id="nestedatt--strategy"></a>
### Nested Schema for `strategy`

Optional:

- `rolling` (Attributes) The rolling strategy of the deployment. (see [below for nested schema](#nestedatt--strategy--rolling))
- `type` (String) The type of the deployment strategy,
either "recreate" or "rolling".

<a id="nestedatt--strategy--rolling"></a>
### Nested Schema for `strategy.rolling`

Optional:

- `max_surge` (Number) The maximum percent of targets to deploy at once.



<a id="nestedatt--timeouts"></a>
### Nested Schema for `timeouts`

Optional:

- `create` (String)
- `delete` (String)
- `update` (String)

