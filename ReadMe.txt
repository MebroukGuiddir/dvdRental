####une application Java-Maven/JDBC qui liste une table
####Hacked by GUIDDIR MEBROUK 



##Cloner l’entrepôt  github
git clone git@github.com:MebroukGuiddir/dvdRental.git

## Créer une passerelle réseau
sudo docker network create --driver bridge --subnet 172.23.0.0/16 -o “com.docker.network.bridge.name”=”bridge-host” bridge-docker


## Pour lancer le conteneur de la base de données
## Sur la racine du projet
cd ./dvdRental/data
sudo docker build -t postgres_image:latest . --build-arg FILE=dvdrental.tar --build-arg DBNAME=dvdrental
sudo docker run  -d --name postgres_dvdrental --network bridge-docker --restart always -p 5432:5432 postgres_image



## La commande docker pour compiler et exécuter  l'application Java dans un conteneur
cd ../
sudo docker build -t java_image:latest .
sudo docker run -it -p 8080:8080 --name java_app --network bridge-docker --restart always java_image:latest

