**Name:** Andrew Chen  
**Email:** anc062@ucsd.edu  
**Section:** D31 – Ensemble of Agents  
**Mentor:** Yoav Freund

**1. What is the most interesting topic covered in your domain this quarter?**

The most intriguing aspect has been generating weak-learners with LLM agents in boosting. In standard AdaBoost as used in Viola-Jones face detection algorithm, each iteration selects from a fixed set of candidates (all possible Haar features with thresholds) and picks the candidate with the lowest weighted error. In our approach, a number of agents generate a weak learner in code form every iteration. The candidates are scored on a validation set, the best candidate becomes part of the boosted chain, and the sample weights are adjusted so that the next iteration emphasizes the examples where the boosted chain performs poorly. According to the theory of boosting, all that is required of each weak learner is to be better than random on the reweighted data, and thus the agents are not restricted to any particular family of features. They can design weak learners specifically for the examples where the current chain fails. The open question I find most intriguing is whether a few reasonable proposals per iteration can outperform an exhaustive search among thousands of cheap features.

**2. Describe a potential investigation you would like to pursue for your Quarter 2 Project.**

I would like to benchmark agent-based boosting against standard Haar feature AdaBoost using the same parameters: number of boosting iterations, same training/validation/testing sets, and the same evaluator. I would evaluate the detection rate for the same false positive rate (1%, 5%, 10%), number of weak classifiers required for the same level of accuracy, and the computation time per iteration. Otherwise, we do not know if the agents provide any value or if they are a costly approach to re-discovering Haar features. Provided that the approach stands up to scrutiny, an obvious extension to this work would be to use the same loop in our ongoing project of detecting humpback whale sounds from seafloor audio.

**3. What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**

In our initial run, each of the four agents created a complete and independent cascade, which was then compared with the other completed cascades. The difference in the algorithm is that in each of the boosting cycles, the four agents will compete on the same chain. In each cycle, the agent with the least weighted validation error is included in the chain, and all agents get feedback about the reweighted errors. This means that the agents will work together in one boosting process as opposed to competing to create different models.

**4. What other techniques would you be interested in using in your project?**

First, I would like to explore the way the completed chain is segmented into cascade steps, such as the soft cascade method in which the thresholds are set up based on the validation data after the chain is constructed rather than trained individually as described in the original Viola-Jones paper. Second, I would like to see if the diversity of the agents leads to better proposals by using various LLMs (different frontier models and open-weight models), different prompts, and different amounts of context for the misclassified examples.

