# Chapter 4 Dynamic Programming #

The statements in **COMMENT** are based on the author's understanding, so they may be incorrect.


## Question 1: What is Dynamic Programming (DP)? What are its important properties?

DP refers to a collection of algorithms that can be used to *compute optimal policies* given a *perfect model* of the environment as *Markov Decision Process* (MDP).

DP requires intensive computation and a perfect model, which are insufficient in many cases.

However, DP is theoretically important, because many algorithms follow the idea of DP but with fewer limitations. 

**COMMENT**
When mentioning *optimal policies*, we should think of the Bellman optimality equations in which the optimal value functions, v<sub>\*</sub> or q<sub>\*</sub>, are defined. 
DP *computes optimal policies* by approximating the optimal value functions.


## Question 2 What is policy evaluation (prediction)?

Policy evaluation (prediction) is about how to compute the state-value function v<sub>π</sub> for *an arbitrary policy π*. From the definition of the state-value function, 
the state-value function can be computed by an equation dependent on the policy π and the perfect environment model (recommend to check the equation 4.4 in the book).

There are two methods that can find the state-value function v<sub>π</sub> using the equation: 

1. *Analytical policy evaluation* (named by myself): Given an arbitrary policy and a perfect dynamics model, 
    it is straightforward to list |S| (the number of the states) linear equations to analytically solve the |S| unknowns.
    However, it requires a large amount of computation when |S| is large.
    
    *Further question*: To what extent does the required computation increase as |S| increases? Exponentially? or Linearly? or something else?
   
2. *Iterative policy evaluation*: Repeatedly using the right side of the equation to replace the value of the left side. The state-value function is randomly initialised, 
    but the terminal state must be given a value 0. This method is shown to converge when the discount factor is less than 1 or eventual termination is guaranteed 
    from all states under the policy π (it also is the condition of the existence and uniqueness of v<sub>π</sub>.
    
    To write a computer program to implement iterative policy evaluation, it is normal to compute the value of a state using the new value of its successor state, 
    rather than compute the value of a state after updating all state values. The reason is that the in-place algorithm converges faster, 
    because it uses new data as soon as they are available. Furthermore, the order of updating has a significant influence on the rate of convergence. 
    
    *Further question 1*: Why the terminal state must be given a value 0? 
    
    *Further question 2*: How to prove that the value function convergences under the condition?


## Question 3 What is the expected update?

The expected update refers to a collection of update methods that are based on an *expectation over all possible next states* rather than on a *sample next state*.


## Question 4 What is policy improvement theorem? And how to prove it?

If q<sub>π</sub>(s, π'(s)) >= v<sub>π</sub>(s) for all states, then v<sub>π'</sub>(s) >= v<sub>π</sub>(s) for all states. 
It means if π'(s) can generate an action that leads to a higher discounted reward, then the state-value function of the state under π' is higher than that under π.
Recalling the Bellman optimality equation which *max* state-value function, policy improvement theorem shows a way to maximise the state-value function, 
i.e., always choose the action that has the highest Q-value.

The proof needs to use the definition of action-value function, which can bridge action-value function and state-value function. (Look up the book for more details)


## Question 5 What is policy improvement?

The process of making a new policy that improves on an original policy, by making it greedy with respect to the *value function* of the original policy, 
is called policy improvement. Policy improvement theorm garantees that the value function can be monotonously improved if the policy is updated to take the best actions. 
Furthermore, if the state-value function of a new policy is the same as the state-value function of an old policy, following the Bellman optimality equation, 
they are the optimal policy.


## Question 6 What is policy iteration?

Starting from a random policy, we repeatedly execute policy evaluation and policy improvement. The policy improvement theorem garantees that each policy is a strict improvement over the previous one, unless it is already optimal. Therefore, policy iteration makes the policy improve to be the optimal policy. 


## Question 7 What is value iteration?

Value iteration can be regarded as policy iteration in which policy evaluation is stopped after just one sweep. 
The value function is always updatded using the current optimal policy. 

On the other hand, value iteration is obtained by turning the Bellman optimality equation into an update rule, 
i.e., using the Bellman optimality equation to update the parameters of the value function.


## Question 8 What is asynchronous dynamic programming? Which problems does it want to solve? What are its advantages?

Rather than standard DP that needs to sweep all state space in policy evaluation or value iteration, 
asynchronous dynamics programming update the values of states in *any order whatsoever*, using *whatever values of other states* happen to be available.
It implicates asynchronous DP allow great flexibility in selecting states to update. Asynchronous means updating each state *asynchronously*.
Note that, to converge correctly, asynchronous DP has to update all states before some point in the computation.

Asynchronous DP aims to alleviate the computation required by the standard DP. Standard DP is computationally intensive as it has to sweep all state space. 
Asynchronous DP gives different priorities to every states, and updates them regarding their priority. 

Asynchronous has two advantages:
    
1. Avoid the agent get into unmeanful update. Some state is irrelated to the optimal policy, or some state is more important to learn the optimal policy,
   asynchronous may use good strategies to update these states.
    
2. Combine interactions and updates. As asynchronous DP can select a certain state to update, it can update the state that it is facing, 
   and focus on the most relevant states.

**COMMENT**
Asynchronous DP would be more useful than standard DP as it put more resouces on important things. This strategy is intuitive and reasonable. 
For example, in many cases, some states is irrelated to the optiaml policy so that the agent can totally ignore these states.
As mentioned before, the order of the update has a significant influence on the rate of convergence, so that asynchronous DP may provide a better order to update.


## Question 9 What is generalised policy iteration?

Generalised Policy Iteration (GPI) refers to the general idea of letting *policy-evaluation* and *policy-improvement* processes interact, 
independent of the granularity and other details of the two processes (e.g., which state to be updated, how many policy-evaluations for one policy-improvement). 
There are two important parts in GPI: policy-evaluation and policy-improvement. They are competing and cooperating. 
Policy-evaluation makes policy-improvement inaccurate, and vice versa. However, the two processes interact to find a single joint solution: 
the optimal value function and an optimal policy. 


## Question 10 What is the computation complexity of DP?

In the worst case, the time that DP methods take to find an optimal policy is polynomial in the number of states and actions. 
If *n* and *k* donote the number of states and actions, a DP method takes a number of computational operations that is less than some polynomial function of *n* and *k*.

**COMMENT**
The complexity of policy evaluation is O(n), while the complexity of policy improvement is O(n^k). Therefore, the overall complexity is O(n^k).


