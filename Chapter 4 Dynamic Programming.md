# Chapter 4 Dynamic Programming #


### Question 1: What is Dynamic Programming (DP)? What are its important properties?

DP refers to a collection of algorithms that can be used to *compute optimal policies* given a *perfect model* of the environment as *Markov Decision Process* (MDP).

DP requires intensive computation and a perfect model, which are insufficient in many cases.

However, DP is theoretically important, because many algorithms follow the idea of DP but with fewer limitations. 

**COMMENT**
When mentioning *optimal policies*, we should think of the Bellman optimality equations in which the optimal value functions, v<sub>\*</sub> or q<sub>\*</sub>, are defined. 
DP *computes optimal policies* by approximating the optimal value functions.


### Question 2 What is policy evaluation (prediction)?

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


### Question 3 What is the expected update?

The expected update refers to a collection of update methods that are based on an *expectation over all possible next states* rather than on a *sample next state*.






