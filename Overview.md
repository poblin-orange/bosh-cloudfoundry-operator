#Bosh

##Role d'un bosh opérateur +(1)



##inception (terraform, bosh-init et bootstraping CPI)
* terraform
https://www.terraform.io/docs/providers/openstack/index.html
https://www.terraform.io/docs/providers/cloudstack/index.html
https://www.terraform.io/docs/providers/vcd/index.html

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

 * Un compte dédié linux est nécessaire (le contexte courant, user et mdp sont sauvegardés dans le home directory).
 Pour faciliter l'acces nominatif à un bosh director, ISAD a développé une docker image comportant la plupart des outils nécessaires à un opérateur
 https://github.com/Orange-OpenSource/orange-cf-bosh-cli
 
 * Cette image docker peut être déployée comme une bosh release, et rentrer dans le management courant d'un déploiement.
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


##Health Monitor +(1)

* config+(1)

* notification mail

* plugin hm

vs un polling de l'api bosh pour connaitre l'état des déploiments et des jobs

## Bosh SPOFs
* database postgres
* blobstore
* dns powerdns

## tuning bosh
* nombre de worker (protection du Iaas)
* time outs du health monitor

## tuning deployment manifest
* ips range
les clauses reserved servent à définir l'intervalle d'IPs qui seront utilisées par bosh
les Ips statiques sont celles qu'on souhaite que bosh affecte de façon permanente à des vms
Les Ips restantes sont utilisées par bosh pour affecter des IPs a son gré (ie: pour les jobs compilation de release, ou des jobs permanents ne nécessitant pas une IP fixe)

NB: le concept est différent des configuration IPs statiques ou par dhcp. Bosh director utilise l'un ou l'autre des mécanismes selon le CPI

* choix des flavors de vm
la taille mémoire des vms influe sur la taille de disque nécessaire sur le root disk (ie: il faut un espace swap égal à la taille de la RAM)

* choix du type de stockage. local versus shared
Si le CPI le permet,il faut priviligier un stockage local pour l'ephemeral disk (cycle de vie lié à celui de la vm, ie jetable)
Pour les disques persistants, ils doivent pouvoir être réattachés à la volée à une nouvelle vm => stockage shared généralement

* canary
* max in flight 


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

#### bosh-deployer
TBC https://github.com/poblin-orange/bosh-deployer

#### bosh director API +(1)
* reference: l'API est partiellement documentée (éléments stables seulement) http://bosh.io/docs/director-api-v1.html
* status


###bosh release avec errand

TBC: https://github.com/Orange-OpenSource/cloudfoundry-operators-tools-boshrelease
* service autosleep 
* cachet / cachet monitor


###bosh snapshots / backup

TBC: travaux ISAD

* bosh snapshots

### chaos lemur
s'assurer de la fiabilité d'un déploiement
* https://github.com/strepsirrhini-army/chaos-lemur
* https://blog.pivotal.io/pivotal-cloud-foundry/products/chaos-lemur-testing-high-availability-on-pivotal-cloud-foundry

TBC: support openstack, aws et vsphere. cloudstack KO

# CloudFoundry

## Role d'un cloudfoundry operator
* garantir la maj et l'absence de faille sur le socle cloudfoundry
* administrer les organisations, les buildpacks et les service brokers
* garantir l'étanchéité des composants de la plateforme, avec et entre les tenants utilisateurs.
* gérer le capacitaire global des ressources iaas (ips, stockage, mémoire)

## Installation et upgrade

### génération de manifest
* outil spiff

### smoke tests
### acceptance tests TBC
### PAT performance acceptance test TBC



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
* interconnection syslog
* limites: multitenancy, sso
 
### logsearch cloudfoundry operator


## APM for cf apps
* new relic Saas



## diego +++ (3)

### capacitaire

### cf ssh+(1)
* prerequis
* securisation

### cf routing
TBC: travaux ISAD

## cf metering
TBC: 
* https://github.com/cloudfoundry-incubator/cf-abacus
* 


### migration DEA Runner => Diego Cell+++ (3)
* pérenité des dea runner: la compatiblité entre DEA Runner et Diego Cell a été largement assurée. Néanmoins il faut anticiper que l'effort de la communauté cf se fera sur Diego.
* plugin diego pour cf cli


### compatiblilité Docker / RunC

* capacité à deployer une image docker en cf app. TBC limites
* support des Dockerfile ko


## Enjeux d'upgrades ++++++ (6)

### cf release+ (1)

### buildpacks
* aujourd'hui les versions de buildpacks offline sont lieés à la release cf
* upgrade global possible par un cf admin, en CLI
* prochainement, des bosh releases dédiées et versionnées par buildpack

Les buildpacks portent les middlewares (et les failles associées): apache /nginx/tomcat/node/ruby ...

### rootfs
* bosh release rootfs dédiées et versionnées pour diego

Les rootfs amène la vue Os offerte aux cf apps (et les failles associes, ubuntu 14.04)

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

Elements "uniques"
* blobstore: externalisable dans un stockage objet API s3. TBC
* base postgres

Elements réplicables
* routers
* nats
* etcd
* consul
* api
* loggregator traffic controller 


## cf notifications

# Services

## enjeux


### marketplace, scope de visibilité
* par space, broker privés
* par org
* publics

### statefull

p-mysql galera cluster

### stateless
* limites des cups pour un opérateur cf
* static-cred broker https://github.com/Orange-OpenSource/static-creds-broker
(ex: o-logs, o-smtp)

### registring de brokers dans le marketplace
* http ou https entre cloudfoundry et le broker
* ip ou dns

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


