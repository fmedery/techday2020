
# Before the demo

## Consumer VPC

* Create the `consumer VPC` with 2 private subnet.
* Deploy consumer1 in the private subnet 1.
* Deploy consumer2 in the private subnet 2.
* On both consumers:

  ```bash
  sudo yum install -y elinks
  ```

## Proxy VPC

* Create the `proxy VPC`.

## Transit Gateway

* Create a `TGW`.
* Link it with both VPC.
* Update VPCs'route tables.

## Application1

```bash
eksctl create cluster -f eksctl/app1.yaml
```

switch context to **cluster application1**

```bash
kubectl create ns application1
kubectl create -f k8s/
```

## Application2

```bash
eksctl create cluster -f eksctl/app2.yaml
```

Switch context to **cluster application2**

```bash
kubectl create ns application2
kubectl create -f k8s/
```

# AWS PrivateLink

## Endpoint for application1

* Create the *Endpoint Service* connected to `application1 NLB`.
* Create the *Endpoint* in the `proxy VPC` (pointing to the *Endpoint Service*).
* Create the application1 *Endpoint* SG  to allow `HTTP` from CIDR from the `consumer VPC`.

## Endpoint for application2

* *Endpoint Service* connected to app2 NLB.

`
The rest will be done during the demo.
`

# Demo

## Demo 1: testing application1 connectivity from both consumers

* Showcase that both `application1 VPC` and `application2 VPC` have the same CIDR Block.
* from consumer 1:
  * Use `elinks --dump` to get the output of application1.
* from consumer 2:
  * Use `elinks --dump` to get the output of application1.

## Demo 2: Create application2 Endpoint + SG and test the connectivity from both consumers

* From AWS Console:
  * Create the application2 *Endpoint* in the `proxy VPC`.
  * Create the application2 *Endpoint* SG to **only** allow HTTP from consumer 1 IP.
From consumer1:
* from consumer 1:
  * Use `elinks --dump` to get the output of application2.
* from consumer 2:
  * Use `elinks --dump` to get the output of application2: command will timeout after 30 sec.
