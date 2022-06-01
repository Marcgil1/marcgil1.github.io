---
title: "RL Algorithms"
date: 2022-04-01
draft: false
---

You may find the project [here](https://github.com/marcgil1/rl_algorithms).

Reinforcement Learning (RL) is an area of AI whose main problem is determining
the actions an agent should take in its environment in order to maximise some
reward. An example of this would be an agent playing chess: At each timestep,
the agent may choose to take an action (moving a piece), thus alterating its
environment (changing the state of the board). When finishing the game, it
receives either a reward of +1 if the play was won, a penalty of -1 if it lost,
or 0 if got to stalemate, thus being able to decide how beneficial the
decisions taken were.

In this repo, there are implementations for some of the basic algorithms of
Deep RL, an area combining RL with Deep Learning.

All implementations are based on an Agent class presenting methods for:

- Taking an action given some observation.
- Observing the result of the taken action.
