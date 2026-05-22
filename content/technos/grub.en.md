---
title: "GRUB"
description: "GRand Unified Bootloader — chargeur d'amorçage standard sur les systèmes Linux x86, supportant BIOS et UEFI."
tags: ["bootloader", "uefi", "bios", "security"]
---

GRUB (GRand Unified Bootloader) est le chargeur d'amorçage le plus répandu sur les distributions Linux. Il prend en charge les modes BIOS legacy et UEFI, et est capable de charger de multiples systèmes d'exploitation via un menu configurable.

Points clés :

- **Configuration** : générée automatiquement par `grub-mkconfig` à partir de `/etc/default/grub`
- **Secure Boot** : GRUB doit être signé par une clé reconnue par le firmware UEFI — c'est là qu'intervient le **shim**
- **Modules** : GRUB charge des modules dynamiquement (`grub-install` les copie dans `/boot/grub/`)
- **GRUB2** : la version actuelle, incompatible avec GRUB Legacy (0.x)

La chaîne de démarrage typique en UEFI Secure Boot est : `firmware → shim → GRUB → noyau`.