# Cloud Native Architecture

[Retour](./README.md)

## Description

Permet aux entreprise de rouler leur application de manière évolutive dans un environement public, privé ou hybride. 
Exemple:

- Container
- Service Mesh (Sert à indiquer la manière dont les différents éléments d'une application interagissent entre eux)
- Microservice
- Immutable Infrastructure
- API

## Application traditionnel (Lagacy)

Approche monolithique, ne possède qu'une seul base de code et resort avec un seul fichier binaire à la fin. Facile à dévolopper, mais difficile à faire évoluer.

### Solution

Cloud Native Architecture propose l'idée de découper l'application en pièce pour facilité la gestion. Au lieu d'avoir une grosse application qui fait tout, nous avons plusieurs petites applications/services qui communiquent entre-elles. 

De cette manière, il peut y avoir une équipe par fonction et ils peuvent évoluer indépendemment l'un de l'autre.

![Monolothique Architecture VS Microservice Architecture](./res/Monolithicvsmicroservices.png)

## Caractéristiques

- Possibilité d'automation (Pipeline)
- Auto-guérison
- Évolutif
- Rentable
- Facile à maintenir

## Bon point de départ

Twelve-factor app est une guideline pour développer des applications cloud native.

https://12factor.net/

## Mise à l'échelle automatique

On peut définir un maximum et un minimum pour la mise à l'échelle en fonction du coup en argent et en ressource que nos applications demandent

### Horizontale

On ajoute une instance de plus, que ce soit une VM un serveur physique ou autre.

### Verticale

On augmente la capacité des ressources que l'on a déjà, donc plus de RAM, CPU etc.

## Serverless

Le but est d'enlever une charge de travail au dev. En fournissant le code de l'application, le cloud provider va s'occuper de l'environement de l'application. Il peut s'autoscaller selon la réception d'évènements comme des requêtes.

## Open Container Initiative (OCI).

Donne des spécifications pour les images docker, comment ils vont être build et comment il vont rouler, récemment il y a aussi des spécification sur la distributions qui ont été ajouté.

## Liens pour en savoir plus

[Cliquez ici](https://trainingportal.linuxfoundation.org/learn/course/kubernetes-and-cloud-native-essentials-lfs250/cloud-native-architecture/cloud-native-architecture?page=8)


