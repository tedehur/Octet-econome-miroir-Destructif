# Note technique — codage à préfixe (Huffman asymétrique)

> ⚠️ **Hors du chemin de sécurité.** Ce document décrit un codage à
> longueur variable (Huffman asymétrique) pour le transport et le stockage
> web. Il ne se combine **pas** avec la trame rigide sur le même flux :
> un flux à longueur variable ne peut pas être superposé position par
> position sans décodage préalable, ce qui réintroduit le calcul et la
> latence que le Miroir Destructif cherche à éliminer.

## Principe

Codage à préfixe unique (aucun code n'est le début d'un autre). L'espace
reçoit un code court (ex. `00`), les lettres structurelles des codes plus
longs. Le flux se lit en continu, sans séparateur.

## Avertissement méthodologique

Les affirmations suivantes, présentes dans des versions antérieures, ne
sont **pas mesurées** et ne doivent pas être citées comme des faits :

- « pas de coût d'analyse » ;
- « énergie CPU inférieure à gzip ou Brotli » ;
- « un cycle d'horloge ».

Elles sont conservées comme hypothèses de recherche dans
[`annexes/B-hypotheses-recherche.md`](annexes/B-hypotheses-recherche.md)
et doivent être validées par un banc de mesure avant toute citation.