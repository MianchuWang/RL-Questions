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
