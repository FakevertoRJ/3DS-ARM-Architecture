# 3DS-ARM-Architecture

> Documentation de l'architecture ARM11/ARM9 de la Nintendo 3DS.  
> Objectif: Comprendre comment une console moderne boot, gère la mémoire et exécute du code bas-niveau.

![ARM11](https://img.shields.io/badge/CPU-ARM11%204x%20268MHz-blue) 
![ARM9](https://img.shields.io/badge/COPROC-ARM9%20268MHz-green)
![GPU](https://img.shields.io/badge/GPU-PICA200-orange)

## ⚠️ Disclaimer
Ce repo contient uniquement de la documentation technique et des exemples homebrew. 
Aucune clé, aucun firmware, aucun contenu piraté. Basé sur les infos publiques de 3dbrew.org

## 🧠 Vue d'ensemble

La Nintendo 3DS utilise 2 processeurs ARM principaux :

| CPU | Rôle | Mode | Vitesse |
| --- | --- | --- | --- |
| **ARM11 MPCore x4** | Exécute les jeux et l'OS | ARMv6KZ, User/Kernel | 268MHz - 804MHz |
| **ARM9** | Sécurité, WiFi, carte SD | ARMv5TE | 268MHz |

+ **GPU PICA200** : Gère la 3D et les effets

## 📁 Sommaire de la documentation

| Fichier | Description |
| --- | --- |
| [docs/memory_map.md](docs/memory_map.md) | Adresses mémoire: VRAM, FCRAM, Registres HW |
| [docs/arm11_cpu.md](docs/arm11_cpu.md) | Registres, modes CPU, pipeline ARM11 |
| [docs/interrupts.md](docs/interrupts.md) | VBlank, Timer, GPU, Cartes |
| [docs/gpu_pica200.md](docs/gpu_pica200.md) | Comment envoyer des commandes au GPU |
| [docs/boot_process.md](docs/boot_process.md) | De l'allumage au lancement d'un .3dsx |

## 🚀 Exemples Homebrew

Compile avec `devkitARM` + `libctru`

```bash
cd examples/01-hello
make
