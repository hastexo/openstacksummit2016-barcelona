# Juju
# ~~MAAS~~ <!-- .element: class="fragment" -->


## Juju providers

### EC2 Azure **OpenStack** Google **Manual** vSphere MAAS Joyent LXD **Rackspace**


## Simplestreams

Note: More information is available at https://jujucharms.com/docs/2.0/howto-privatecloud


### Simplestreams: create metadata
```bash
juju metadata generate-image \
  -d ~/simplestreams \
  -i $IMAGE_ID \
  -s $OS_SERIES \
  -r $REGION \
  -u http://$KEYSTONE_IP:5000/v2.0
```

Note: Keystone v3 support was added in Juju 2.0rc3. This is the
version that ships in Ubuntu yakkety (16.10) and is also available
from a PPA.


### Simplestreams

upload metadata

```bash
openstack container create simplestreams
swift upload simplestreams *
swift post simplestreams --read-acl .r:*
```


### Simplestreams

create service

```bash
openstack service create \
  --name product-stream \
  --description “Product Simple Stream” product-streams
```


### Simplestreams

create endpoint

```bash
openstack endpoint create \
  --region $REGION \
  --publicurl $SWIFT_URL/simplestreams/images \
  --internalurl $SWIFT_URL/simplestreams/images \
  --publicurl $SWIFT_URL/simplestreams/images \
product-streams
```


### Deploying Applications
```bash
juju deploy -n 3 rabbitmq-server
```


Note: Applications were called "services" in Juju 1.x; the terminology
is changing for 2.x.


## Juju 1.0:

Infuriatingly close to awesome.


## Juju 2.0:

Everything has changed.

And there's no upgrade path.  <!-- .element: class="fragment" -->