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

* bosh dns et recursors

## certificats
* certificats pour les domaines intranet / autosignés

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
* SSL certificats domains wildcards
* custom SSL certs
* split brain dns pour les cf-apps / dns interne

## admin-ui++ (2)

## cf Web UI consoles

## maj de buildpacks

## maj de rootfs

## certificats pour les cf app
* certificats pour les domaines intranet / autosignés


## centralisation des logs cloudfoundry

### splunk

### logsearch cloudfoundry operator

## diego +++ (3)

### capacitaire

### cf ssh+(1)
* prerequis
* securisation


### migration DEA Runner => Diego Cell+++ (3)
* plugin diego pour cf cli

## Enjeux d'upgrades ++++++ (6)

### cf release+ (1)

### buildpacks

### rootfs
* bosh release rootfs pour diego

###cf cli des utilisateurs (warn / versions)
* positionner le niveau de cli attendu par cloudfoundry
* repository de plugin cf cli


## gestions des quotas



## gestion des security groups cloudfoundry (trafic sortant des cf apps)
* implémentation ip tables sur le réseau container garden

 

## CF Health Management+ (1)

### HA par composants CF

### cf apps restart / migration cell runner - drain des apps

### CF SPOFs: comment les réduire

Performance: aspects à 



## cf notifications

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


