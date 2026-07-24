# Boot Process Nintendo 3DS

Comment la 3DS passe de "bouton Power" à "écran d'accueil".  
2 CPU = 2 étapes de boot. ARM9 démarre en premier.

## 🔁 Vue d'ensemble

## 1. Étape ARM9 : Le "Boot9"

C'est le plus bas niveau. Il tourne à `0xFFFF0000` en interne.

| Action | Détail |
| --- | --- |
| **Vérification** | Vérifie la signature du `NATIVE_FIRM` dans la NAND |
| **Déchiffrage** | Déchiffre le kernel avec les clés hardware |
| **Chargement** | Copie `NATIVE_FIRM` en RAM à `0x08000000` |
| **Handover** | Libère l'ARM11 et lui dit "démarre" |

Rôle principal: Sécurité. L'ARM9 est le "garde". Il gère aussi SD, WiFi, carte.

## 2. Étape ARM11 : Le "Kernel" NATIVE_FIRM

Une fois que l'ARM9 dit OK, l'ARM11 démarre.

| Action | Détail |
| --- | --- |
| **Init HW** | Active GPU, écrans, touches, mémoire |
| **Lance les services** | `fs:`, `gsp:`, `hid:`, `apt:` etc. Ce sont des processus système |
| **Lance le Home Menu** | `menu.smdh` devient le processus principal |

C'est à ce moment que tu vois l'écran d'accueil avec les bulles.

## 3. Lancer un Jeu / Homebrew

| Type | Comment ça boot |
| --- | --- |
| **Cartouche .3ds** | ARM9 monte la cartouche → ARM11 charge l'exe du jeu |
| **CIA installé** | ARM11 charge le .cia depuis la NAND/SD |
| **Homebrew .3dsx** | Le `Homebrew Launcher` est déjà un .3dsx. Il charge ton .3dsx en mémoire et l'exécute en mode "Userland" |

### Mode Userland vs Kernel
- **Userland** : 99% des homebrews. Accès limité au HW. Safe.
- **Kernel** : Luma3DS, CFW. Accès total. Peut patcher le kernel.

## 🧠 Adresses clés pendant le boot

| Adresse | Qui l'utilise | Contenu |
| --- | --- | --- |
| `0xFFFF0000` | ARM9 BootROM | Code interne, non dumpable |
| `0x08000000` | ARM11 | NATIVE_FIRM + Jeux |
| `0x1FF80000` | Les deux | Mémoire partagée pour communiquer |

## 🛠️ Pour les devs Homebrew
Quand tu lances `hello.3dsx` avec le Homebrew Launcher:
1.  Le Launcher demande au kernel: "alloue moi de la FCRAM"
2.  Il copie ton `main.c` compilé en RAM
3.  Il saute à `main()` → ton code tourne

Tu n'as pas besoin de toucher au Boot9. DevkitPro fait tout.

## 🔗 Ressources
- [3dbrew Boot Process](https://www.3dbrew.org/wiki/Boot_process)
- [3dbrew NATIVE_FIRM](https://www.3dbrew.org/wiki/NATIVE_FIRM)

---
**À retenir** : ARM9 = Sécurité, ARM11 = Utilisateur.  
C'est pour ça que hacker la 3DS = trouver une faille dans l'ARM9.
