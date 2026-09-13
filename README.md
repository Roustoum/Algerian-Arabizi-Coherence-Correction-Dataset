# Algerian Arabizi Coherence & Correction Dataset

An open, hand-authored dataset of short Algerian Arabizi (Latin-script Algerian Darija) sentences, each labeled as coherent or incoherent, with a hand-written correction for every incoherent sentence.

## Overview

This dataset supports two linked tasks over short Algerian Arabizi sentences:

1. **Coherence classification** — decide whether a sentence makes sense (`coherence = 1`) or is semantically incoherent (`coherence = 0`).
2. **Conditional correction** — for an incoherent sentence, produce a corrected, coherent version of it.

Each incoherent example was built by taking a coherent Algerian Arabizi sentence and swapping one element (an object, a place, a time, an actor, ...) for a word that breaks its real-world plausibility, while keeping the sentence grammatically well-formed:

```
rouht ne9ra fel koucha,0        <- incoherent ("I went to study in the kitchen")
rouht ne9ra fel bus,1            <- the corrected, coherent version
```

## Files

- `data.csv` — the prepared dataset, containing:
  - `text`: String. The Algerian Arabizi sentence to judge.
  - `coherence`: Integer, `0` or `1`. `0` = incoherent; `1` = coherent.
  - `correction`: String. The corrected, coherent version of `text`, present only when `coherence = 0`. Empty when `coherence = 1`.

## Example

```csv
text,coherence,correction
ntayab kroumb survet,0,ntayab kroumb chwiya
9law dinde,1,
el moujahid de7mani sa3id kber fi 3ayla pistache,0,el moujahid de7mani sa3id kber fi 3ayla bourjwaziya
```

## Creation and Maintenance

This dataset is hand-authored: contributors wrote pairs of sentences by hand — one deliberately incoherent sentence, immediately followed by its coherent correction — imitating realistic Algerian Arabizi writing rather than sampling or scraping real posts.

The dataset is actively maintained in this repository rather than being a single static drop:

- The source material is a larger set of closely related, hand-written pairs; only a sampled subset is kept in `data.csv` at any given time, to reduce redundancy and near-duplicate examples between rows.
- Additional sentence pairs have been added by hand in subsequent revisions to broaden topic coverage.
- A small number of rows that did not cleanly follow the incoherent-then-coherent pairing pattern have been reviewed and cleaned up.

Changes are tracked through this repository's commit history.

## License

This dataset is released under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license — see [`LICENSE`](./LICENSE). You are free to share and adapt the data for any purpose, including commercially, as long as you give appropriate attribution.

It is free to use for research, education, model training, and competition purposes. Because it is fully original and hand-written, it contains no third-party copyrighted text and no personal data belonging to real individuals.

## Known Limitations

- **Synthetic, single-population origin.** All sentences were hand-written by a small group of contributors, not sampled from real-world Algerian text. Vocabulary, topics, and phrasing reflect that group's choices rather than the natural distribution of Algerian Arabizi writing.
- **Narrow incoherence pattern.** Incoherence is always introduced by a single-element substitution, so models trained on this data may learn to exploit this specific construction rather than general coherence judgment. Real-world incoherent text can fail in far more varied ways.
- **No standard Arabizi spelling.** Arabizi has no official transliteration standard; the spelling conventions here reflect the contributors' personal habits and may not generalize to other writers' conventions.
- **Sampled, not exhaustive.** Only a fraction of the available hand-written pairs is included at any time, chosen to reduce near-duplicate examples; some topical or lexical patterns from the source material may be under-represented as a result.

## Intended Use

Suitable for: binary coherence/plausibility classification in Arabizi and Algerian Darija, conditional text correction / minimal-edit generation, robustness and dialect-understanding evaluation, and instruction-tuning or fine-tuning models to jointly judge and correct short informal Arabic dialect text.

Models trained on this dataset should not be assumed to generalize to naturally occurring incoherent text, other Arabic dialects, or Arabizi spelling conventions beyond those used by the original contributors.
