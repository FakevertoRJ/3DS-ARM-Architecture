# CPU ARM11 MPCore de la 3DS

La 3DS a 4 coeurs ARM11. Mais les jeux n'utilisent que 2 coeurs max.

## Spécifications
- **Architecture** : ARMv6KZ
- **Vitesse** : 268 MHz en mode normal, 804 MHz en mode "New 3DS"
- **Cache** : 32KB I-Cache + 32KB D-Cache par coeur
- **Modes** : User, System, IRQ, SVC, Abort, Undefined

## Registres principaux
Les 16 registres 32-bit classiques :

| Registre | Nom | Rôle |
| --- | --- | --- |
| `r0 - r3` | Arg/Temp | Passer les 4 premiers arguments de fonction |
| `r4 - r11` | Callee-saved | Variables locales, conservés |
| `r12` | IP | Temporaire |
| `r13` | SP | Stack Pointer |
| `r14` | LR | Link Register = adresse de retour |
| `r15` | PC | Program Counter |

### Différence avec x86
Pas de `eax, ebx`. Ici tout est à plat : `r0 à r15`. 
La pile grandit vers le bas. `push {r4, lr}` = sauvegarde.

## Calling Convention
`fonction(arg1, arg2, arg3, arg4)`  
`arg1 -> r0, arg2 -> r1, arg3 -> r2, arg4 -> r3`  
Retour de fonction -> `r0`
