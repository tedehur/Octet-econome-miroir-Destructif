# Changelog

## [2.0.0] — 2026-11

### Corrigé
- Hypothèse « espace = 1 bit, autres octets = 9 bits » abandonnée
  (incompatible avec un décodage sans ambiguïté).
- Distinction explicite entre trame rigide (sécurité) et Huffman (transport).
- Affirmations non mesurées (énergie, un cycle d'horloge) déplacées en
  hypothèses de recherche.
- Paragraphe central du Miroir : « compare bit-à-bit » → « superpose
  position par position ».
- Ajout du point aveugle « source de dédoublement ».
- Ajout de l'invariant d'idempotence de réconciliation.

### Ajouté
- Modèle de menace formel.
- Paramétrage de la réponse graduée (seuils, garde-fou anti-DoS).
- Feuille de route en cinq lots avec critères de sortie.