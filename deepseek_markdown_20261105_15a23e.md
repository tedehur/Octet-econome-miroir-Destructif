# Outils

## `octet_compressor.py`

Preuve de concept : encodage/décodage d'un texte en trame `.octet`
(en-tête JSON + payload binaire), avec vérification de roundtrip.

> ⚠️ Ce script démontre un roundtrip d'encodage, **pas** une garantie
> de sécurité. Il ne remplace pas une implémentation bas niveau (C, Rust,
> WASM) ni le nœud FPGA.

### Usage

```bash
python -m tools.octet_compressor --input examples/sample.txt \
    --output examples/sample.txt.octet
python -m tools.octet_compressor --decode --input examples/sample.txt.octet \
    --output examples/sample.decoded.txt