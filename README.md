# Mise en place d'un cluster Hadoop Spark 

### Etape 1 : Prérequis

# 1
> Créer un compte google plateform 

Aller sur https://console.developers.google.com/ et Créer un compte 

> Créer un google plateform projet

- Cliquer sur 'Create Project' et remplir les champs
- Associer à ce projet les API suivants :
  - Google Compute Engine
  - Google Cloud Storage
  - Google Cloud Storage JSON API 

####### NB : on suppose pour le reste du tutoriel que le nom du projet crée est Projet_GCP

> Installer et Configurer gcloud

  - Aller sur [ Google Cloud SDK ] et suivre les étapes
  - 
```sh
$ gcloud auth login                   ## authenticate to Google cloud
$ gcloud config set project hdp-00    ## set the default project
$ gsutil mb -p hdp-00 gs://hdp-00     ## create a cloud storage bucket

```
