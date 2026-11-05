# Octet-Économe & Miroir Destructif

> Architecture de résilience pour systèmes critiques : trame binaire rigide,
> superposition matérielle et réponse graduée face aux ransomwares et
> compromissions de réseaux internes.

[![Statut](https://img.shields.io/badge/statut-recherche%20conceptuelle-orange)]()
[![Licence](https://img.shields.io/badge/licence-Apache%202.0-blue)]()
[![Contributions](https://img.shields.io/badge/contributions-bienvenues-brightgreen)]()

---

## ⚠️ Avertissement

Ce dépôt contient une **recherche conceptuelle**, pas un produit fini.
Aucune affirmation de performance, d'économie d'énergie ou de sécurité
absolue n'est validée par un banc de mesure à ce jour. Les hypothèses
non mesurées sont explicitement listées dans
[`docs/annexes/B-hypotheses-recherche.md`](docs/annexes/B-hypotheses-recherche.md).

Le code fourni (PoC Python, ébauche Rust) est **illustratif** : il démontre
un roundtrip d'encodage/décodage, pas une garantie de sécurité.

---

## Le problème

Les systèmes critiques (santé, industrie, infrastructures) souffrent d'une
vulnérabilité systémique face aux ransomwares et aux compromissions de
réseaux internes. La défense périmétrique logicielle classique échoue
lorsqu'un attaquant est déjà à l'intérieur.

## La proposition

Deux mécanismes distincts, à ne pas confondre :

| Mécanisme | Rôle | Principe |
|---|---|---|
| **Trame rigide Octet-Économe** | Intégrité / superposabilité | Écriture à positions attendues ; toute insertion ou suppression décale le flux et casse la superposition |
| **Miroir Destructif** | Résilience / anti-ransomware | Deux chemins physiquement indépendants (Alpha, Bêta), superposés par un nœud FPGA ; réponse graduée en cas de divergence |

Un troisième mécanisme, **hors du chemin de sécurité**, est documenté
séparément : un codage à préfixe (Huffman asymétrique) pour le transport
et le stockage web ([`docs/08-note-huffman-transport.md`](docs/08-note-huffman-transport.md)).

---

## Principes de sécurité

1. **Sécurité par désynchronisation physique** — corrompre deux réseaux
   isolés au même cycle d'horloge est la contrainte qui protège le système.
2. **Superposition, pas calcul** — le vote compare position par position,
   sans recalcul de signature ; la latence est immédiate.
3. **Séparation des privilèges** — l'écriture en base mère exige un vote
   identique **et** une clé matérielle présentée physiquement.
4. **Réponse graduée** — divergence isolée → blocage local ; divergence
   grave ou répétée → bascule sur réseau PCA isolé, quarantaine forensique.
5. **Honnêteté méthodologique** — toute affirmation non mesurée est
   étiquetée comme hypothèse de recherche.

---

## Documentation

| Document | Contenu |
|---|---|
| [`docs/00-whitepaper.md`](docs/00-whitepaper.md) | Livre blanc consolidé |
| [`docs/01-format-trame-rigide.md`](docs/01-format-trame-rigide.md) | Spécification de la trame |
| [`docs/02-miroir-destructif.md`](docs/02-miroir-destructif.md) | Architecture du miroir |
| [`docs/03-noeud-vote-fpga.md`](docs/03-noeud-vote-fpga.md) | Nœud de vote matériel |
| [`docs/04-reponse-graduee.md`](docs/04-reponse-graduee.md) | Seuils et procédures |
| [`docs/05-reconciliation.md`](docs/05-reconciliation.md) | Idempotence et conflits |
| [`docs/06-feuille-de-route.md`](docs/06-feuille-de-route.md) | Lots et critères de sortie |
| [`docs/07-modele-de-menace.md`](docs/07-modele-de-menace.md) | Surface d'attaque, priorité Red Team |
| [`docs/08-note-huffman-transport.md`](docs/08-note-huffman-transport.md) | Compression web (hors sécurité) |

---

## Schémas

Les diagrammes Mermaid sont dans [`diagrams/`](diagrams/) :

- `niveau-0-systeme.mmd` — vue système (soignants, clones, vote, PCA)
- `niveau-1-redondance.mmd` — redondance active Alpha/Bêta
- `niveau-2-fpga.mmd` — nœud matériel (SERDES, PTP, comparateur, vote)

---

## Preuve de concept

```bash
# Encodage
python -m tools.octet_compressor --input examples/sample.txt \
    --output examples/sample.txt.octet

# Décodage (vérification roundtrip)
python -m tools.octet_compressor --decode --input examples/sample.txt.octet \
    --output examples/sample.decoded.txt

# Tests
pytest tests/
