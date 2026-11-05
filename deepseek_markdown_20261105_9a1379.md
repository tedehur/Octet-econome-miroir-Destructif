# Modèle de menace

## Surface d'attaque

| Composant | Risque | Priorité |
|---|---|---|
| Source de dédoublement | Corruption symétrique (identique sur les deux calques) | **Critique** |
| Nœud FPGA | Fault injection, usurpation PTP, saturation watchdog | **Critique** |
| Référence PTP | Désynchronisation forcée | Haute |
| Lien optique/cuivre | Interception, altération physique | Moyenne |
| Base mère | Écriture non autorisée | Haute |
| Clés matérielles | Vol, duplication | Haute |

## Ce que la superposition ne protège pas

- Une corruption identique sur les deux calques (source de dédoublement).
- Une attaque coordonnée sur les deux réseaux au même cycle d'horloge
  (théoriquement possible, pratiquement hors de portée — à mesurer).