# Udemy retour sur premier examen

[Retour](./README.md)

## StatefulSets

Les statefulsSets sont pratique pour les applications qui ont besoin de déploiement et de mise à l'échelle ordonnée.

Ils ont également besion de headless service.

https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/

## ReplicaSet

Il doit maintenir un certain nombre stable de replica pods qui roule toujours. Il garanti la disponibilité d'un certain nombre de pod.

## Deamonset

Il s'assure que certains ou tous (Ou presque) les nodes roulent une copie d'un pod. Si on détruit le DeamonSet, il va détruire les copies qu'il a créé.

## Cronjob

Un CronJob créé des jobs sur un horaire régulier.

https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/

## kube-scheduler

Quand un nouveau Pod est créé, c'est le Scheduler qui détermine à quel Node l'assigner selon les ressources disponibles et si ce derni est propice.

https://kubernetes.io/docs/reference/command-line-tools-reference/kube-scheduler/

## CustomResourceDefinitions

Peut être utilisé pour ajouter de nouveaux types de ressources personnalisées à un cluster, l'API de Kubernetes s'occupe de l'entreposer

https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/

## Kubernetes Components

Un cluster Kubernetes contient worker machines qu'on appel node ou worker node qui roule des applications dans un conteneur. Ils contiennent les pods qui sont les composantes de l'application. Tout ce la est controllé par le control plane, ce dernier contient un scheduler, etcd,cm, ccm et etcd

### *Kubernetes objects are RESTful objects.*

![chrootdirectories](./res/components-of-kubernetes.svg)

https://kubernetes.io/docs/concepts/overview/components/

## Kubernetes Federation (KubeFed)

Sert à la coordination de plusieurs clusters. Les 2 principaux avantages sont :

- Sync des ressources à travers les clusters
- Peut configurer automatique les loadbalancer et les serveurs DNS.

On peut également compter dans les bénéfices la basse latence, permet de créer des clusters disponibles dans plusieurs régions et évite la limite de mise à l'.échelle sur les pods et nodes.

## Les 4C de Cloud Native Security

Cloud, Clusters, Containers, and Code.

## CNCF

Cloud Native Computing Foundation

## Liste de tous les objets disponibles dans le cluster

    kubectl api-resources

## kubelet

Le node agent primordial, il roule sur chaque node

## cgroup

cgroup permet de limiter les ressources, choisir les proritées et qui a contrôle de quoi.

## Open container initiative

Run, build and distribute containers

## Taches Site Reiliability Engineer

- Service Level Agreements 'SLA'
- Service Level Objectives 'SLO'
- Service Level Indicator 'SLI'

## Kubernetes dashboard

- Managing running applications
- Troubleshooting any issues withn applications
- Managing the entire Kubernetes cluster
- NOT Installing new Kubernetes cluster

## Kubernetes Services

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName
- NOT Ingre

## Required Fields in K8s Objects

- spec
- kind
- apiVersion
- metadata

Container Orchestrator Systems (COS)

- Kubernetes
- Apache Mesos
- Docker Swarm
