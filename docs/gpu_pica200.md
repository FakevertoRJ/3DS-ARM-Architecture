# GPU PICA200 - Nintendo 3DS

Le GPU de la 3DS s'appelle `PICA200` et il est fait par DMP. 
C'est lui qui gère la 3D, les effets, et l'affichage des 2 écrans.

## ⚡ Spécifications

| Caractéristique | Détail |
| --- | --- |
| **Nom** | DMP PICA200 |
| **Fréquence** | 268 MHz |
| **Fonctions** | 3D hardware, shading, lighting, rasterization |
| **Mémoire** | Utilise la VRAM à `0x00000 - 0x001FFFFF` |
| **Écrans** | Écran haut 400x240 3D + Écran bas 320x240 2D |

Note: La 3DS n'a pas d'OpenGL/DirectX. On parle directement au GPU via des "commandes".

## 🔧 Comment ça marche

Le CPU ARM11 envoie des "commandes" au GPU. Le GPU les lit et dessine.

Le flux de base:
1.  **CPU** : Prépare les sommets, textures, matrices dans la FCRAM
2.  **CPU** : Écrit des commandes dans la FIFO du GPU à `0x1EF00000`
3.  **GPU PICA200** : Lit la FIFO et dessine dans la VRAM
4.  **GPU** : Envoie l'image finie vers le framebuffer à `0x1FF00000`

## 📦 Concepts clés

### 1. Vertex Shader
Programme très court qui tourne sur le GPU pour chaque sommet.  
Rôle: Transformer `x,y,z` en position écran. Appliquer les matrices.

### 2. Pipeline Fixe
Le PICA200 n'est pas programmable comme une carte PC. Il a un pipeline fixe:
`Vertex -> Primitive Assembly -> Rasterization -> Fragment Shader -> Output`

Mais on peut quand même configurer: lighting, texture, fog, alpha test.

### 3. Commandes GPU
Exemple de commandes qu'on envoie:
