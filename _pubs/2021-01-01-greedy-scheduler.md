---
layout: base
title: 'Approaching Scheduling Problems via a Deep Hybrid Greedy Model and Supervised Learning'
abstract: 'Scheduling still constitutes a challenging problem, especially for complex problem settings involving due dates and sequence-dependent setups. The majority of existing approaches use heuristics or meta-heuristics, like Genetic Algorithms or Reinforcement Learning. We show that a supervised learning framework can learn and generalize from generated optimal target schedules, which amplifies convergence compared to unsupervised methods. We present a deep hybrid greedy framework, which can predict near-optimal schedules by utilizing the following key mechanisms: (i) Through the interplay between heuristics and a deep neural network our hybrid model can combine the benefits. Specifically, complex patterns from optimal schedules can be learned by a neural network. We reduce the computational costs by outsourcing trivial decisions to heuristics and therefore, allowing consistent decisions during training. (ii) The problem complexity can be reduced, by employing a greedy prediction scheme, where one job at a time is predicted. (iii) We propose a re-scheduling mechanism for idle jobs, which enables long-term cost reduction and renders the framework reactive and dynamic. Through the heuristics and the neural network, our model is real-time capable during inference. We compare our model against prevailing scheduling heuristics and our model outperformed one of them in terms of makespan and lateness minimization. The key purpose of this work is to give a proof of concept, that supervised learning is applicable for complex scheduling problems.'
author:
  - Johann Schmidt
  - Sebastian Stober
conference: 'IFAC INCOM'
doi: '10.1016/j.ifacol.2021.08.095'
link: 'https://www.researchgate.net/publication/356059266_Approaching_Scheduling_Problems_via_a_Deep_Hybrid_Greedy_Model_and_Supervised_Learning'
tags: [Scheduling]
---
