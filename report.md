# Week 4 Report: Auction Mechanism Design for Carbon Permits

## Problem Statement
We are optimizing the **allocative efficiency** of carbon permit auctions. The core problem is determining which auction mechanism from Uniform-Price, Discriminatory (Pay-as-Bid), or Vickrey-Clarke-Groves (VCG), best allocates scarce permits when firms have private information about their abatement costs.

This matters because inefficient allocation, where permits do not go to the firms who value them the most, can represent a massive economic loss for organizations like the EU Emissions Trading System. Our focus will be on the phenomenon of **Demand Reduction** in Uniform-Price auctions. This is where firms strategically underbid on marginal units to lower the market-clearing price.

**Success Measurement:**
* **Primary:** Allocative Efficiency (Ratio of actual value generated to theoretical maximum value).
* **Secondary:** Demand Reduction Index (DRI), which measures strategic bid shading on marginal units.

**Constraints:**
* Firms must not know others' costs (private information).
* Bids must be monotonic ($Price_{High} \ge Price_{Low}$).

## Technical Approach
We model the auction as a partially observable Markov game using **Multi-Agent Reinforcement Learning (MARL)**.

**Mathematical Formulation:**
* **Objective:** Each agent $i$ maximizes profit $\pi_i = \sum v_i(k) - \text{Payment}_i$, where $v_i(k)$ is the value of the $k$-th permit derived from a quadratic abatement cost function.
* **Action Space:** A 4-dimensional continuous vector representing a two-tier demand schedule: $[p^H, q^H, p^L, q^L]$.
* **Mechanism Logic:** The environment sorts bids and clears the market according to the specific rules of Uniform, Discriminatory, or VCG auctions.

**Implementation Strategy:**
* **Environment:** A custom Gymnasium environment `CarbonPermitAuctionEnv` that handles the economic logic (clearing prices, allocating permits, calculating profit).
* **Agents:** Independent PPO (Proximal Policy Optimization) agents, implemented in PyTorch/Stable-Baselines3. Each firm has its own policy network.
* **Validation:** We validate the environment using unit tests that replicate theoretical examples (e.g., verifying that a single firm can lower the clearing price by shading its second bid).

## Initial Results

## Next Steps
