# Causal Inference for the Brave and True
This is the summary notes of the book Causal Inference for the Brave and True.  
Link - [here](https://matheusfacure.github.io/python-causality-handbook/landing-page.html)

# Content



# 01 Introducion to Causality

## Data Scientists Have Changed Over Time
Get into the beer, ignore the foam is what Data Scientist should do:
- Math and Statistics have been helpful forever, there are the foundations
- Learn what makes your work valuable and valuable, not the latest fancy tools that no one figured out how to use
- No shorcuts to success. Learn Math and stats!

## Answering a Different Kind of Question
Machine Learning is pretty good at prediction. However, there are drawbacks:
- ML is not panacea, it might give wrong directions if data is wrong. i.e., prices are low during dark seasons in hotel industry while get high when in demand, and models would just draw the conclusion that increasing the price would lead to higher revenue.
- ML is notoriously bad at the above incerse causality type of problem where we want to figure out "what if".
- Causal questions are everywhere and essential to people, life, work, and business. Unfortunately, ML can't answer then merely rely on **correlation-type** prediction methods.
- Figure out how to make association be causation.

## Basic Knowledge of Causal Inference
### One Big Assumption
>We can never observe the same unit with and without treatment.

### Notation
- For the treament intake for unit *i*:  

```math
T_i=\begin{cases}
1 \ \text{if unit i received the treatment}\\
0 \ \text{otherwise}
\end{cases}
```

- Take care of **potential outcomes**:
  - What happened is **factual** and what didn't happen is **counterfactual**
  - $Y_{oi}$ or $Y_i(0)$ is the potential outcome for unit *i* without the treatment
  - $Y_{1i}$ or $Y_i(1)$ is the potential outcome for the same unit with the treatment  
- Individual Treatment Effect 

  $Y_{1i} - Y_{0i}$

- Average Treatment Effect (ATE)  
  
  $ATE = E[Y_{1} - Y_{0}]$
- Average Treatment Effect on the Treated (ATT)  
  
  $ATT = E[Y_{1} - Y_{0}|T=1]$

## Bias Everywhere
Intuitively, we might say the ATE would be the average score in the treatment group minus the average score in the control group, which is  

$E[Y|T=1] - E[Y|T=0]$  

However, for schools that can provide tablets to their students, their $Y_{0}$ is **counterfactual**, we can't observe it, but it should probably bigger than $Y_{0}$ of the untreated schools.  

Hence, we have  
- **Association** is measured by $E[Y|T=1] - E[Y|T=0]$
- **Causation** is measured by $E[Y_{1} - Y_{0}]$

Let's do some math to tell you why **assocaition is not causaltion**. For the treated, the observed outcome is $Y_{1}$, for the untreated, the observed outcome is $Y_{0}$. Then we have,

$E[Y|T=1] - E[Y|T=0] = E[Y_{1}|T=1] - E[Y_{0}|T=0]$

Now, let's add and subtract $E[Y_{0}|T=1]$, which is a counterfactual outcome. We have,

$E[Y|T=1] - E[Y|T=0] = E[Y_{1}|T=1] - E[Y_{0}|T=0] + E[Y_{0}|T=1] - E[Y_{0}|T=1]$

Finally, with a little bit reordering,  

```math
E[Y|T=1] - E[Y|T=0] = \underbrace{E[Y_1 - Y_0|T=1]}_{ATT} + \underbrace{\{ E[Y_0|T=1] - E[Y_0|T=0] \}}_{BIAS}
```

## When Association IS Causation?
- If $E[Y_0|T=1] = E[Y_0|T=0]$, then association IS CAUSATION
- If the treated and the untreated only differ on the treatment itself, **the difference in meanse BECOMES the causal effect**

```math
\begin{align}
E[Y_1 - Y_0|T=1] &= E[Y_1|T=1] - E[Y_0|T=1] \\
&= E[Y_1|T=1] - E[Y_0|T=0] \\
&= E[Y|T=1] - E[Y|T=0]
\end{align}
```

- Also, treated and untreated are exchangeable **prior** and **after** the treatment.
