---
title: "Optimization"
date: 2025-12-07
draft: false
ai_tags: ["cs50", "ai", "notes"]
summary: "Making the Best Choice When Perfection Is Too Expensive - Notes on CS50AI Lecture 3"
---

Have you ever wondered how Google Maps suggests a “good enough” route instead of testing every possible path, or how recommendation systems settle on a decent suggestion without exploring every option?  

### CS50AI-Lecture3 by David J.Milan and Bryan Yu
<iframe style="aspect-ratio: 16 / 9; height: 100% !important; width: 45vw;" src="https://www.youtube.com/embed/qK46ET1xk2A?si=tkRdQNzETU_mJS-7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br>

Lecture 3 of CS50’s AI course introduces **optimization** — the idea that intelligence is often about finding *better* solutions, not *perfect* ones.

In this lecture, we move away from asking *“Is this correct?”* and instead ask *“Is this the best we can reasonably do?”*


# Index
---
1. [What Is Optimization?](#what-is-optimization)
2. [Local Search](#local-search)
3. [Hill Climbing](#hill-climbing)
4. [Local Minima, Plateaus, and Ridges](#local-minima-plateaus-and-ridges)
5. [Random Restart](#random-restart)
6. [Simulated Annealing](#simulated-annealing)
7. [Linear Programming](#linear-programming)
8. [Constraint Satisfaction Problems](#constraint-satisfaction-problems)
9. [Ending Note](#ending-note)
<br><br>

In many real-world problems, AI is not trying to *reach a destination*.  
Instead, it is trying to *improve a situation*.

There may not be a clearly defined goal state. There may not even be a single best answer. There is just a large space of possibilities, and we want one that is reasonably good.

This is where **optimization** comes in.

<br>

# What Is Optimization?
---
Optimization is the problem of choosing the *best available option* from a set of possibilities, according to some measure.

That measure is usually formalised as a function.

Sometimes we want to **maximize** something:
- Accuracy
- Profit
- Satisfaction
- Coverage

Sometimes we want to **minimize** something:
- Cost
- Error
- Distance
- Time

Consider a simple daily decision: how long should you study today?

Studying zero hours is bad. Studying 20 hours is also bad. Somewhere in between lies a balance point. That balance depends on fatigue, deadlines, and diminishing returns. Optimization captures this idea mathematically.

The key shift here is subtle but important:

> We are no longer asking “Is this correct?”  
> We are asking “Is this better than the alternatives?”

<br>

# Local Search
---
Local search approaches optimization the way humans usually do: **incrementally**.

You start somewhere. Anywhere.  
Then you ask: *Can I improve this a little?*

You do not map the entire universe of possibilities. You do not build a full decision tree. You just look around.

Imagine adjusting your chair while studying. You lean back slightly. Better. You adjust the height. Worse. You undo that change. This is local search.

Formally:
- A **state** represents one complete solution.
- A **neighbor** is a solution obtained by a small modification.
- The algorithm remembers only the current state.

This is powerful because it saves memory and computation. It is dangerous because it limits perspective.

<br>

# Hill Climbing
---
Hill climbing is the most straightforward local search strategy.

At every step, it does the same thing:
1. Look at all neighboring states.
2. Pick the one that improves the situation the most.
3. Move there.
4. Repeat.

There is no planning. No backtracking. No regret.

This is why hill climbing feels intuitive. It mirrors how we make many decisions in real life.

If you are looking for better Wi-Fi signal in your house, you move your phone slightly. If the signal improves, you stay. If it worsens, you move back.

Hill climbing works beautifully when the landscape is simple. Unfortunately, most real problems are not.

<br>

# Local Minima, Plateaus, and Ridges
---
Hill climbing fails not because it is stupid, but because it is **too confident**.

### Local Minima
A local minimum is a solution that looks optimal from nearby positions but is far from globally optimal.

Imagine choosing the first decent internship offer you receive. Locally, nothing looks better. Globally, waiting might have produced a stronger option.

Hill climbing stops here and declares victory.

### Plateaus
A plateau is a flat region where all nearby states look equally good.

This is like scrolling endlessly through similar YouTube videos. Nothing feels worse. Nothing feels better. The algorithm does not know what to do next.

Without additional logic, hill climbing stalls.

### Ridges
Ridges are even trickier. Improvement exists, but only if you temporarily move sideways or even slightly downhill.

This is common in learning. Sometimes understanding gets worse before it gets better. Hill climbing refuses to take that risk.

<br>

# Random Restart
---
Random-restart hill climbing is a pragmatic admission: **we may have started badly**.

Instead of trusting one run, the algorithm:
- Starts at a random state.
- Climbs until stuck.
- Starts again elsewhere.
- Repeats many times.

Each run explores a different region of the search space.

This is similar to rewriting an essay from scratch instead of endlessly editing a bad first draft. Sometimes restarting is more efficient than repairing.

Given enough restarts, the probability of finding a global optimum increases sharply.

<br>

# Simulated Annealing
---
Simulated annealing adds one crucial idea: **controlled randomness**.

Early in the process, the algorithm allows itself to make worse moves. This feels counterintuitive, but it is essential.

Why? Because sometimes the only way out of a bad situation is to temporarily accept something worse.

Think of switching careers. The short-term salary drop may be real. The long-term improvement may be worth it.

As time progresses, simulated annealing becomes more conservative. The willingness to accept worse solutions decreases. Eventually, the algorithm behaves like hill climbing.

This balance between exploration and exploitation is one of the most important ideas in optimization.

<br>

# Linear Programming
---
Some optimization problems have a special structure: everything can be expressed linearly.

In linear programming:
- Variables represent decisions.
- Constraints restrict those decisions.
- The objective function is linear.

For example:
- How many units of each product should a factory make?
- How should time be allocated across tasks?
- How can costs be minimized while meeting requirements?

These problems are mathematically elegant and often solvable optimally at scale. When a problem fits this form, linear programming is incredibly powerful.

<br>

# Constraint Satisfaction Problems
---
Constraint satisfaction problems (CSPs) are slightly different.

Here, we are not optimizing a numeric score. We are simply looking for *any solution that satisfies all constraints*.

Sudoku is the classic example. You do not care which valid solution you find. You just need one.

Each CSP has:
- Variables
- Domains
- Constraints

The difficulty lies in managing interactions between constraints. A choice that works locally may cause failure later.

AI solves CSPs by careful ordering, backtracking, and pruning — rejecting impossible paths early before they consume resources.

<br>

# Ending Note
---
Lecture 3 shifts our understanding of intelligence.

AI is not always about finding *the* correct answer.  
Often, it is about finding a **good answer efficiently**, under limited time and resources.

Optimization captures this idea beautifully.

This post is part of my ongoing deep dive into **CS50’s Introduction to Artificial Intelligence with Python**, where I’m documenting my learnings, insights, and interpretations in a practical, simplified form.

If you’re also exploring AI — whether as a student, researcher, or just a curious mind — I’d love to connect and exchange ideas.

📬 Let’s connect on LinkedIn: [linkedin](https://www.linkedin.com/in/soham-gupta-b567b2274/)

More coming soon from future weeks of CS50AI. Stay tuned — and stay curious.
— *Soham Gupta*

> This post is based on ***[CS50’s Introduction to Artificial Intelligence with Python](https://cs50.harvard.edu/ai/2024/)*** — an open course by Harvard University taught by **[David J. Malan](https://cs.harvard.edu/malan/)** and **[Brian Yu](https://pll.harvard.edu/instructor/brian-yu/)**.
>
> You can explore the course materials **[here on GitHub](https://github.com/cs50)**.
