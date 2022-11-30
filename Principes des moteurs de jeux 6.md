# Principes des moteurs de jeux 6 : réseau

## TCP vs UDP

- mise à jour TCP
- jeu entre joueur U/T
- lobby T
- achats T
- sauvegardes T
- discussion T
  - texte T
  - voix U
- partage réseau sociaux T
- DRM T
- Streaming U
  - diffusion
  - cloud gaming

----

| TCP                   | UDP      |
| --------------------- | -------- |
| garantie de réception | rapidité |
| ordre                 |          |
| intégrité             |          |
| connexion             |          |

### exemple : mario cart

position 12 octets

orientation 16 octets

vitesse 12 octets

objets 1 octets

action 1 octets

somme : 42 octets <- trop petit par rapport à la taille de trame



add donc :

compteur	pour ordre

checksum	pour intégrité

UUID	pour connexion

message historique	pour (aider à la garantie de réception)

## Messages

- type
- taille
- contenu

## Appendix

### RAID

*redendence array of inexpensive disk*

RAID 5: 坏了一块盘不影响

```pseudocode
d = a XOR b XOR c
```

