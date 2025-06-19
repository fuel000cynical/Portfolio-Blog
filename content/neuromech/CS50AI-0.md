---
title: "Search"
date: 2025-06-19
draft: false
ai_tags: ["cs50", "ai", "notes"]
summary: "Making Systems Find Paths - Notes on CS50AI Lecture 0 lecture"
---

Artificial Intelligence, at its very core, is about decision-making. And almost every decision — from finding a path through a maze to defeating an opponent in a game — can be framed as a search problem. Week 0 of CS50’s AI course dives right into this idea, teaching us how to formalize problems so that computers can solve them efficiently.

### CS50AI-Lecture0 by David J.Milan and Bryan Yu
<iframe style="aspect-ratio: 16 / 9; height: 100% !important; width: 45vw;" src="https://www.youtube.com/embed/WbzNRTTrX0g?si=6WdYrCHlK53IJ4YF" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br>

In these notes, I unpack key concepts discussed in the course, state spaces, nodes, and transition models, and explain how different algorithms approach the same search problem in radically different ways — some blindly (uninformed), others intelligently (informed). We also enter the realm of adversarial search, where our program must make optimal decisions against an opponent — the foundation of AI in games.


# Index
---
1. [What is a Search Problem](#what-is-a-search-problem)
1. [Defining a Problem](#defining-a-problem)
2. [The Search Algorithm](#the-search-algorithm)
3. [Various Search Algorithms](#various-search-algorithms)
4. [Adversarial Search](#adversarial-search)
5. [Ending Note](#ending-note)
<br><br>

# What is a Search Problem
---
A search problem is a formal way of describing a situation where an agent must find a sequence of actions that leads from a starting state to a goal state.

In other words:
> A search problem asks: “Given a defined world, how do I reach my goal from where I am right now?”

# Defining a problem
---
To start with solving problems requiring path finding by an algorithm, we first need to be able to define the problem in certain programmable elements. These elements give us a well-defined structure to follow.

### Elements of a problem

1. #### Agent
- The entity that perceives its environment and acts upon that environment.
- The thing that does the action.

2. #### State 
- The Same Configuration of the agent and its environment.
- **Initial State** is the state with which the agent begins with

3. #### Actions
- Choices that can be made in a state
- To be defined as a function **Action(s)** -> where *s* is the current state and the return is the set of actions possible in state s.

4. #### Transition model
- a description of what state results from performing any applicable action in any state. 
- Functions as **Result (s, a)** -> returns the state resulting from performing action *a* and state *s*

5. #### State Space
- a set of all the states reachable from the initial state by any sequence of actions.

6. #### Goal Test
- way to determine whether a given state is a goal state.

7. #### Path Cost
- Numerical cost associated with a given path

8. #### Node
a data structure that keeps track of
- a state
- a parent (node that lead to this node)
- an action (applied to parent)
- a path cost (from initial state to node)

9. #### Frontier
- a data structure contain all possible way forward from all latest node.

<br>

# The Search Algorithm
---
Now that we can define our problem in a much more navigable way, we would start by creating or exploring some algorithms which can be used to find our path. 


### Approach

> - Start with a frontier that contains the initial state
> - **Repeat**: 
> 	1. If frontier is empty, then no solution
> 	2. Remove a node from frontier
> 	3. If node contains goal, return solution
> 	4. expand node, add resulting nodes to the frontier.
>
> Now, in example:
> (We need path from A to E)
> <image src="/image/SearchAlgoDiagram-1.svg" style="width: 30vw;">
>
> So we will have frontier:
>
> A -> B -> C,D -> E,D -> Goal 
>
> *(here we got lucky)*

As you may have already noticed, the above approach might not work every time. **This method may lead to an infinite loop and thus is problematic**. So, we need to look at the problem differently. 

> **Revised Approach**
> - Additional State to frontier
> - Start with empty explored set
> - Repeat:
> 	1. If frontier empty, no solution
> 	2. Remove a node from frontier
> 	3. If node is goal, return solution
> 	4. Add node to explored set
> 	5. Expand Node, add resulting node to frontier (if they are not already in frontier or **explored set**)

<br>

### Choosing which node to remove
When we look at our algorithm, it is to be noted that the efficiency and accuracy of our algorithm is wholly or majorly driven by the selection of which node is to be removed. This is the place where one needs to put some thought into. Thus, the selection criteria we select allows different types of search algorithms to emerge. (Which node to remove is effectively the search algorithm.)

<br>

# Various Search Algorithms
---
Now that we have a grasp of the search algorithms, lets look at some search strategies.
<br><br>

### Uninformed Search Algorithms
A search strategy that uses no problem specific knowledge.

> #### Algorithm 1: Stack System
>  Last in first Out aka *depth first algorithm*
>  (or in other words, an algorithm which removes the node which entered the frontier most recently)  
>
>  Due to the last in first out aspect, this algorithm explores the complete path till the end which a node provides it with. 
>
>**Pros**
>  - Will always find the path in a finite are
> 
>**Cons**
>  - May not be optimal, i.e might give a longer path to the solution than the one available.

> #### Algorithm 2: Queue System
>
> First in First Out aka *Breath first algorithm*
> (or in other words, an algorithm which forms a kind of pipe with entry of nodes from one side and exit from the other side)
>  
> Due to the first in first out aspect, this algorithm explores all the possible paths simultaneously.
>
>**Pros**
>  -  Gives optimal solution due to the fact that the shortest path would hit the goal first.
>
>**Cons**
>  -  May be more memory heavy due to so many paths being explored.

<br>

### Informed Search Algorithms:
A search strategy that uses problem-specific knowledge to find the solutions more efficiently. Since these algorithms require problem specific algorithm making, we will take the classic problem of solving a maze as our example. The algorithm has to find the best (shortest) path from a start point to end point of a maze.

> #### Algorithm 3: Greedy Best-First Search
> This algorithm a basic form of greedy algorithm (as seen in Data Structures and Algorithms), i.e. this algorithm considers only the local optimal and chooses the best. It lacks a global or wider outlook and just thinks as to what would be the best to choose right now. 
> 
> The search algorithm that chooses the node that is closest to the goal as estimated by a *heuristic* function h(n).
> - For maze the heuristic will be manhattan distance.
>> **Manhattan Distance** refers to the distance between the current and the end goal node by counting the nodes we need to go up and then right to reach the end node from the current node.
>
> The optimal solution finding depends on the heuristic.

> #### Algorithm 4: A* (A Star) Search
> A search algorithm that expands node with the lowest value of *g(n) + h(n)*
> where 
> - g(n) = cost to reach node
> - h(n) = estimated cost to goal (using Manhattan Distance)
>   
>  This is only optimal is:
>  1. h(n) is admissible *(never overestimates true cost)*
>  2. h(n) is consistent *(for every node n and successor m with step cost C, h(n) <= h(m) + C)*

<br><br>

# Adversarial Search
---
The adversarial search problem is defined as when 2 search agents opposing each other are trying to find the best way to their optimal solution.

Example: **Tic Tac Toe**

The algorithm which is used here is a recursive minimax function. The reason for naming it Minimax would become clear soon enough.

### Minimax 

We will have two players, Os and Xs.

We shall define it numerically with the following possibilities:
- O wins -> -1
- Tie -> 0
- X wins -> 1

So the *Max* player (X) aims to maximize the score while *Min* player (O) tries to minimize.

##### The Game
- S-0: The initial state
- Player(S): returns which player to move in State S
- Action(S): returns legal moves in state S
- Result(S, A): returns state after action a taken in state S -> transition model
- Terminal(S): Checks if state S is a terminal state **(Game Over State)***
- Utility(S): final numerical value for terminal state(S)

> <image src="/image/Minimax_Algo.svg" style="width: 40vw;">

Here the green triangle is the icon for maximizing while the red triangles are minimizing.
Each Red triangle will have a certain number defining how much it will minimize and thus the algo can choose to depend on priorities.

<br><br>

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