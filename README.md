# ML Field Notes: Building Models That Work

For ML engineers who've hit the limits of tutorials. Battle-tested insights on training, debugging, and shipping models that actually work in the real world.

## [Field Notes](field-notes/README.md)

## Series Overview

Your model hits 95% accuracy on the validation set, then crashes to 30% in production. Your active learning loop labels the same examples repeatedly. Your "balanced" dataset still fails on minority classes that actually matter. **ML Field Notes** tackles these real-world problems with battle-tested solutions from 16+ years of applied machine learning and computer vision experience across the financial, defense, and critical infrastructure industries.

Each post dissects one specific problem with a practical solution you can apply immediately; the kind of knowledge that only comes from debugging failures late into the night, optimizing models under production deadlines, and navigating the messy reality where clean datasets don't exist.

### What You'll Learn

This series covers the nuanced, often overlooked aspects of building production ML systems:

- **🚀 Production Reality**: Planning for model drift, monitoring that matters, and building systems that survive deployment
- **🏗️ Model Validation**: Detecting when your model learns shortcuts, identifying systematic errors, and avoiding validation set overfitting
- **🔍 Data & Evaluation**: Why 80/20 splits fail, how much label noise you can tolerate, and what to label next
- **📊 Practical Strategies**: Active learning that works in practice, handling class imbalance pragmatically, and solving cold-start problems
- **⚙️ Architecture Decisions**: When to add more data vs. better models, understanding learning curves, and recognizing architectural limits

### Who This Is For

You'll get the most value from these posts if you:
- Ship models to production (or need to soon) and face real-world constraints
- Debug models that work in development but fail in deployment
- Make architecture decisions without clear guidance (more data vs. better model?)
- Deal with messy data, label noise, and class imbalance in practice
- Want to make better decisions faster, informed by battle-tested experience

---

