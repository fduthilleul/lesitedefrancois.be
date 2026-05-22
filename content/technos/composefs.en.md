---
title: "composefs"
description: "Système de fichiers composé conçu pour les images de conteneurs, combinant efficacement plusieurs couches en lecture seule."
tags: ["filesystems", "containers", "overlayfs"]
website: https://github.com/composefs/composefs
---

composefs est un système de fichiers en lecture seule introduit dans le noyau Linux, conçu spécifiquement pour le montage efficace d'images de conteneurs OCI. Il permet de composer plusieurs couches de système de fichiers sans les fusionner physiquement, réduisant ainsi la duplication de données sur disque.

Il est étroitement lié à **fs-verity** pour la vérification d'intégrité : chaque fichier monté via composefs peut être vérifié cryptographiquement à la lecture, ce qui en fait un choix de prédilection pour les environnements sécurisés comme Fedora CoreOS ou les runtimes de conteneurs tels que podman et bootc.