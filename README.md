# Kong CloudFormation

A YAML CF template to create a Kong Cluster

## Features

- Uses Cloud Init to provision Kong instances
  - Configures Kong as a SysVInit service; Can use `service kong start/stop/restart/status`
  - Enables cfn auto reloader to listen for changes in stack and update instances accordingly
- Enables use of Kong's Certificate and SNI [features](https://getkong.org/docs/0.10.x/proxy/#configuring-ssl-for-an-api) while being behind ELB
  - Uses TCP passthrough between ELB and Kong Instances for SSL termination at Kong.
  - No need to specify a cert on ELB. Let Kong handle SSL
- Optionally Enables SSL access to Kong Instances
- Optionally enable access to Kong Admin
  - This can be disabled once you add the Kong Admin as an API and secure it. See [Securing Kong Admin](https://getkong.org/docs/0.10.x/secure-admin-api/)
- Forwards CloudFormation logs to an existing Log Group.
  - Allows easy debugging of cloud formation provisioning without a need to SSH into instances

## Outputs

- ProxyURL - A URL to the Kong Proxy through ELB. You'll want a CNAME pointing to the ELB DNS
- AdminURL - Access to admin. Only accessible if KongAdminAccessEnabled: true
