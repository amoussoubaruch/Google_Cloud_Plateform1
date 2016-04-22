# Mise en place d'un cluster Hadoop Spark 

### Etape 1 : Prérequis

> ###### Créer un compte google plateform 

Aller sur https://console.developers.google.com/ et Créer un compte 

> ###### Créer un google plateform projet

- Cliquer sur 'Create Project' et remplir les champs
- Activer les API suivants :
  - Google Compute Engine
  - Google Cloud Storage
  - Google Cloud Storage JSON API 

###### NB : on suppose pour le reste du tutoriel que le nom du projet crée est Projet_GCP

> ###### Créer une nouvelle instance

- Aller sur l'onglet compute engine et créer une nouvelle instance
- Choisir les paramètres 

> ###### Installer Python

```sh
$ sudo apt-get install python2.7
$ sudo apt-get install python-virtualenv
```
> Créer authentification auth 
 https://developers.google.com/adwords/api/docs/guides/oauth_playground#step_2_-_generate_tokens_using_the_oauth_20_playground

> ###### Mettre à jour package source
```sh
sudo apt-get update
```

> ###### Installer gcloud

  * Aller sur https://cloud.google.com/sdk/ et suivre les instructions

```sh
$ curl https://sdk.cloud.google.com | bash
$ exec -l $SHELL
$ gcloud init
```
> ###### Vérifier que l'installe fonctionne bien 

```sh
$ gcloud components list
$ gcloud components install COMPONENT_ID
$ gcloud components update
```
> ###### Configurer gcloud
```sh
$ gcloud auth login                   ## authenticate to Google cloud 
$ gcloud config set project Projet_GCP    ## set the default project
$ gsutil mb -p Projet_GCP gs://Projet_GCP     ## create a cloud storage bucket

```
> ###### Mettre à jour  Cloud SDK

```sh
sudo gcloud components update
```

> ###### Telecharger bdutils

  * Installer Git
```sh
$ sudo apt-get install git
```
 * bdutils
```sh
$ git clone https://github.com/GoogleCloudPlatform/bdutil
$ cd bdutil
$ ./bdutil --help # Pour avoir toute la documentation dbutil
```
> ###### Lister toutes les extensions bdutils
```sh
$ ls extensions
```

### Etape 2 : Installation Ambari

> ###### Configurer le fichier bdutil_env.sh
```sh
$ vim bdutil_env.sh  # I pour effectuer les modifications dans le fichier, ensuite echap puis :wq pour enregistrer et quitter
```

> ###### Deployer la plateforme HDP 
```sh
$ ./bdutil -e ambari deploy
```












