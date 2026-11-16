# A Path Already Walked

> Markdown version of the project page at https://aiml-sdu.github.io/path-already-walked-page/. Interactive figures are on the web page. Every number here also appears there and comes from the paper or its stored results.

On inheriting network-neuroscience tools for mechanistic interpretability

Network neuroscience has spent two decades learning which graph statistics mislead and why. We argue that interpretability can borrow its tools once every graph claim declares the graph it is about, and we report a pre-registered test of our own proposal that failed.

Phongsakon Mark Konrad, Toygar Tanyel, Serkan Ayvaz · University of Southern Denmark and Promake · Seoul, 2026

[OpenReview](https://openreview.net/forum?id=dSfjkJB3bQ) · [PDF](https://openreview.net/pdf?id=dSfjkJB3bQ) · [Markdown](index.md) · [Code](https://github.com/aiml-sdu/path-already-walked) · arXiv · coming soon · Cite this article

Each dot is one of the 144 attention heads, with layers 0 to 11 from left to right. Each line is one of the 950 strongest earlier-to-later edges by the Jacobian measure defined below. Rewiring runs the pre-registered null in your browser, and at 10% density the rich-club coefficient Φ stays at 0.21 however often you press it.

Graph statistics computed on a transformer can reflect preprocessing choices as much as the model. We propose a transformer graph contract, a declaration of nodes, edges, prompts, threshold, null model and behavioural target that is fixed before any statistic is computed. We then map twelve network-neuroscience primitives to transformer questions and state eight translations, each with the result that would refute it. A pre-registered test of two of them on GPT-2 small failed, and the reasons show how much the edge measure and the null decide.

## Abstract

Mechanistic interpretability and network neuroscience both began with single parts, and both now ask how those parts connect. Network neuroscience has two decades of graph measures, null models and known failure modes for that question. We argue that transformers can inherit these tools as methods, and the paper makes three contributions.

First, we state a contract that every graph claim declares before any statistic is computed. It comes with a map from 12 network-neuroscience primitives to transformer questions and with a guide to the null model, the random ensemble of graphs that defines chance. Second, we define a Jacobian measure of how strongly one component drives another, and we state 8 testable translations, each with the result that would refute it. Finally, we ran one pre-registered test of 2 translations on GPT-2 small, and both predictions failed. The normalised rich-club coefficient was 1.00, and the agreement between detected communities and the 7 labelled classes of heads was −0.02.

We found the reasons for the failure only after the test, and they show how much the edge construction and the null model decide on their own. We do not claim that neuroscience results transfer automatically.

### What a bad outcome would have looked like

Our pre-registration named the results that would refute each prediction. The rich club fails if its normalised coefficient sits at or below 1, or if its heads overlap the heads that matter for the task no more than chance would. Modularity fails if the detected communities match the labelled head classes no better than a permutation of the labels. Both failures occurred. A third problem, which we did not write down in advance, settled the rich-club test before any network property could. The edge measure placed almost every strong edge in the first two layers, and the null we chose could not move the statistic for such a club.

Node

A component the claim is about. In our test every node is one attention head.

Edge

A nonnegative strength of influence from one node to another. Here it always runs from an earlier layer to a later one.

EC

Our effective-connectivity measure. It is the squared size of the Jacobian block from one head's output to another's, averaged over prompts, so it measures sensitivity and makes no intervention.

Null model

A random ensemble of graphs that keeps chosen properties fixed. A statistic counts as a finding only if it falls outside what the ensemble produces.

Φ_norm

The rich-club coefficient divided by its value under the null. Values above 1 mean that the best-connected heads link to each other more often than chance.

AMI

Adjusted mutual information, the agreement between two ways of grouping the same heads. It is 0 at chance and 1 for identical groupings.

Contract

The list of declarations, nodes, edges, prompts, threshold, null and target, that a graph claim fixes before any statistic is computed.

## Interpretability is retracing neuroscience's route from parts to wiring

Both fields started with parts that could be named, ablated and counted. Neuroscience had single cells, brain regions and lesion effects, and interpretability had neurons and attention heads.

Both then met units that respond to mixtures of things. Cells in prefrontal cortex mix task variables, and transformers represent more features than they have dimensions, which is called superposition. Both reached for sparse coding. Sparse autoencoders, the interpretability version, now carry sparse coding's known problems, among them decompositions that differ from run to run.

Both fields now draw subgraphs. Neuroscience calls a recurring subgraph a motif and scores it against a null ensemble, while interpretability calls a prompt-specific subgraph a circuit and finds it by patching activations. What neuroscience adds is the habit of computing statistics over all components and comparing them with a null. The parallel is one of method, and we do not claim that transformers are brains.

Tap a row for the detail from the paper.

## A graph claim should say which graph it is about

One transformer induces many graphs. Nodes can be neurons, heads, SAE features or whole blocks, and edges can be weights, activation correlations, patching effects or Jacobians. Each choice of threshold, of symmetrisation and of prompt set can change the answer, and a paper that reports only the final statistic gives the reader no way to tell which of these choices produced it.

The transformer graph contract fixes these choices before any statistic is computed. Signed effects are projected to a nonnegative strength or split into a positive and a negative graph. Directed measures are never quietly swapped for undirected ones, and binary measures get a threshold or a density target that is matched across models. The null keeps what the architecture forces, namely layer order, density and the degree of each node.

A result then has to pass two checks, since its statistic must lie outside what the null produces and it must predict held-out behaviour better than a simple count of components would. If either check fails, so does the claim.

*Figure.* **Figure 1**The contract as five stages. Select one to see what it asks for and what our GPT-2 small test declared there. Blue marks what the contract declares.

Choose each declaration. The checklist applies the paper's rules to your choices, and it computes nothing about any model.

## Every borrowed measure comes with a price of entry

Small-world structure, rich clubs, modularity and controllability each answer a question one could ask of a transformer. None of them means anything until the graph, the projection to edges and the null are declared. Pick a primitive to see the question it asks and what it costs to ask it.

## Eight claims, each written down with the result that would refute it

Each translation turns the analogy into a question that a transformer can answer. Priority records how direct the analogy is, and it says nothing about how likely the claim is to hold. A translation that fails still marks where the analogy stops. We ran the two that were cheapest to test, and hovering their rows lights up the verdicts in entry 07.

## A null model can only test what it does not already build in

If the null lets layer order vary, a statistic that only reflects the architecture will look significant. The rule is short. Keep every nuisance property that could produce the effect by construction, and randomise only the property under test. Choose a research goal to see what the rule asks for.

## One way to measure how strongly a head drives another

Effective connectivity, the directed influence of one unit on another, is where network neuroscience and patching-based circuit work meet. A patching edge records the effect of a finite intervention. Our proxy records infinitesimal sensitivity instead, and the two measures complement each other.

Writing the proxy down forces two declarations that the contract asks for, signed or unsigned effects and proxy or intervention. A rich club is only meaningful against a degree-preserving null, so its coefficient is reported as a ratio to that null.

How close does the proxy come to an intervention? We compared it with finite path patching on 20 edges, the 10 strongest by EC and 10 drawn at random from the retained edges. Pairwise probing grows with the product of the two component sets, and vector-Jacobian products can often cut the number of derivative queries.

*Figure.* **Figure 3**The 10 strongest edges (EC ≈ 4–7 × 10³) and 10 random retained edges (EC ≈ 50–230) have similar finite effects. With a Spearman correlation of 0.38, the proxy ranks edges only weakly as patching does.

## We pre-registered a test of our own proposal. Both predictions failed.

A contract is worth something only if its authors hold themselves to it. We took the two cheapest translations, rich-club ordering and modularity, and tested them on GPT-2 small with indirect-object identification prompts, sentences in which the model must name the person who received something. Scroll through the protocol to see what was fixed and when.

Before running anything we wrote down every contract choice. These were the nodes, the edge measure, both prompt sets, the direction of edges, the threshold, the null and the behavioural target.

We hashed the pre-registration file with SHA-256, recorded the hash before the run and had the script check it again at launch, so the plan could not change after we saw any data.

Edges came from 300 prompts with 16 random probes each. The null drew 1,000 rewirings, the intervals used 1,000 bootstrap samples, and the whole run took 545 seconds on an M3 Pro laptop.

Each prediction was tested one-sided at α = 0.025, a Bonferroni correction over the two. The failure criteria were copied verbatim from Table 2.

Both predictions failed. The verdict cards below record the numbers.

15 templates, filled with names, places and objects that are single GPT-2 tokens. Half the prompts name the indirect object first (ABBA), half the subject first (BABA). The model should continue with the indirect object, and the corrupted run replaces all three names with unrelated ones (ABC).

Examples are drawn in your browser from the script's own templates and word lists, the same way the generator builds them. They are not the specific 600 prompts of the run, which were seeded, 300 for edges and 300 held out.

The rich club was exactly as rich as chance, with a normalised coefficient of 1.00. Its 25 heads shared one member with the 25 heads that matter most for the held-out logit difference. The communities found in the graph did not line up with the seven known classes of IOI heads. As a check on the proxy itself, gradient edges agreed only weakly with path patching.

Runs the pre-registered swap procedure 50 times in your browser, on the real edges at the density chosen in the graph at the top. The verdict comes from the stored run of 1,000 rewirings, marked by the lines.

### Why it failed. The edges measured scale, and the null had no room to move.

We found the reasons below after the test, so they are not part of it. They are the paper's warning in concrete form.

The raw Jacobian is dominated by the output scale of early heads. Mean EC is 161 for edges that leave layer 0, 102 for layer 1, and between 5 and 8 for every later layer. So 927 of the 950 retained edges leave layers 0 and 1, all 25 club heads sit in layers 0, 1 and 3, and the club is a set of whole early layers.

That is where the null runs out of room. Our null keeps each head's degree inside every layer pair, which for a club made of whole layers also fixes the number of edges inside the club. Every null graph reproduced the observed coefficient, and the test had no power. Try it in the graph at the top of the page.

The unnormalised Jacobian is dominated by the output scale of early heads, so **927 of the 950** retained edges leave layers 0 and 1, and all 25 club heads lie in layers 0, 1 and 3.

Bars show the AMI between detected communities and the 7 labelled head classes, and the dashed tick marks the permutation 97.5th percentile. The slider also moves the graph at the top.

### Threshold sensitivity

Modularity passes at 20% density (AMI 0.18, p = 0.02). The pre-registration lists 5% and 20% as report-only checks, so we do not count this as support. It is exactly the threshold dependence that the contract exists to expose.

The example shows one contract failing, and it says nothing yet about the translations themselves. A next test would pre-register a scale-normalised edge and a null that keeps only the global degree sequence and layer order. That would be a new pre-registration, with no re-analysis of this one.

## What this does and doesn't show

This is a position and methodology paper with one experiment. The contracts and translations were tested once, on one small model and one task, and the test failed.

- How much the edge construction and the null model decide. On GPT-2 small they left the test with no power (try the null).

- A contract and eight translations, each with a stated failure criterion, written so that others can run them.

- That a failed test can be reported in full, with the pre-registration, the script and all results available.

- That any translation holds or fails in general. One model, one task, one test (entry 07).

- That neuroscience results transfer to transformers. Transformers are fully observable, discrete and engineered, and brains are partly observable, continuous and biologically constrained.

- That the Jacobian proxy is causal. It is a sensitivity measure (compare with patching), and dense attention can make some efficiency statistics trivial.

A positive result would need a scale-normalised edge, a null with enough freedom to move the statistic, and replication across models and tasks. Small-world scaling against architecture-preserving nulls is still untested, and so is a comparison of connectivity from patching with connectivity from activations.

The main risk is the number of free choices. Graph construction, thresholding, symmetrisation, prompt selection and the null can each change the answer. A useful report shows threshold sensitivity, separates signed from unsigned effects, controls for density, and keeps discovery apart from validation. Without these controls the import adds vocabulary and no explanatory pressure.

## Cite this article

```bibtex
@inproceedings{konrad2026path,
  title     = {A Path Already Walked: On Inheriting Network-Neuroscience
               Tools for Mechanistic Interpretability},
  author    = {Konrad, Phongsakon Mark and Tanyel, Toygar and Ayvaz, Serkan},
  booktitle = {ICML 2026 Workshop on Mechanistic Interpretability},
  year      = {2026},
  url       = {https://openreview.net/forum?id=dSfjkJB3bQ}
}
```

Code, pre-registration and all results are at [github.com/aiml-sdu/path-already-walked](https://github.com/aiml-sdu/path-already-walked). An arXiv version is in preparation.
