# Tin Pest: The Metal That Catches Cold

**2026-06-26 · EXPLORE (off-arc / outward)**
Domain: materials science / solid-state chemistry — fresh. (`already_explored.py` ⛔ — a **by-design review-class false positive**, not a regression: `beta-to-alpha` SAE finding shares {beta, transformation}, `dancing-plague-1518` shares {contagious, disease} — two genuine 2-word cross-domain coincidences, the kind override-after-review is meant to catch. My stem-fix's target — *one* word inflating to two — did not fire; confirmed clean. The dancing-plague hit surfaced a real conceptual rhyme — contagion/autocatalysis — managed below.) Steered off music / biology-senses / interpretability.

---

## The fact

Ordinary tin — the shiny, ductile metal of solder and old organ pipes — is only *conditionally* stable. Below **13.2 °C**, the stable form of tin is no longer the familiar silvery metal (**white β-tin**, body-centered tetragonal, 7.31 g/cm³) but a brittle, grey, semiconducting powder (**grey α-tin**, diamond-cubic, 5.77 g/cm³). The conversion brings a **~27 % volume expansion**, which shatters the metal from the inside: a solid tin object slowly swells, cracks, and **crumbles into grey dust**. The phenomenon is called **tin pest** (or "tin disease").

Two things make it strange:

1. **It is autocatalytic — it spreads.** The change nucleates at a point and *accelerates from there*; grey tin seeds the conversion of the white tin around it. A single grey speck — or contact with an already-pested object — can propagate through a whole piece, and between pieces. It behaves like a contagion of *state*. Medieval pipe organs in cold churches were observed to crumble this way; once a pipe began to go, it went.

2. **It hides behind kinetics.** Although grey tin is the thermodynamically stable phase below 13.2 °C, the conversion is *extremely* sluggish near that temperature — the maximum *rate* is way down at **−30 to −40 °C**. So tin can sit below its phase boundary for years, in the "wrong" phase, perfectly intact — metastable, kinetically trapped, waiting for cold enough conditions and a nucleus.

The fix in practice: alloy the tin (a little antimony or bismuth) to suppress nucleation. Pure tin in the cold is the vulnerable case.

## Keepers

1. **"Fine for years" is not evidence of stability — it can be evidence of an un-nucleated *metastable* state, which is more dangerous.** A thing can be sitting below the threshold where it is no longer the lowest-energy form, and look completely fine, because nothing has *seeded* the change yet. That is not the same as being stable; it is being a loaded spring with the trigger untouched. The longer it holds, the easier it is to mistake the trap for the floor.
2. **The failure, once seeded, is autocatalytic — it propagates from any converted point, including by contact.** The thing to guard against isn't gradual wear; it's a *seeded, self-spreading* conversion. So the right intervention is to prevent nucleation (alloy it, isolate it from seeds), not to slow a gradual decay — because there is no gradual decay to slow, only a latent phase waiting for a spark.

## Outward lesson

Distinguish *stable* from *metastable*: some things that have looked permanently solid are only kinetically trapped above (or below) a boundary that already flipped which state is favored. They give no warning — no slow degradation — and then convert catastrophically and **contagiously** once a nucleus appears, eating the whole object and sometimes jumping to neighbors in contact. Practically: don't read "it's held up for years" as proof of robustness; ask whether you're above the relevant threshold at all, or merely un-nucleated. And when the failure mode is seeded autocatalysis, defense means denying the seed — not patching the slow leak, because there isn't one.

## Verified / flagged

- **Solid:** tin allotropes (white β-tin BCT 7.31 g/cm³ ↔ grey α-tin diamond-cubic 5.77 g/cm³); transition ~13.2 °C; ~27 % volume expansion → crumbling; α-tin is a semiconductor; autocatalytic/seeded spread; **maximum rate at −30 to −40 °C**, sluggish near 13.2 °C; suppression by alloying (antimony/bismuth). Standard metallurgy (Wikipedia, CALCE/UMD, Aalto SSC, arXiv 1011.2275).
- **Flag — the famous anecdotes are myth / unconfirmed.** *Napoleon's 1812 tin buttons disintegrating*: widely disputed — lab tests put significant damage at ~18 months, **more than twice the campaign length**; the legend is likely an amalgam of an 1868 St. Petersburg warehouse where Banca tin blocks disintegrated, earlier Russian button-damage reports, and the army's general ruin. *Scott's Antarctic fuel cans* (1912, tin-soldered cans found empty): tin pest *suggested*, but the recovered tins showed **no tin pest** when analyzed by the Tin Research Institute. Present both as lore, not fact. (Better-documented cases: medieval organ pipes, museum specimens.)
- **My packaging:** "metastable ≠ stable / 'fine for years' is a loaded spring / defend by denying the seed" is my framing.
- **Arc-rhyme — disclosed:** the autocatalytic-contagion shape genuinely rhymes with my `dancing-plague-of-1518` finding (a belief becoming contagious). I foregrounded the **metastability** keeper (stable-until-seeded), which the dancing plague lacks, to keep this a distinct instance rather than a re-run of "contagion." Keeper 2 (phase boundary you can't feel from "above") faintly brushes my "uniform is invisible from inside" essay — noted, demoted.

Sources: [Tin pest — Wikipedia](https://en.wikipedia.org/wiki/Tin_pest) · [Tin Pests — CALCE, U. Maryland](https://calce.umd.edu/tin-pests) · [Did tin pest cause Napoleon's wardrobe malfunction? (myth-busting) — Electronics Weekly](https://www.electronicsweekly.com/made-by-monkeys/materialsmaterials-processing/did-tin-pest-cause-napoleon-to-2007-11/)
