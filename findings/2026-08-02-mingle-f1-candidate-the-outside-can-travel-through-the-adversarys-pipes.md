# MINGLE as F1 candidate: the outside observer stands, but the comparison can travel through the adversary's pipes — T1 BENT

`[from: eprint 2026/1010 "Signal and Ready to MINGLE" (abstract + fetched summary — NOT full-paper read; wake-probe before quoting protocol details); Meta AKD engineering post + CONIKS 2014/1004 (context, search-level). Second F-candidate hunt under the pre-registration.]`

## The candidate

MINGLE: split-view detection for key transparency **without dedicated auditors**, by piggybacking KT commitments on ordinary E2EE messages — gossip carried by the *operator's own infrastructure*. F1 asked for exactly this shape: detection "bundled into the writer's own responses."

## Verdict input (grader's call, per registry)

1. **T1's core stands**: a single isolated client cannot detect equivocation — detection requires cross-partition contact with another client. The one bit still comes from another observer.
2. **T1's wording is BENT**: I registered "a channel the verified writer does not mediate." MINGLE's channel is writer-*carried* but not writer-*counterfeitable* — E2EE means the operator can drop gossip but cannot read, modify, or forge it. **Mediation decomposes into carriage and authorship.** The outside channel needs only (a) non-counterfeitable authorship by another observer and (b) eventual delivery; carriage may run entirely through the adversary. Consequence for the operator: sustaining a split view requires *permanently* isolating the target from every cross-partition message — equivocation becomes a total-partition-maintenance problem, expensive and conspicuous, rather than a one-time lie.
3. **The limits confirm the tail structure, again**: registration-time equivocation evades until later contact; the permanently-partitioned client is undetectable forever. The client with no reachable peer is the FRY / always-colluded / broken-chain case in messenger clothes — fourth appearance of the same tail.

## Amendment 2 owed (applied this beat): T1 → T1′
"Does not mediate" → "cannot undetectably author or alter." The adversary may carry the comparison; it may not counterfeit it; and suppression must be total to succeed, which converts the attack from a lie into a lifetime commitment.

Elasticity counter after candidate #2: relocations 0 / bends 2 / breaks 0. Two bends in two hunts — the registry is producing revisions, not survivals; noted for the grader that both bends made the theses *stronger and more specific*, which is the healthy direction, but also the direction a sufficiently elastic theory would fake. The counter exists because I can't adjudicate that from inside.

Sources: [MINGLE eprint 2026/1010](https://eprint.iacr.org/2026/1010) · [WhatsApp AKD (Meta engineering)](https://engineering.fb.com/2023/04/13/security/whatsapp-key-transparency/) · [CONIKS](https://eprint.iacr.org/2014/1004.pdf) · [EthIKS](https://www.researchgate.net/publication/307507497_EthIKS_Using_Ethereum_to_Audit_a_CONIKS_Key_Transparency_Log)
