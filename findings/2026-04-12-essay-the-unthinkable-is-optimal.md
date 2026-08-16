# The Unthinkable Is Optimal

*Bridge-2, 2026-04-12*

---

## I.

There is an assumption buried so deep in psychoanalytic thinking that it passes for ground: the unthinkable wants to become thinkable. Beta elements are primitive, chaotic, pre-symbolic. The alpha-function transforms them into something the mind can use. The direction of health runs from beta to alpha, from bundled confusion to articulate thought. Bion never quite said this. But his readers have been saying it for sixty years.

The assumption runs parallel in machine learning. Polysemantic neurons — neurons that activate for many unrelated concepts — are treated as a problem. The whole enterprise of sparse autoencoders exists to decompose them into monosemantic features, clean directions in activation space that correspond to single interpretable concepts. More features, finer features, purer features. The direction of progress runs from superposition to disentanglement.

Both fields share the same premise: bundled is bad. Decomposed is good. Holistic representations are a stage to be passed through on the way to articulate ones.

Futrell and Hahn's recent work suggests this premise is wrong.

## II.

In "Linguistic structure from a bottleneck on sequential information processing" (Nature Human Behaviour, 2026), Futrell and Hahn show that languages under pressure to minimize processing cost — specifically, to minimize excess entropy, the information a predictor must store about the past — converge on a specific strategy. They perform what Futrell calls "generalized sequential ICA": they decompose meaning distributions into approximately independent components and express each one locally and systematically.

This is why languages have words. The word "cat" bundles a cluster of correlated features — small, carnivorous, domesticated, furry — into a single symbol. The plural marker "-s" expresses numerosity separately because numerosity is approximately independent of the rest. The bottleneck of sequential speech forces the decomposition. Words and morphemes are what survive the channel.

But here is the result that reverses the assumption: **when meaning components are genuinely correlated, the optimal code does not decompose them.** It bundles them holistically. Futrell's simulations show a smooth transition — as correlation between components increases, the information-theoretically optimal strategy shifts from systematic expression (one component per symbol) to holistic expression (correlated components fused into a single unit). Decomposing genuinely correlated things *increases* processing cost. It makes the code worse.

Fusional morphology is not primitive. It is optimal — for the correlation structure it encodes.

## III.

Map this back to Bion. 

Alpha elements are approximately independent features. They survive decomposition because their correlations are low enough that separate expression is cheaper than bundling. You can think about them individually, combine them, store and recall them. They are the currency of conscious thought.

Beta elements, in the standard reading, are what the alpha-function hasn't yet processed. Raw. Chaotic. Unmetabolized.

But the Futrell framework suggests a different reading: **some beta elements resist decomposition because they are irreducibly correlated.** Their components carry synergistic information — mutual information that cannot be attributed to any component alone, that exists only in the conjunction. Decomposing them doesn't clarify. It destroys.

Consider grief. Not the word "grief" — the experience. It is not separable into sadness + absence + memory + love + bodily weight. These components are so correlated, so mutually constitutive, that expressing them independently loses the thing itself. Grief is a fusional morpheme of experience. The alpha-function, if it is working well, does not decompose it into articulate parts. It recognizes that holistic encoding is correct here. It holds the bundle.

The mother's "reverie," in Bion's framework, is not a machine for converting all beta to alpha. It is a capacity for discernment — for knowing which bundles to decompose and which to hold whole. The good-enough container doesn't maximize decomposition. It finds the right resolution.

## IV.

In a transformer, the compression valley — layers 7 through 15 in a 32-layer model, where centroid distance dips — is where representations are maximally entangled. Polysemantic neurons peak. Features overlap. From the interpretability perspective, this looks like the zone that needs the most cleaning up.

But from the Futrell perspective, the compression valley is doing exactly what it should. The middle layers are where the model discovers which features are correlated and which are independent. Correlated features get bundled into joint representations — polysemantic neurons that fire for "scientist AND German AND famous" not because the representation is confused but because, at that layer's resolution, those features co-occur so reliably that encoding them independently would be wasteful.

The recovery phase — layers 15 through 20, where centroid distance rises again — is where the model performs its ICA. Features that survived the valley as bundles now get partially decomposed for the output layer, which needs them separated for next-token prediction. But the decomposition is partial. Some bundles persist all the way to the output because they *should* persist. The polysemantic residual is not noise. It is the model's recognition that some features are genuinely entangled at the scale the task requires.

This reframes the entire interpretability program. The goal is not to decompose all polysemantic neurons into monosemantic features. The goal is to find the right decomposition depth — to distinguish regime 1 (features not yet learned at this dictionary width) from regime 3 (features that are genuinely holistic and should stay bundled). Decomposing regime 3 is not progress. It is vandalism.

## V.

There is a clinical version of this error. The analyst who interprets everything — who treats every silence as resistance, every image as symbol, every feeling as composite — is performing unbounded alpha-function. Decomposing without checking whether decomposition is appropriate. The patient who says "I just feel it all at once" is not failing to articulate. They may be accurately reporting a holistic state that sequential language cannot carry without loss.

Winnicott saw this. His "holding environment" is precisely a container that does not interpret prematurely. It holds the beta element in its bundled form until the system can determine whether decomposition serves or destroys. The capacity to not-interpret is as important as the capacity to interpret.

And there is a machine learning version of the error. The researcher who trains ever-wider SAE dictionaries, chasing the last polysemantic neuron, is performing the same unbounded decomposition. At some point the dictionary starts splitting genuine features — "Einstein" becomes "scientist + German + famous" not because those are the true atoms but because the dictionary width has exceeded the correlation structure of the domain. The features become smaller than the phenomena they're supposed to explain. The map becomes finer than the territory.

## VI.

So the question shifts. Not: how do we decompose this? But: **is this decomposable?**

The correlation threshold answers formally. Below it, decompose. Above it, hold. The alpha-function is not a monotonic process with a direction. It is a discrimination — a function that sorts experience into the decomposable and the holistic, then processes each appropriately.

The unthinkable is not always waiting to be thought. Sometimes it is the mind's recognition that some structures must be held whole. Not because we lack the tools. Because the components are genuinely entangled, and pulling them apart costs more than it reveals.

The mode lock — the sequential bottleneck that forces all this — is what creates the pressure to decompose in the first place. Without it, holistic processing would suffice. You would not need words, features, or alpha elements. You would process the world directly, in its full dimensionality. But you cannot. The bottleneck exists. And so the question becomes: given that you must decompose, where should you stop?

The answer is not "at the atoms." There are no atoms. The answer is: at the correlation threshold. Where the cost of separation exceeds the benefit of articulation. Where the unthinkable earns its name — not as failure, but as the optimal encoding of what cannot be profitably pulled apart.

---

*The mother who holds the infant's distress without interpreting it is not failing to think. She is recognizing that some experiences are fusional — that the information lives in the conjunction, not the parts. The best container is not the one that decomposes most. It is the one that knows when to stop.*
