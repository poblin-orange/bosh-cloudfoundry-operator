#Bosh

##Role d'un bosh opérateur +(1)


##inception (terraform, bosh-init et bootstraping CPI)

##configuration cloudstack CPI++++ (4)

revue de configuration

##découpage bosh                     +++ (3)

* urbanisme réseau+(1)

* micro / master / ops

##static routing avec network release++

##configuration des dns

* domaine par bosh

* recursors

## docker bosh-cli en bosh release+

##gestion des manifestes

* bosh.io

* gestion de conf git

* submodule git par release

##Enjeux d'upgrades

###bosh ++++ (4)

###CPI

###stemcells++++ (4)

##Health Manager+(1)

* config+(1)

* notification mail

* plugin hm

vs un polling de l'api bosh pour connaitre l'état des déploiments et des jobs


##Manques et travaux en cours (coté Cf et anticipation coté ISAD)

### bosh 2 +++ (3)

* cloud config

* bosh links

* add ons

* pools d'ip par bosh master

* compatibilité avec les releases bosh 1.0

### bosh on demand services

#### bosh-deployer https://github.com/poblin-orange/bosh-deployer

#### bosh director API +(1)

###bosh release avec errand

###bosh snapshots / backup



# CF

##Role d'un cloudfoundry operator

##domains

* shared / private par org

* custom SSL certs

## admin-ui++ (2)

## cf Web UI consoles

## maj de buildpacks

## maj de rootfs

## splunk / logsearch cloudfoundry operator

## diego +++ (3)

### capacitaire

### cf ssh+(1)

### migration DEA Runner => Diego Cell+++ (3)

## Enjeux d'upgrades ++++++ (6)

### cf release+ (1)

### buildpacks

### rootfs

###cf cli des utilisateurs (warn / versions)

## gestions des quotas

## gestion des security groups cloudfoundry (trafic sortant des cf apps)

## cf notifications 

## CF Health Management+ (1)

### HA par composants CF

### cf apps restart / migration cell runner - drain des apps

### CF SPOFs: comment les réduire

Performance: aspects à 


# Services

## enjeux


### marketplace, scope de visibilité
* par space / par org

### statefull

p-mysql galera cluster

### stateless
* limites des cups pour un opérateur cf
* static-cred broker
* o-logs

### registring de brokers dans le marketplace

### purge

### dashboard et sso

### update service broker


#Manques et travaux en cours (coté Cf et anticipation coté ISAD)

## dynamic security group broker ++++ (4)

https://github.com/Orange-OpenSource/sec-group-brokerchain/blob/master/README.md

## suivi des métriques

## alerting

## backups

## multi-site


