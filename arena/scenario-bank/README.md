# Scenario Bank

> Index of every arena scenario that has been run, past and present.
> Generator reads this BEFORE proposing a new scenario to enforce
> the anti-reuse rule (≥2 axes must differ from every prior scenario
> for the same lesson).

## Fingerprint format

Each scenario's fingerprint is a semicolon-delimited axis map, e.g.:
```
char=korean-nobleman; era=joseon-period; genre=drama;
palette=warm-earth; model=midjourney; modality=medium-set;
culture=east-asian-secular; scale=medium; domain=period-film-still
```

## Index

| ID  | Lesson | Date | Fingerprint summary | Outcome |
|-----|--------|------|---------------------|---------|
| S01 | L09 | 2026-04-17 | 1920s American general store · female shopkeeper · warm earth · commercial-product · small-set (8/9 axes flipped from DHYANA) | **void** · lesson-unnecessary (text over-specified) |
| S02 | L09 | 2026-04-17 | Feudal Japan tsuba workshop · male artisan · documentary · muted indigo-ochre · editorial · A/B control (7/9 flipped from DHYANA, 7/9 from S01) | **partial** · 3A beat 3B on 2/4 dims · adversarial-valid · ledger row #9 |
| S03 | L09 | 2026-04-17 | Ancient Aztec temple plaza · elderly priest · fantasy · jade-terracotta · game concept · A/B control all-directional dims (6/9 flipped from DHYANA/S01/S02) | **pass** · 3A beat 3B on 3/4 dims · adversarial-valid · ledger row #10 · **triggered L09 promotion** |
| S04 | L09+L12 | 2026-04-17 | Victorian steampunk lab · female scientist · editorial · cool-steel-gaslight · scientific-illustration · 6-gen multi-factor (ref strategy × crop size, 8/9 flipped vs DHYANA) | **findings** · H1/H2/H3 PASS + H4 PARTIAL · adversarial-valid · ledger row #11 · **methodology investigation — spawned L12, narrowed L09 scope. NOT a validation pass** |

## DHYANA baseline (reference, not an arena scenario)

```
char=adult-tibetan-monk; era=sci-fi-spiritual; genre=drama;
palette=cyan-amber; model=nano-banana-pro; modality=large-storyboard;
culture=east-asian-spiritual; scale=large-set; domain=film-still
```
Any arena scenario must differ from this on ≥3 axes.
