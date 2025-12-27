---
title: "Learning"
date: 2025-12-13
draft: false
ai_tags: ["cs50", "ai", "notes"]
summary: "Learning as Approximation, Mistake, and Slow Pattern Recognition - Notes on CS50AI Lecture 4"
---

At some point, writing rules stops working.

You can write rules for chess openings. You can write rules for how to drive on an empty road. You can even write rules for how to answer exam questions if the format never changes. But very quickly, those rules begin to crack. There are exceptions. There are edge cases. There are situations where the rule technically applies but feels wrong.

### CS50AI-Lecture4 by David J.Milan and Bryan Yu
<iframe style="aspect-ratio: 16 / 9; height: 100% !important; width: 45vw;" src="https://www.youtube.com/embed/-g0iJjnO2_w?si=_me7SVGLi4_GqMN9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br>

Lecture 4 of CS50’s AI course begins exactly at that fracture point.

This is where artificial intelligence stops being about *knowing* and starts being about **learning**. And learning, it turns out, is not clean. It is noisy. It is inefficient. It involves making the same mistake several times before something finally clicks.

That alone already feels uncomfortably human.

<br>

# Index
---
1. [What Does It Mean to Learn?](#what-does-it-mean-to-learn)
2. [Supervised Learning](#supervised-learning)
3. [Nearest-Neighbor Learning](#nearest-neighbor-learning)
4. [Perceptrons and Linear Decision Boundaries](#perceptrons-and-linear-decision-boundaries)
5. [Decision Trees](#decision-trees)
6. [Overfitting and Generalization](#overfitting-and-generalization)
7. [Reinforcement Learning](#reinforcement-learning)
8. [Ending Note](#ending-note)

<br>

Before this lecture, most AI systems we studied lived in polite, well-defined worlds. The maze existed. The probabilities were given. The costs were known. Even uncertainty had structure.

Learning removes that safety.

Now the system is thrown into the world with incomplete information and told, in effect: *figure it out*. There is no rulebook. There is only experience.

<br>

# What Does It Mean to Learn?
---
When we say a machine “learns,” it’s tempting to imagine something dramatic happening. Some moment of insight. Some internal shift. That’s not what’s going on.

Learning, in the AI sense, is painfully literal. A system is said to learn if its **performance improves with experience**.

That’s it. No understanding. No awareness. Just improvement.

And yet, that definition hides something profound.

Think about how you learned to read people’s moods. No one gave you a formal rule like: *if eyebrows move at angle θ and voice pitch increases by x, then anger*. You were just exposed to situations. Enough of them. Slowly, something settled.

AI learning works the same way. Patterns accumulate. Weights adjust. Errors reduce. Nothing feels intelligent in isolation. Intelligence emerges only across time.

<br>

# Supervised Learning
---
Supervised learning is the most comfortable kind of learning, because it mirrors how we are taught.

There is an input. There is a correct output. Someone tells you when you are wrong.

It’s school. It’s coaching. It’s training with feedback.

Emails labeled spam or not spam. Images labeled cat or dog. Past cases labeled approved or rejected. The AI is not discovering truth here. It is absorbing correlations.

What matters is not that it gets the training examples right. What matters is whether it performs well when the labels disappear.

That is where anxiety enters.

Because a model can look brilliant on data it has already seen. It can also collapse the moment the world changes slightly. And the unsettling thing is that, during training, both models look identical.

<br>

# Nearest-Neighbor Learning
---
Nearest-neighbor learning almost feels like cheating.

There is no deep abstraction. No internal rule. Just comparison.

Something new appears. The system asks: *what does this resemble?* And then it copies the outcome.

This is how recommendation systems work. This is how humans work. We look at similar people. Similar situations. Similar outcomes. We imitate.

It’s crude. It’s shallow. And it works more often than it should.

What bothers me about nearest-neighbor methods is not their simplicity, but their honesty. They don’t pretend to understand. They just say: *this looks familiar*.

In some ways, that is more realistic than elaborate models that claim insight but are just better at hiding their guesswork.

<br>

# Perceptrons and Linear Decision Boundaries
---
Eventually, storing every example becomes impractical. Memory fills up. Comparisons slow down. We want compression.

Perceptrons offer that compression.

They don’t remember individual cases. They remember a **boundary**. A rough dividing line between categories. On one side, yes. On the other, no.

This is elegant. Clean. Mathematical.

And deeply fragile.

Because the world is rarely separable by straight lines. People don’t behave linearly. Risk doesn’t accumulate neatly. Meaning doesn’t split cleanly.

The perceptron’s failure is instructive. It reminds us that every learning model smuggles in assumptions about reality. When those assumptions break, performance collapses — not gradually, but suddenly.

<br>

# Decision Trees
---
Decision trees feel different. They feel explainable. Almost comforting.

If this, then that. Otherwise, something else.

You can trace the logic. You can point to a path. You can say *this is why the decision happened*. Humans love this.

But trees can grow wild. Too many questions. Too many branches. Too much confidence in early splits.

A bad question near the top poisons everything below it. And once again, this feels familiar. First impressions matter too much. Early labels stick too strongly. Correction becomes expensive.

Decision trees quietly teach a lesson: learning is not just about data. It’s about **which distinctions you choose to care about**.

<br>

# Overfitting and Generalization
---
This is where learning turns dangerous.

A model can always be made to fit the past perfectly. Always. You just make it complex enough. Flexible enough. Detailed enough.

But perfection on the past often signals failure in the future.

Overfitting is what happens when a system mistakes noise for structure. When it memorizes accidents. When it falls in love with coincidences.

This is not a machine problem. This is a human problem too.

We overlearn bad experiences. We extrapolate from tiny samples. We see patterns where none exist. We become confident for the wrong reasons.

Generalization — the ability to perform well on what you haven’t seen — is the real test. And it is never guaranteed. Only managed. Carefully. With humility.

<br>

# Reinforcement Learning
---
Reinforcement learning removes the comfort of being told the right answer.

There is no label. There is only consequence.

You act. Something happens. You feel reward or punishment. Over time, behaviour shifts.

This is how animals learn. This is how children learn. This is how habits form.

What makes reinforcement learning unsettling is that it doesn’t care *why* a reward exists. Only that it does. Short-term gains can dominate. Long-term harms can be ignored.

A system optimizes what you reward — not what you intended.

That observation alone should make anyone uncomfortable.

<br><br>

# Ending Note
---
Lecture 4 feels less like computer science and more like psychology wearing mathematical clothing.

Learning systems are not rational in the way we imagine intelligence to be. They are statistical. They are biased by data. They are shaped by feedback. They overfit. They generalize poorly. They improve anyway.

They don’t discover truth. They approximate usefulness.

And maybe that is all intelligence ever was.

This post is part of my ongoing deep dive into **CS50’s Introduction to Artificial Intelligence with Python**, where I’m documenting my learnings, insights, and interpretations in a practical, simplified form.

If you’re also exploring AI — whether as a student, researcher, or just a curious mind — I’d love to connect and exchange ideas.

📬 Let’s connect on LinkedIn: [linkedin](https://www.linkedin.com/in/soham-gupta-b567b2274/)

More coming soon from future weeks of CS50AI. Stay tuned — and stay curious.
— *Soham Gupta*

> This post is based on ***[CS50’s Introduction to Artificial Intelligence with Python](https://cs50.harvard.edu/ai/2024/)*** — an open course by Harvard University taught by **[David J. Malan](https://cs.harvard.edu/malan/)** and **[Brian Yu](https://pll.harvard.edu/instructor/brian-yu/)**.
>
> You can explore the course materials **[here on GitHub](https://github.com/cs50)**.

