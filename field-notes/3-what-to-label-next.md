# Which Samples Should You Label Next?
You've got a backlog of 100,000 unlabeled datapoints but time and budget to annotate only 500 this sprint. Which ones should you pick?

This isn't academic. For nearly all supervised learning tasks, collecting and labeling training data is your biggest cost; not model training itself. The human time investment to assign labels and review quality is immense. Supervised models require thousands if not millions of annotated samples to learn useful patterns. Even if data collection and annotation is cheap ($0.50 / sample) your annotation budget will dwarf your training bill. More importantly, data annotation takes significantly longer (weeks or months) than model training (hours or days) which is often the biggest bottleneck to model development cycles.

You want to maximize model progress each development cycle. This means maximizing the learning opportunities in the samples you are adding to your training data; so which samples do you select to achieve this? The ones your model is most challenged or confused by, right? Smart! But only prioritizing these examples (model uncertainty sampling) is not enough. You'll end up annotating hundreds of slightly different examples of only the worst edge cases for your current model.

The better answer: prioritize sample diversity first, then model uncertainty within each diverse bucket.

## Why Uncertainty Alone Fails
Imagine a model that detects if workers are wearing their hardhat in a heavy construction zone. Maybe the model currently struggles when a worker's hardhat is partially obscured. You want to improve on this, but you don't want your entire sample budget to be of only partially obscured hardhats. You model has other weak points you need to focus on too (hard hat color, worker pose, etc.). If you sample exclusively from the samples the highest model uncertainty, you will burn the majority of your annotation budget on slight variations of one problem area.

Worse, this additional negative impacts:

1. Catastrophic forgetting: Your model gets significantly worse in areas it was once very good at (e.g., it gets really good at detecting partially obscured hardhats but forgets how to hardhats on workers directly in front of the camera)
2. Distribution drift: Your training set stops looking like the real world your model will see in production (e.g., the model begins to expect that mostly hard hats will be partially obscured when the reality is this a minority edge case)

## Why Diversity Alone Fails
Sampling based on data diversity is always a safe bet. We want our model generalize across all of our data rather than learning patterns that work for only specific pockets. That said, if you pick the most diverse 500 samples and you might label a bunch of easy, well-separated examples your model already handles fine. You're burning annotation budget on confirmation rather than learning.

## Cluster Before You Sample
The key insight: Diversity first guarantees you're sampling from across your data. Uncertainty second guarantees you're learning within each region of the space.

Step 1: Cluster your unlabeled pool of data
Use embeddings from your model's penultimate layer to cluster all unlabeled examples. Aim for 20-50 clusters depending on your dataset size and diversity.

Step 2: Calculate uncertainty scores
Run inference and get model uncertainty for every unlabeled example. There are many ways to estimate model uncertainty, but a tried and true approach to train multiple versions of a model and check for prediction disagreement on unlabeled examples.

Step 3: Sample top-k uncertain per cluster
Within each cluster, take the most uncertain examples. If you need 500 labels across 25 clusters, that's ~20 per cluster. This guarantees diversity because you're forced to sample from every region of your data space, while focusing your attention on the most uncertain examples in each region.

## Takeaway

Think of it like studying for an exam. You want to practice problems you struggle with (model uncertainty), but you need to make sure you're covering all topics (data diversity). 

Next time you're selecting data to label, run this two-step filter: First, cluster your unlabeled pool into 20-50 groups using your model's embeddings. Then, within each cluster, select the most uncertain examples. You're not hoping diversity emerges from your sample. You're building it in.