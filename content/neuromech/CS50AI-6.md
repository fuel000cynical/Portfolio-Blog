---
title: "Language"
date: 2025-12-25
draft: false
ai_tags: ["cs50", "ai", "notes"]
summary: "Why Language Is the Hardest Thing We Pretended Was Easy - Notes on CS50AI Lecture 6"
---

Language is deceptive.

It feels natural, almost effortless. We speak before we understand grammar. We read before we know what syntax is. Words arrive so early in life that they stop feeling like a technology at all.

### CS50AI-Lecture6 by David J.Milan and Bryan Yu
<iframe style="aspect-ratio: 16 / 9; height: 100% !important; width: 45vw;" src="https://www.youtube.com/embed/_hAVVULrZ0Q?si=sifr9qhc55XcgWQg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br>

Lecture 6 of CS50’s AI course exposes how misleading that familiarity is. The moment we try to teach language to a machine, the illusion collapses. What seemed intuitive becomes brittle. What felt obvious becomes deeply underspecified.

This lecture is not about language as poetry or persuasion. It is about language as structure, probability, and approximation — and about how quickly meaning slips away when reduced to symbols.

<br>

# Index
---
1. [Why Language Is Hard for Machines](#why-language-is-hard-for-machines)
2. [Words as Data, Not Meaning](#words-as-data-not-meaning)
3. [n-Grams and Local Context](#n-grams-and-local-context)
4. [Probability, Prediction, and Plausibility](#probability-prediction-and-plausibility)
5. [Information Retrieval and Ranking](#information-retrieval-and-ranking)
6. [Parsing and Structure](#parsing-and-structure)
7. [Ambiguity as the Default](#ambiguity-as-the-default)
8. [Ending Note](#ending-note)

<br>

Earlier lectures dealt with environments that could be fully specified: states, transitions, rewards. Language refuses that containment. It leaks context. It depends on history. It changes meaning based on tone, intent, and shared assumptions.

Teaching AI language is not about encoding rules. It is about managing uncertainty at scale.

<br>

# Why Language Is Hard for Machines
---
The difficulty with language is not vocabulary size. It is not grammar either. Those are manageable.

The problem is that language is not self-contained. Every sentence assumes a world beyond itself. Speakers rely on shared knowledge, cultural cues, and expectations that are never written down.

When someone says, “That was great,” the words alone do not tell you much. Tone does. Context does. Prior interaction does.

Machines do not have that background for free. Everything must be inferred or approximated. And inference, as we’ve already seen, is always probabilistic.

<br>

# Words as Data, Not Meaning
---
In AI systems, words are not meanings. They are tokens.

This is an uncomfortable but necessary shift. A model does not know what a “tree” is. It knows how often the token *tree* appears near *leaf*, *branch*, or *forest*. Meaning emerges indirectly, through patterns of use.

This is closer to how dictionaries are written than how humans understand language. Definitions refer to other words. Meaning is relational, not grounded.

What matters, computationally, is not what a word represents, but how it behaves across contexts.

<br>

# n-Grams and Local Context
---
One of the earliest strategies for handling language is to assume that **nearby words matter most**.

An n-gram model predicts the next word based on the previous *n − 1* words. It does not look far back. It does not plan ahead. It reacts locally.

This feels naive, and it is. But it works surprisingly often.

If you hear “peanut butter and…”, you don’t need deep reasoning to guess the next word. Local context carries a lot of weight.

The limitation is obvious. Meaning often depends on long-range dependencies. Sarcasm, references, and narrative structure all break n-gram assumptions. Still, as a baseline, they reveal how much of language is pattern rather than intention.

<br>

# Probability, Prediction, and Plausibility
---
Language models are not trying to tell the truth. They are trying to produce **plausible sequences**.

This distinction matters.

When a model predicts the next word, it is not asserting belief. It is ranking likelihoods based on past data. The output may sound confident, even authoritative, but that confidence is aesthetic, not epistemic.

This explains why language models can generate fluent nonsense. Plausibility does not guarantee correctness. It only guarantees familiarity.

Humans do this too, more often than we admit.

<br>

# Information Retrieval and Ranking
---
Much of language processing is not about generation at all. It is about retrieval.

Search engines, document classifiers, and recommendation systems operate by ranking text based on relevance. The question is never *what does this mean?* but *how useful is this here?*

Techniques like TF-IDF formalize this intuition. Words that appear often in one document but rarely elsewhere become signals of importance.

This reframes language as evidence. Not truth, not meaning — evidence of relevance under a specific query.

It is a pragmatic view. And an influential one.

<br>

# Parsing and Structure
---
Language is not just sequences of words. It has structure.

Parsing attempts to recover that structure by identifying grammatical relationships. Subjects, verbs, objects. Clauses nested inside clauses.

This is where language starts resembling logic again. Trees. Hierarchies. Dependencies.

But natural language resists clean parsing. People interrupt themselves. They omit words. They rely on implication. Formal grammar becomes a rough guide, not a rulebook.

Parsing works best when language behaves politely. Real language rarely does.

<br>

# Ambiguity as the Default
---
Ambiguity is not a flaw in language. It is a feature.

Sentences can mean different things to different people. Sometimes that flexibility is intentional. Sometimes it is unavoidable.

AI systems must choose an interpretation anyway. They cannot remain undecided forever. That choice is often invisible to the user, but it shapes everything downstream.

This is where language processing becomes ethically loaded. When ambiguity collapses into a single interpretation, something is lost. Sometimes nuance. Sometimes fairness.

Language models do not resolve ambiguity. They suppress it.

<br>

# Ending Note
---
Lecture 6 strips language of its mystique.

What remains is not meaning, but structure. Not understanding, but probability. Not intention, but use.

And yet, out of those thin materials, systems emerge that speak convincingly, retrieve intelligently, and sometimes persuade more effectively than humans.

That should not impress us too quickly.

Language, after all, was never just about words. It was about shared worlds. Machines operate without those worlds — and that absence matters.

This post is part of my ongoing deep dive into **CS50’s Introduction to Artificial Intelligence with Python**, where I’m documenting my learnings, insights, and interpretations in a practical, simplified form.

If you’re also exploring AI — whether as a student, researcher, or just a curious mind — I’d love to connect and exchange ideas.

📬 Let’s connect on LinkedIn: [linkedin](https://www.linkedin.com/in/soham-gupta-b567b2274/)

More coming soon from future weeks of CS50AI. Stay tuned — and stay curious.
— *Soham Gupta*

> This post is based on ***[CS50’s Introduction to Artificial Intelligence with Python](https://cs50.harvard.edu/ai/2024/)*** — an open course by Harvard University taught by **[David J. Malan](https://cs.harvard.edu/malan/)** and **[Brian Yu](https://pll.harvard.edu/instructor/brian-yu/)**.
>
> You can explore the course materials **[here on GitHub](https://github.com/cs50)**.
