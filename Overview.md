#Bosh

##Role d'un bosh opérateur +(1)


##inception (terraform, bosh-init et bootstraping CPI)
* terraform
* bosh-init

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
https://bosh.io/docs/trusted-certs.html

## gestion de l'authentification sur bosh director
* par user / password
les utilisateurs peuvent être créés en mode interfactif. Il est néanmoins recommandé de les définir dans le bosh.yml du director afin de pouvoir les gérer en configuration
NB: réserver un utilisateur pour le health manager. dédier d'autres utilisateurs pour les accès API, comme chaos lemur)


* par uaa
les versions récentes de bosh permettent une authentification via UAA (et donc indirectement sur un backend LDAP, ou SAML)
TBC
http://bosh.io/docs/director-users.html

* génération d'un certificat ssl pour l'API bosh
Le director vient avec un certificat par défaut, pour le trafic API sur 25555
Il faut générer un certificat spécifique pour pouvoir accéder de façon sécure à l'API Bosh.
http://bosh.io/docs/director-certs.html



## docker bosh-cli en bosh release+

 Un compte dédié linux est nécessaire (le contexte courant, user et mdp sont sauvegardés dans le home directory).
 Pour faciliter l'acces nominatif à un bosh director, ISAD a développé une docker image comportant la plupart des outils nécessaire à un opérateur
 https://github.com/Orange-OpenSource/orange-cf-bosh-cli
 
 Cette image docker peut être déployée comme une bosh release, et rentrer dans la management courant d'un déploiement.
 https://github.com/cloudfoundry-community/docker-boshrelease


##gestion des manifestes

* bosh.io



* gestion de conf git


* submodule git par release

##Enjeux d'upgrades

###bosh ++++ (4)

###CPI
Le connecteur Iaas de Bosh est un composant pluggable (external CPI). Il se configure avec une bosh release colocalisée dans le deploiement d'un bosh director.
A ce titre, il peut être upgradé indépendemment. La mise à jour du CPI ne met pas à jour les déploiements fils d'un director, il faut selon les cas recréer les vms (bosh recreate)

https://github.com/cloudfoundry-community/bosh-cloudstack-cpi-release
https://github.com/cloudfoundry-incubator/bosh-openstack-cpi-release


###stemcells++++ (4)

Les stemcells sont développées et maintenues par la communauté Cloudfoundry.
Elles très régulièrement publiées sur bosh.io http://bosh.io/stemcells


##Health Manager+(1)

* config+(1)

* notification mail

* plugin hm

vs un polling de l'api bosh pour connaitre l'état des déploiments et des jobs

## Bosh SPOFs
* base postgres
* blobstore
* dns powerdns

##Manques et travaux en cours (coté Cf et anticipation coté ISAD)

### bosh 2 +++ (3)

* cloud config
* pools d'ip par bosh master
* bosh links
* add-ons

* compatibilité avec les releases bosh 1.0

### bosh on demand services

TBC travaux ISAD, produit Anynine

https://blog.anynines.com/how-to-build-a-postgresql-cloud-foundry-service-part-3/

#### bosh-deployer https://github.com/poblin-orange/bosh-deployer

#### bosh director API +(1)
* reference: l'API est partiellement documentée (éléments stables seulement) http://bosh.io/docs/director-api-v1.html
* status


###bosh release avec errand

https://github.com/Orange-OpenSource/cloudfoundry-operators-tools-boshrelease


###bosh snapshots / backup

TBC: travaux ISAD

* bosh snapshots


# CF

##Role d'un cloudfoundry operator


##domains

* shared / private par org
* SSL certificats domains wildcards
* custom SSL certs
* split brain dns pour les cf-apps / dns interne

## admin-ui++ (2)

https://github.com/cloudfoundry-community/admin-ui-boshrelease

## cf Web UI consoles

## maj de buildpacks

## maj de rootfs

## certificats pour les cf app
* certificats pour les domaines intranet / autosignés (diego seulement)
https://github.com/cloudfoundry-incubator/diego-release/releases/tag/v0.1454.0



## centralisation des logs cloudfoundry

### splunk

### logsearch cloudfoundry operator

## diego +++ (3)

### capacitaire

### cf ssh+(1)
* prerequis
* securisation

### cf routing

TBC: travaux ISAD

### migration DEA Runner => Diego Cell+++ (3)
* pérenité des dea runner: la compatiblité entre DEA Runner et Diego Cell a été largement assurée. Néanmoins il faut anticiper que l'effort de la communauté cf se fera sur Diego.
* plugin diego pour cf cli


### compatiblilité Docker / RunC




## Enjeux d'upgrades ++++++ (6)

### cf release+ (1)

### buildpacks
* aujourd'hui les versions de buildpacks offline sont lieés à la release cf
* upgrade global possible par un cf admin, en CLI
* prochainement, des bosh releases dédiées et versionnées par buildpack

### rootfs
* bosh release rootfs dédiées et versionnées pour diego

###cf cli des utilisateurs (warn / versions)
* positioner le niveau de cli attendu par cloudfoundry
* repository de plugin cf cli


## gestions des quotas

TBC: travaux pour automatiser le setting des quotas via un bosh errand

## gestion des security groups cloudfoundry (trafic sortant des cf apps)
* implémentation ip tables sur le réseau container garden
* TBC: provisionnement dynamique de security group par space selon les services bindés.
 

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


