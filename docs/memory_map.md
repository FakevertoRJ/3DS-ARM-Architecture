# Memory Map Nintendo 3DS

La 3DS utilise un mapping mémoire fixe. Chaque adresse a un rôle précis.

## Vue globale ARM11

| Adresse de début | Adresse de fin | Taille | Utilisation |
| --- | --- | --- | --- |
| `0x00000` | `0x001FFFFF` | 2 MB | **VRAM** : Mémoire vidéo du GPU PICA200 |
| `0x08000000` | `0x0BFFFFFF` | 64 MB | **FCRAM** : RAM principale pour les applications |
| `0x10000000` | `0x1FFFFFFF` | 256 MB | **Registres HW** : GPU, DMA, Interrupts, etc |
| `0x1FF00000` | `0x1FFBFFFF` | 768 KB | **VRAM LCD** : Framebuffer des 2 écrans |
| `0x1FF80000` | `0x1FFFFFFF` | 8 MB | **FCRAM partagée** : Données système |

### Points clés à retenir
1.  **FCRAM** = là où tourne ton code homebrew. C'est ton "tas" + "pile".
2.  **Registres HW à 0x10000000** : Pour allumer le GPU ou lire les boutons, tu écris ici.
3.  **VRAM** : Tu ne peux pas exécuter du code depuis la VRAM. Uniquement pour textures/vertices.

Source: [3dbrew Memory Layout](https://www.3dbrew.org/wiki/Memory_layout)
