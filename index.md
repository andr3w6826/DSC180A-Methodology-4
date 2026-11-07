**Name:** Andrew Chen  
**Email:** anc062@ucsd.edu  
**Section:** D31 – Ensemble of Agents  
**Mentor:** Yoav Freund

**1. What is the most interesting topic covered in your domain this quarter?**

The most interesting topic has been using LLM agents as the weak-learner generator inside boosting. In standard AdaBoost, as used in Viola-Jones face detection, each round searches a fixed pool of candidates (every Haar feature with a threshold) and keeps the one with the lowest weighted error. In our setup, several agents each write a weak learner as code every round. The candidates are scored on a validation set, the best one joins the boosted chain, and the sample weights are updated so the next round focuses on the examples the chain still gets wrong. Boosting theory only requires each weak learner to beat chance on the reweighted data, so the agents aren't limited to one feature family. They can design learners aimed at the specific examples the current model misses. The open question I find most interesting is whether a few reasoned proposals per round can match or beat exhaustive search over thousands of cheap features.

**2. Describe a potential investigation you would like to pursue for your Quarter 2 Project.**

I would like to benchmark agent-boosting against standard Haar-feature AdaBoost under identical conditions: the same number of boosting rounds, the same train/validation/test splits, and the same evaluator. I would compare detection rates at fixed false-positive rates (1%, 5%, 10%), how many weak learners each method needs to reach a target accuracy, and the compute cost per round. Without this baseline we can't tell whether the agents add real value or are just an expensive way to rediscover Haar features. If the approach holds up, a natural extension is applying the same loop to our long-term project, detecting humpback whale calls in seafloor acoustic recordings.

**3. What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**

In our first attempt, each of the four team members built an agent that produced a complete, independent cascade, and we compared the finished cascades. The change is to have all four agents compete within each boosting round on a single shared chain. Each round, every agent proposes a weak learner, the one with the lowest weighted validation error is added to the chain, and all agents receive feedback on the reweighted errors before the next round. This makes the agents collaborators in one boosting process rather than competitors building separate models, which is the core idea of an ensemble of agents.

**4. What other techniques would you be interested in using in your project?**

First, I'd like to experiment with how the finished chain is split into cascade stages, for example a soft-cascade approach where rejection thresholds are calibrated on validation data after the chain is built, instead of training each stage separately as in the original Viola-Jones paper. Second, I'd like to test whether diversity among the agents improves the proposals: using different LLMs (frontier models from different providers as well as open-weight models), different prompts, and different amounts of context about the misclassified examples.