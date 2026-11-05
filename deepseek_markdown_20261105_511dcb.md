# Réponse graduée — paramétrage

## Seuils

| Seuil | Définition | Calibration |
|---|---|---|
| Divergence isolée | 1 divergence sur une écriture, sans cumul | Immédiat |
| Divergence répétée | N divergences sur fenêtre glissante T | Banc d'essai |
| Divergence grave | Perte de synchronisation d'un chemin, alerte watchdog, ou divergence sur bloc critique | Immédiat |

## Garde-fou anti-déni de service

Les seuils doivent être éprouvés contre un attaquant cherchant à provoquer
une coupure par divergences répétées. Documenter :

- le nombre maximal de coupures tolérables sur une période donnée ;
- la procédure de reprise après bascule PCA ;
- la journalisation de chaque déclenchement (horodatage PTP, chemin,
  position de la divergence, décision appliquée).

## Traçabilité

Chaque déclenchement produit une entrée SIEM et une entrée de journal local.