# Chapter 5 Monte Carlo Methods

## Question 1 What is the Monte Carlo Method? What is the basic idea behind it?

Monte Carlo Methods refer to a collection of estimation algorithm whose operation involves a significant random component (estimate value functions). 
In Sutton's book, Monte Carlo Methods are a collection of methods based on averaging complete returns.

As value function is the expected return, an obvious way to estimate it is to average the returns observed after visits to that state. 
As more returns are observed, the average should converge to the expected value. 

## Question 2 What is first-visit MC and every-visit MC?

first-visit MP: Given a trajectory, update a state only using the part of the trajectory after the first apperance of the state (Monte Carlo). 
every-visit MP: Given a trajectory, update a state using the parts of the trajectory after every appearance of the state (function approximation, eligibility traces). 

All of them converges to the expected return. 

## Question 3 What is the advantages of MC methods, compared with DP?

1. The estimate of a state are independent of that of other states, so we can only estimate the states that are interested. 
   Furthermore, the computational expense of estimating the value of a single state is independent of the number of states.
2. MC methods can learn from actual experience. 
3. MC methods can learn from simulated experience. This method requires a learnt model, 
   however learning a model that can generate states from a desired probability distribution is much easier to learn a distribution in explicit form.

## Question 4 When π is deterministic, why does estimation of action values require exploration, and that of state values doesn't?

Monte Carlo estimation of action values is to estimate q<sub>π</sub>(s, a). 
If π is deterministic, the action under the state will be always the same, so not all state-action pairs are visited. 
Therefore, the agent does not know the value of other action, which makes policy improvement infeasible. 

For estimation of state value, which requires a model, the agent can sample many actions, and estimate the expected return of the next state, 
and chooose the most promising action. Here all states can be visited.

In Sutton's book, he proposes a exploration method named *exploring starts*, i.e., every state-action pair has a nonzero probability of being selected as the start.


## Question 5 What is the Monte Carlo control with exploring starts?

**Version 1 MCES based on GPI** 

The MCES are finding the optimal policy based on two assumptions:
   1. An infinite number of episodes, and
   2. The episodes are generated with exploring starts.
 
 Firstly, MCES estimates the action value function using an infinite number of epidoes.
 Then, it does policy improvement (policy improvement theorem guarantees its convergence).
 
 **Version 2 MCES based on value iteration**
 
 The MCES are finding the optimal policy based on only one assumption: the episodes are generated with exploring starts.
 Version 2.1 and Version 2.2 are algorithms that aims to remove the first assumption in Version 1.
 
 **Version 2.1** This version uses a index to measure the error of the estimated action value. If the error is small enough, we can then do policy improvement. 
 Although this approach can probably be made completely satisfactory in the sense of guaranteeing correct convergence up to some level of approximation. However, it is also likely to require far too many episodes to be useful in practice. 
 
 **Version 2.2** This version is similar to value iteration that does not requires the completion of value evaluation. 
 In MCES, update the policy under a state once the update the action value function of the state-action pair. 
 
   **Problem of Version 2.2** Regardless the policy, all trajectories are saved to compute the action value function. 
   Although the value function seems converge to a suboptimal policy(I think), it is easy to prove that the value function will converge to the optimal policy. 
   Let's prove that: if the policy converges to a suboptimal, the value function will converge to the correpsonding value, 
   so the policy can be improved to a better policy. (Have not properly proved yet)
 
 






