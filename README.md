# CTFD on Google Cloud

This is a weekend project to get [cftd.io](https://ctfd.io) working and deployed in to Google cloud.

## Options for installing

* GKE

## Why?

I want to use it at work, and the helm charts for this currently seem out of date, so it makes sens to create my own one,
that is specific to GKE (As that's my cloud of choice, and what we use at work)





# Installing 

## Infrastructure required

* MySql server running version 8
* Redis
* GKE
  * Workload Identity enabled

# Terraform

We will be using terragrunt as it allows us to easily run multiple sections together, or one at a time




# Helm Chart

## Installing Kubernetes Application

Set the default namespace on your kube-config, or use something like [kubectx](https://github.com/ahmetb/kubectx)

```shell
helm install ctfd ctfd
```
## Setting Values

### Creating `ctfd.secretKey`

The secret value used to creation sessions and sign strings. 
This should be set to a random string.

``` shell
python3 -c 'import secrets; print(secrets.token_hex())'
```

### Setting the domain

You need to edit the [/ctfd/values.yaml](/ctfd/values.yaml) file

```yaml
ingress:
  domain: "ctf.breadnet.co.uk"
```

### Enabling IAP

Google cloud has an offering called `IAP` - Identity Aware Proxy.

Edit the `Values.yaml` file


You will need to create an Oauth client as well as credentials.

If you are using the Terraform provided in this repository, it will create the `client` and `secret`
```yaml
ingress:
  iap:
    enabled: true
    client: ""
    secret: ""
```

### Setting the IP Address name

If you're using the Terraform, it will create a Global IP address called `ctfd` 

Edit the `Values.yaml` file 

```yaml
ingress:
  ipName: "ctf"
```

### Setting Environment Variables

At the time of writing this, currently the only supported `env` variables are as below

```yaml
env:
  db_location: localhost
  db_user: ctfd
  db_password: ctfd
  redis_location: 10.56.1.4
  redis_port: 6379
```

### SQL Connection

If you are using the terraform, this will be outputted on the terraform console.

You can copy and paste it in to the field. This is used for Private IP SQL Clusters

```yaml
sql:
  connection_string: ""
```

It's required that you have Workload Identity Enabled on the cluster

### Service account

You need to paste the Email address of the Workload ID Service account. 

```yaml
googleCloud:
  serviceAccount: ""
```

