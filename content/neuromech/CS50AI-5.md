---
title: "Neural Networks"
date: 2025-12-21
draft: false
ai_tags: ["cs50", "ai", "notes"]
summary: "Why Stacking Simple Things Starts Feeling Like Thought - Notes on CS50AI Lecture 5"
---

At first, neural networks sound like a metaphor that got out of hand.

We talk about neurons. Layers. Signals. We draw diagrams that vaguely resemble brains. And then we reassure ourselves that none of this is *really* biology — it’s just math. Linear algebra wearing organic metaphors.

### CS50AI-Lecture5 by David J.Milan and Bryan Yu
<iframe style="aspect-ratio: 16 / 9; height: 100% !important; width: 45vw;" src="https://www.youtube.com/embed/J1QD9hLDEDY?si=MFU4dk2PBpZQc1Yw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br>

Lecture 5 sits right at that tension point.

This is where AI becomes powerful enough to feel uncanny, yet simple enough to feel almost disappointing once you look closely. Nothing in a neural network understands anything. And yet, somehow, meaning begins to emerge.

That contradiction is the heart of this lecture.

<br>

# Index
---
1. [Why Single Models Aren’t Enough](#why-single-models-arent-enough)
2. [Neural Networks as Layered Approximation](#neural-networks-as-layered-approximation)
3. [Activation Functions and Non-Linearity](#activation-functions--non-linearity)
4. [Training, Loss, and Backpropagation](#training-loss-and-backpropagation)
5. [Gradient Descent as Slow Adjustment](#gradient-descent-as-slow-adjustment)
6. [Overfitting, Capacity, and Depth](#overfitting-capacity-and-depth)
7. [Why Neural Networks Feel Different](#why-neural-networks-feel-different)
8. [Ending Note](#ending-note)

<br>

Up to now, most of the learning models we saw felt limited in very obvious ways. Nearest neighbors needed memory. Perceptrons needed linear separability. Decision trees grew brittle.

Each model failed loudly.

Neural networks fail quietly.

<br>

# Why Single Models Aren’t Enough
---
A single perceptron can draw a line. That’s its entire worldview.

If the world is separable by straight lines, it works beautifully. If not, it fails completely. There is no graceful degradation. Just wrong answers.

But the real world rarely splits cleanly. Faces are not separated by neat boundaries. Language is not linearly separable. Neither is handwriting, emotion, fraud, or intent.

The response to this limitation is almost embarrassingly simple: stack them.

Instead of one weak model, use many. Let them cooperate. Let their imperfections cancel out.


<br>

# Neural Networks as Layered Approximation
---
A neural network is not intelligent. It is **layered approximation**.

Each layer takes a crude guess at representation and passes it forward. The next layer refines that guess slightly. And then slightly more. And then again.

Nothing magical happens at any layer. The magic, if it exists at all, lies in accumulation.

This feels familiar. Humans rarely understand something all at once. We refine. We revise. We misunderstand, then misunderstand less badly.

Neural networks feel powerful not because they reason, but because they **compress complexity across depth**.

<br>

# Activation Functions & Non-Linearity
---
Without non-linearity, neural networks collapse into something boring.

Stack linear layers and you still get a linear function. Nothing new emerges. No expressive power is gained.

Activation functions break that monotony.

They introduce bends. Thresholds. Saturation. They force the model to care about some signals and ignore others.

This is where the network stops being a glorified equation and starts behaving like a system with preferences.

ReLU. Sigmoid. Tanh. Each choice encodes assumptions about how signals should behave. None are neutral. All shape what the network can learn.

And this is uncomfortable, because it means **architecture is bias**.

<br>

# Training, Loss, and Backpropagation
---
Training a neural network is an exercise in patience.

The system makes a prediction. It is wrong. A number tells it how wrong. That number is loss.

Then comes backpropagation — a deeply unintuitive process that nonetheless works astonishingly well. Errors flow backward. Weights adjust. No single neuron knows why it changed. It just did.

This is not reasoning. It is correction without understanding.

And yet, over time, the system improves.

This is where neural networks feel alien. There is no symbolic explanation. Only gradients nudging numbers in directions that happen to reduce error.

<br>

# Gradient Descent as Slow Adjustment
---
Gradient descent is not clever. It is stubborn.

It takes small steps. Very small steps. Over and over again.

Too big a step and everything breaks. Too small and nothing happens. Choosing the step size is itself an art, not a science.

This mirrors human learning more than we like to admit. We don’t leap into mastery. We inch forward. We regress. We stall. We adjust.

There is something deeply humbling about the fact that so much modern intelligence is built on such an unglamorous idea.

<br>

# Overfitting, Capacity, and Depth
---
With enough layers and enough parameters, a neural network can fit almost anything.

That is not a compliment.

Capacity is power, but it is also danger. A network can learn noise. It can learn bias. It can learn shortcuts that collapse the moment conditions change.

Depth amplifies this risk.

The deeper the network, the harder it becomes to understand what it has learned — or why it fails when it does.

And yet, depth also enables abstraction. The same mechanism that hides understanding also creates it.

This tradeoff never disappears. It only becomes harder to manage.

<br>

# Why Neural Networks Feel Different
---
Neural networks feel different because they resist explanation.

You cannot point to a single rule and say *this is why*. You cannot trace a neat decision path. You get weights. Activations. Distributions.

This frustrates lawyers. Regulators. Philosophers. Anyone who wants reasons.

But perhaps that frustration is revealing.

Human decisions are not as transparent as we pretend. We narrate them after the fact. Neural networks simply refuse to play along.

That honesty — that opacity — is unsettling.

<br>

# Ending Note
---
Lecture 5 does not make AI feel smarter. It makes it feel stranger.

Neural networks do not think. They approximate. They compress. They adjust.

And somehow, that is enough to recognize faces, translate languages, and generate text that sounds like thought.

This should not make us worship them. Nor should it make us dismiss them.

It should make us cautious.

Because intelligence, it turns out, may not require understanding at all.

This post is part of my ongoing deep dive into **CS50’s Introduction to Artificial Intelligence with Python**, where I’m documenting my learnings, insights, and interpretations in a practical, simplified form.

If you’re also exploring AI — whether as a student, researcher, or just a curious mind — I’d love to connect and exchange ideas.

📬 Let’s connect on LinkedIn: [linkedin](https://www.linkedin.com/in/soham-gupta-b567b2274/)

More coming soon from future weeks of CS50AI. Stay tuned — and stay curious.
— *Soham Gupta*

> This post is based on ***[CS50’s Introduction to Artificial Intelligence with Python](https://cs50.harvard.edu/ai/2024/)*** — an open course by Harvard University taught by **[David J. Malan](https://cs.harvard.edu/malan/)** and **[Brian Yu](https://pll.harvard.edu/instructor/brian-yu/)**.
>
> You can explore the course materials **[here on GitHub](https://github.com/cs50)**.
