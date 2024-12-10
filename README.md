CAHIER DES CHARGES MODIFIÉ : PROJET SAE502
Objectif :

Automatiser la configuration des switchs dans des infrastructures réseau de grande envergure.
L'objectif est d'éviter la redondance des tâches manuelles en créant des scripts automatisés pour injecter directement les configurations sur plusieurs switchs.
Les configurations se concentreront principalement sur :

    La gestion des ports
    La création et la gestion des VLAN

Environnement et Outils Utilisés :
Infrastructure matérielle et logicielle :

    Nombre de machines : 1 machine virtuelle sous Linux (Ubuntu).
    Nombre de conteneurs Docker :
        1 conteneur Ansible : Pour l'automatisation des configurations.
        1 conteneur de simulation réseau : Pour simuler l'infrastructure réseau à l’aide de GNS3.

Services utilisés :

    Docker : Isolation des environnements Ansible et GNS3.
    Ansible : Automatisation de la configuration des switchs via des playbooks et des rôles.
    Git : Gestion de versions des scripts et collaboration en équipe.
    GNS3 : Simulation réseau avec des équipements virtuels représentant des switchs et routeurs.

Arborescence Visée pour Ansible :

switch_config                # Rôle principal pour la configuration des switchs
├── defaults                 # Variables par défaut
│   └── main.yml             # Définitions par défaut (ex. VLAN ID)
├── files                    # Fichiers statiques (firmware, fichiers de configuration fixes)
├── handlers                 # Gestionnaires d'événements
│   └── main.yml             # Redémarrage des services ou envoi d'une alerte
├── meta                     # Métadonnées du rôle
│   └── main.yml             # Dépendances et documentation sur le rôle
├── tasks                    # Actions principales
│   ├── main.yml             # Lancement des autres fichiers de tâches
│   ├── config.yml           # Configuration des switchs (ports, VLAN)
│   └── backup.yml           # Sauvegarde des configurations avant modification
├── templates                # Modèles dynamiques de configuration (Jinja2)
│   └── switch_config.j2     # Modèle de configuration des switchs
├── tests                    # Fichiers pour tester les scripts
│   ├── inventory            # Inventaire des équipements réseau de test
│   └── test.yml             # Playbook pour valider les scripts
├── vars                     # Variables spécifiques
│   └── main.yml             # Définition des VLAN et autres paramètres spécifiques
└── system_validation        # Rôle annexe pour valider les configurations système

Étapes de Réalisation :
1. Planification et Préparation

    Validation complète du cahier des charges.
    Définition des besoins spécifiques (nombre de VLANs, topologie réseau).

2. Mise en Place de l’Environnement

    Installation des paquets nécessaires : Docker, Ansible, Git, GNS3.
    Création des conteneurs Docker :
        Conteneur pour Ansible.
        Conteneur pour GNS3 (Simulation réseau).
    Configuration réseau : Mise en place d’un réseau bridge pour permettre la communication entre les conteneurs et la VM.

3. Développement des Playbooks et Rôles

    Rédaction des playbooks :
        Configuration des ports.
        Mise en place des VLAN.
        Sauvegarde des configurations existantes.
    Structuration des rôles Ansible conformément à l’arborescence définie.

4. Collaboration et Gestion de Versions

    Création d’un dépôt GitHub pour stocker les scripts et rôles.
    Suivi des versions via Git.
    Documentation des modifications dans les commits et sur le README du projet.

5. Mise en Place du Script d’Automatisation

    Développement d’un script principal pour exécuter :
        Les tâches de configuration.
        La sauvegarde automatique avant toute modification.

6. Tests et Validation

    Simulation des configurations réseau dans GNS3 via le conteneur dédié.
    Validation de la connectivité et des configurations appliquées sur les switchs.
    Tests en boucle pour corriger les erreurs avant une implémentation réelle.

Rôles des Conteneurs Docker :
1. Conteneur Ansible :

    Stockage et exécution des playbooks Ansible.
    Gestion des rôles et configurations.
    Point central de l'automatisation des tâches sur les équipements réseau.

2. Conteneur de Simulation Réseau :

    Contient l’instance GNS3 pour représenter les switchs virtuels.
    Permet de tester les configurations sans impact sur des équipements réels.
    Offre un environnement de simulation proche du réseau réel.

