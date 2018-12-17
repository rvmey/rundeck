# rundeck
Rundeck test project


# Installation options for Kubernetes and other VM based workloads like Kafka, Zookeeper, Vault, Elasticsearch, Logstash, and Kibana

Option 1:  Roll our own VM installs

Pros:
- This option could come closer to conforming to Joe’s requirement that we pre-bake VM images for each application.  Configuration scripts would still have to run after the VMs boot. 
- No vendor lock-in.  
- Full freedom to make configuration changes.

Cons:
- Less support from Canonical.
- Slower time to market because we have to build more code ourselves.  
 
Option 2:  Install VMs with Juju

Pros:
- Juju is Canonical’s preferred tool.
- Time to market 
- We would leverage Canonical’s existing infrastructure code.
- We’ve already started down this path, so we now have some of our own code.
- Easy Kubernetes upgrades 
- Patch upgrades (for example 1.12.1 -> 1.12.2) happen automatically behind the scenes by default.
- Minor upgrades (1.12 -> 1.13) are automated with a sequence of Juju commands we could script: https://kubernetes.io/docs/getting-started-guides/ubuntu/upgrades/
- We could use Juju to spin up Vault, Kafka, and ELK VM’s
- We could use Juju’s “relations” to auto-configure K8s to log to ELK, to use Vault to store the encryption key for K8s secrets stored in etcd, and to setup basic monitoring of each VM to Nagios.

Cons:
- Vendor lock-in.  
- Juju doesn’t support all configurations.
- Switching major Kubernetes components like the CNI plugin might require us to pay for Juju development if that integration isn’t already available, like in the case of the Tigera CNI.  If that happens, we’d have to wait for it to be developed, and possibly pay for it.  FYI – Mike Iatrou told me Canonical started the Tigera integration work about 2 weeks ago even though we haven’t agreed to pay for it because they know we’re in a hurry.
- Juju’s Vault server charms use etcd VM’s instead of consul as Vault’s back-end DB.   
 
Reference:
https://github.com/heptiolabs/wardroom 
https://jujucharms.com/vault 
https://jujucharms.com/kafka 
https://jujucharms.com/zookeeper 
https://jujucharms.com/kubernetes 
https://jujucharms.com/elasticsearch 
https://jujucharms.com/logstash
https://jujucharms.com/kibana 

