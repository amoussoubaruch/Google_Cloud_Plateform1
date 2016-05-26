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

### Etape 3 : Installation Ambari
# Generate an env file from flags, then deploy/delete using that file.
```sh
$ ./bdutil --bucket amoussoubaruch-spark-bucket --project projetgcp-1286  --default_fs gs --machine_type n1-standard-1 --force --zone us-central1-c --num_workers 2 --prefix spark-cluster --verbose generate_config spark_dev_env.sh
```

# Check cluster configuration
```sh
$ nano spark_dev_env.sh
```
### Etape 4 : Deploy instance

```sh
# run cluster
$ ./bdutil --force -e spark_dev_env.sh,extensions/querytools/querytools_env.sh,extensions/spark/spark_env.sh deploy

# ssh to cluster master
$ gcloud --project=projetgcp-1286 compute ssh --zone=us-central1-c spark-cluster-m

# Se connecter en tant qu'utilisateur hadoop
$ sudo su - hadoop

# list files
$ ls -l

# list bucket file
$ hadoop fs -ls
$ gsutil ls gs://amoussoubaruch-spark-bucket

#os.environ["SPARK_HOME"]
$ SPARK_HOME='/home/hadoop/spark-install'

# Add the PySpark classes to the Python path:
$ export SPARK_HOME="$SPARK_HOME"
$ export PYTHONPATH=$SPARK_HOME/python/:$PYTHONPATH
$ export PYTHONPATH=$SPARK_HOME/python/lib/py4j-0.8.2.1-src.zip:$PYTHONPATH
```

### Etape 5 : Run Spark
```sh
$ cd spark-install
$ ./bin/pyspark
```

### Complémenrts

#########2 Après avoir lancer un serveur

########### Delete cluster
```sh
$ ./bdutil delete
```
######### Build application with gcp









