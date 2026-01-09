# 1. Stop Using 80/20 Blindly

The 80/20 train-validation split isn't a principle, it's a habit. After 16 years building ML models on datasets from 50 samples to millions, I still catch myself defaulting to it without thinking. But here's the problem: your validation set isn't decorative. Every decision you make (when to stop training, which architecture to use, whether this model is ready for production) depends on trusting those validation metrics. Trust requires evidence measured in absolute samples, not percentages.

## Why 80/20 Fails at the Extremes

The 80/20 split emerged as a reasonable compromise for moderate-sized datasets. It stuck because it's memorable and passes the gut check. But the math breaks at both ends.

**With small datasets**, 20% doesn't give you enough validation samples to trust anything. Imagine 100 samples across 10 classes. That's only 2 validation examples per class. Your model reports 95% accuracy? Could be real learning. Could be luck. You can't tell the difference, so you can't make confident decisions about whether to deploy, keep training, or collect more data.

**With large datasets**, 20% wastes thousands of samples you paid to label. With 50,000 samples, an 80/20 split puts 10,000 in validation. But you only need 1,000-2,000 validation samples for solid statistical confidence. Those extra 8,000+ samples sitting idle could be improving your model instead.

## Think in Absolute Numbers

Your validation set needs enough samples to give you confidence in your decisions. With 10 examples per class, you're guessing. With 30+ per class, you start trusting the signal. With 100+ per class, you have real confidence for production decisions.

**This means your split should evolve as your dataset grows.** When you have 100 total samples, you might need a 50/50 or 40/60 train/val split just to get enough validation examples per class. As your dataset grows to 1,000 samples, shift to 70/30 — validation is now 300 samples instead of 50. With 10,000+ samples, drop to 90/10 or even 95/5; that's still 500-1,000 validation samples which should yield strong statistical evidence for solid decision making.

The pattern: keep validation size growing in absolute numbers, but shrink the percentage.

## A Concrete Example

On an active learning project starting with fewer than 100 labeled samples across 10 classes, I used a 50/50 split instead of 80/20. Fifty samples for training, fifty for validation. The model barely learned anything, but it learned just enough to score unlabeled samples differently, giving me the signal I needed to identify the next 300 examples worth labeling.

With an 80/20 split, I wouldn't have had enough validation samples to answer the critical question: had the model learned generalizable patterns useful for guiding our next active learning phase? Without sufficient validation data, I couldn't distinguish learning from overfitting. The larger validation set was my compass.

## The Trade-offs

This approach requires actively monitoring your split as data grows, you can't hard code `train_test_split(test_size=0.2)` and forget about it. With 50/50 splits on tiny datasets, your early models will underperform because they're training on less data. But you're trading that initial performance for confident decision-making about what to do next.

## Takeaway

**Count your validation samples per class right now.** Fewer than 30 per class? Your metrics are too noisy to trust—increase validation size even if it means training on less data. More than 100 per class while still growing your dataset? You're wasting training data that could improve your model.

Set a reminder to check this after your next labeling batch. Your split should evolve with your data, not stay frozen at whatever percentage you set on day one.

---

[Back to Contents](../README.md#field-notes)