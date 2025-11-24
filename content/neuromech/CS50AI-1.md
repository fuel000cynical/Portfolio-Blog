---
title: "Knowledge"
date: 2025-11-24
draft: false
ai_tags: ["cs50", "ai", "notes"]
summary: "Inferring and Creating Logic  - Notes on CS50AI Lecture 1"
---
To understand how to build Artificial Intelligence we must have an understanding of how a machine can *think* about information. Before an algorithm can plan, predict, or act, it needs a structured way to represent what it knows and what it can infer from that knowledge. **Lecture 1 of CS50’s AI course, Knowledge**, introduces this foundation by exploring propositional logic, inference rules, and model checking. These tools allow an AI system to move from raw facts to meaningful conclusions, much like how humans reason step-by-step. This lecture sets the stage for everything else in AI: once a machine can represent knowledge clearly, it can begin to reason intelligently.

### CS50AI-Lecture1 by David J.Milan and Bryan Yu
<iframe style="aspect-ratio: 16 / 9; height: 100% !important; width: 45vw;" src="https://www.youtube.com/embed/HWQLez87vqM?si=mwrK019gVCeDRAgt" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br>

In these notes, I unpack key concepts discussed in the course, what is knowledge, sentences, proportional logic, different logical connectives and how we can draw inferences from them, models and model checking, some inference rules, and lastly what are the limitations to the models discussed.

# Index
---
1. [What is Knowledge?](#what-is-knowledge)
2. [Propositional Logic](#propositional-logic)
3. [Logical Connectives](#logical-connectives)
4. [Implication vs Biconditional](#implication-vs-biconditional)
5. [Inference](#inference)
6. [Models & Model Checking](#models--model-checking)
7. [Inference Rules](#inference-rules)
8. [Resolution](#resolution)
9. [Uncertainty & Limitations](#uncertainty--limitations)
10. [Ending Note](#ending-note)
<br><br>

# What is Knowledge?
---
It's giving the computer the ability to use information from the world by reasoning based on some pre-entered information, i.e. knowledge.

In computer terms, **knowledge** is:
- Facts about the world  
- Rules that connect those facts  
- Logical structures that allow inference  

Example:  
- *It is raining.*  
- *If it is raining, the ground gets wet.*  
→ So the ground is wet.

This is the simplest form of **deterministic reasoning**.

AI systems rely on this kind of structure to move from known facts → conclusions.

Now, while we humans use language, we have to be formal and have some set elements to train an AI on this. 

> ### Sentence
> One of the most basic element that we must define is the sentence. It's an assertion about the world in a "knowledge representation language."  

As we move forward, we need to understand proportional logic, the logic we are gonna be using to reason.

<br>

# Propositional Logic  
---
Propositional logic uses **propositions**—statements that are either **true** or **false**.

Some examples of these propositions:
- P: “It is raining.”
- Q: “The sky is cloudy.”
- R: “Soham is coding.”

In each of these statements there is no “maybe”. Each statement can either be right or wrong.
Everything is binary at this level.

Propositional logic is the simplest logical system and forms the base for more complex reasoning (like first-order logic).

<br>

# Logical Connectives  
---
As we move forward to making our AI understand this and reason, we need to define a method by which the AI can check for the proportional logic of statements in a combined form. Thus, we use connectives. Connectives combine propositions to form more expressive statements.

The connectives we shall be using are: 
### **1. NOT (¬P)**  
Takes a statement and flips its truth value.  
If `P = True`, then `¬P = False`.
### **2. AND (P ∧ Q)**  
True only if *both* P and Q are true.
| P | Q | (P ∧ Q) |
|----|----|----|
| True | True | True |
| True | False| False|
| False| True | False|
| False| False| False|
### **3. OR (P ∨ Q)**  
True if *at least one* of P or Q is true.
| P | Q | (P ∧ Q) |
|----|----|----|
| True | True | True |
| True | False| True |
| False| True | True |
| False| False| False|

### **4. IMPLIES (P → Q)**  
“If P is true, then Q must be true.”

This is quite an important logical connection. One way to explain this is by example. 
<br>
We are given the sentence that "A will go out, if it doesn't rain"
Here, the statement "it doesn't rain" is P and "A will go out" is Q, so if P is true, i.e. it doesn't rain, Q will be true -> A will go out.

### **5. BICONDITIONAL (P ↔ Q)**  
True if P and Q share the same truth value.

The statement is such that if P is true then Q will be true, and vice-versa. 

<br>

# Implication vs Biconditional
---
It's quite important to note the difference between these two logical connectives as this is a common source of confusion.


### **Implication (P → Q)**  
Only says:  
> When P happens, Q must follow.

But Q can be true without P.

Following this with an example, we have the statement, "If it doesn't rain, A will go out". Here, we can say that if it doesn't rain then A will go out, but we can't say that if A went out, it wasn't raining. The condition is one directional.


### **Biconditional (P ↔ Q)**  
Says:  
> P is true **exactly when** Q is true.  
They depend on each other.

Following this with an example, we have the statement, "Only if it doesn't rain, A will go out". Here, we can say that if it doesn't rain then A will go out, and we can also say that if A went out, it wasn't raining. The condition is thus for both the statements with respect to the other.


<br>

# Inference  
---
Inference is the process of taking known facts and deriving new facts. It is the base of our knowledge system and the output. To illustrate the meaning of inference, the following example is take.

Example:  
- Fact: “All men are mortal.”  
- Fact: “Socrates is a man.”  
- Conclusion: “Socrates is mortal.”

This is a deductive chain. It is now our task to examine how we may build AI systems that can reason through such statements and thus automate such chains.

# Models & Model Checking  
---
A model is an assignment of a truth value to every propositional symbol. A **model** assigns true/false values to each proposition to form a possible world. [It is to note that if there are "n" variables which are propositional symbols, then the possible worlds are 2 raised to the power n].

An example model:
- `P = True`
- `Q = False`
- `R = True`

A model is *valid* if it satisfies all the statements in our knowledge base.

> The **Knowledge Base (KB)** is a set of sentences known by a knowledge-based agent. We use this to draw conclusions.
> 
>Example KB:
>P → Q
>P
>
>We can ask the KB:  
>> “Is Q true?”
>
>If all models where the KB is true also imply Q → we can infer Q.


### **Model Checking**  
Model Checking is the simplest algorithm possible to make a computer have knowledge and reason through it. In this setup, we check all possible models and see which ones satisfy the rules.

An example that we can use to see is let's say we need to check if the Knowledge Base (KB) entails A. (Entailment refers to the state in which in every model in which KB hold true, A will also hold true).

Example: We have three sentences.
- P: "Its Tuesday"
- Q: "It's Raining"
- R: "Harry will go for a Run"

And let's have the KB to be (P ∧ (¬Q)) → R
Or, in simple english, If it's Tuesday (P) AND it's NOT Raining (¬Q), then Harry will go for a Run (R).

Then, the model checking would first enumerate all possible models:
| Sno. | P | Q | R | KB |
|---|---|---|---|---|
|1|False|False|False|False|
|2|False|False|True|False|
|3|False|True|False|False|
|4|False|True|True|False|
|5|True|False|False|False|
|6|True|False|True|True|
|7|True|True|False|False|
|8|True|True|True|False|

Here, we remove world 1,2,3,4 as the propositional symbol P is false, while we remove 7,8 as ¬Q is false. Now, we needed to find a world where if P and ¬Q, then R must be true. 

Thus, there is only world 6 where our KB entails A, this shall be our inference and output.

> ### Knowledge Engineering
> This is the process in which one takes a problem and figures out how to distill it into symbols. An example can be is the that the famous game, Cluedo, can be distilled into symbols.

This method is noted to be accurate but slow as propositions grow (exponential explosion).

<br>

# Inference Rules  
---
To make it possible for AI to infer particular propositional symbol's value from other symbols, we certain set inference rules. These are:
### **1. Modus Ponens**  
P → Q
P
∴ Q

The most fundamental inference rule.

### **2. And-Elimination**  
From `P ∧ Q` we can infer `P` or `Q`.

### **3. Or-Introduction**  
From `P`, we can infer `P ∨ Q`.

These rules allow AI to build step-by-step chains of reasoning.

<br>

# Resolution  
---
Resolution is a single inference rule powerful enough to replace all others.

The idea is to:
- Convert everything to **CNF (Conjunctive Normal Form)**  
- Use resolution rule on clauses  
- Derive contradictions to prove things

An example:
If we have (P ∨ Q) and another knowledge to be (¬Q ∨ R) <br> then, (P ∨ R)

Resolution is widely used in SAT solvers and automated reasoning systems.

<br>

# Uncertainty & Limitations  
---
We know that pure propositional logic is powerful but, its limited by the following:
- It cannot handle uncertainty  
- It grows exponentially with more variables  
- It cannot express relationships like “Soham is taller than Sam” (which requires first-order logic)

Later in the course, probabilistic reasoning (Bayes, HMMs, etc.) will fix these issues.

# Ending Note  
---
This post is part of my ongoing deep dive into **CS50’s Introduction to Artificial Intelligence with Python**, where I’m documenting my learnings, insights, and interpretations in a practical, simplified form.

If you’re also exploring AI — whether as a student, researcher, or just a curious mind — I’d love to connect and exchange ideas.

📬 Let’s connect on LinkedIn: [linkedin](https://www.linkedin.com/in/soham-gupta-b567b2274/)

More coming soon from future weeks of CS50AI. Stay tuned — and stay curious.
— *Soham Gupta*

> This post is based on ***[CS50’s Introduction to Artificial Intelligence with Python](https://cs50.harvard.edu/ai/2024/)*** — an open course by Harvard University taught by **[David J. Malan](https://cs.harvard.edu/malan/)** and **[Brian Yu](https://pll.harvard.edu/instructor/brian-yu/)**.
>
> You can explore the course materials **[here on GitHub](https://github.com/cs50)**.