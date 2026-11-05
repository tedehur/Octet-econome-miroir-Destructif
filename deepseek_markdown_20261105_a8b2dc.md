# Réconciliation

## Invariants

1. **Ordre PTP** — les écritures validées sont rejouées dans l'ordre de
   leur horodatage PTP d'origine.
2. **Idempotence** — rejouer une réconciliation ne duplique pas l'écriture ;
   un identifiant d'écriture unique est stocké dans la base mère pour
   dédoublonnage.
3. **Escalade des conflits** — si deux clones divergents portent des
   écritures incompatibles sur la même position, la réconciliation est
   suspendue et escaladée à l'administrateur (clé matérielle), avec
   journalisation des deux versions.
4. **Traçabilité** — chaque réconciliation produit une entrée de journal
   (source clone, position, décision, opérateur, horodatage).