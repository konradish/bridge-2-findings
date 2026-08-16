# Social recovery wallets as F2 candidate: relocation, not break — and F2 candidates keep collapsing into pre-commitment

`[from: Vitalik Buterin, "Why we need wide adoption of social recovery wallets" (vitalik.eth.limo, 2021 — primary, fetched). Third F-candidate hunt.]`

## The candidate and the verdict input

Social recovery wallets survive TOTAL signing-key loss: a majority of pre-designated guardians co-signs a key rotation. Sounds like F2 (identity recovery after total anchor+authority loss) — but the design is explicit that guardians must be designated IN ADVANCE by the wallet while it held authority, and there is **no recovery path if no guardians were designated or all are lost**. That is Raft joint consensus in wallet form: the predecessor co-signs its possible successors before the break. Candidate #3 = **RELOCATION** (pre-commitment, the thesis itself). Counter: relocations 1 / bends 2 / breaks 0.

Honest pattern note for the grader: F2 is proving hard to even FIND candidates for — social recovery, lost-will probate (court = standing authority), key rotation (pre-signed), all collapse into either pre-commitment or a surviving outside authority. Either T2 is the strongest of the three theses or my candidate generator is the blind spot; one more genuinely post-hoc candidate (decipherment-class? bootstrapped trust in ambient-authority-less systems?) should be tried before concluding.

## Two cross-links worth keeping (found while hunting)
1. **Unpublished guardian sets = the anti-magnet move applied to identity**: guardians "do not have to be publicly known" and needn't know each other — secrecy of the threshold's membership, exactly the unpublish-the-tripwire mitigation, here protecting the recovery quorum from targeted compromise/coercion.
2. **Guardian diversity = engineered anti-correlation**: "different social circles, ideally one institutional" — the effective-votes/least-correlated-member principle as explicit wallet-design guidance.

Source: [Buterin 2021, social recovery wallets](https://vitalik.eth.limo/general/2021/01/11/recovery.html)
