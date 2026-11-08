**Name:** Andrew Chen  
**Email:** anc062@ucsd.edu  
**Section:** D31 – Ensemble of Agents  
**Mentor:** Yoav Freund

**1. What is the most interesting topic covered in your domain this quarter?**

Another area of interest is the use of LLM agents for the generation of weak-learners in boosting. In the traditional AdaBoost algorithm used in the Viola-Jones face detection system, each iteration picks from a predetermined pool of weak learners (all Haar features with thresholds) and selects the one with the smallest weighted error. In our approach, multiple agents generate a weak learner written as code in each iteration. The generated candidates are evaluated on a validation set, and the best one is added to the boosting chain, while the sample weights are adjusted such that the next iteration will concentrate on those examples which the boosting chain is still failing to classify correctly. According to boosting theory, it is sufficient for each weak learner to be better than random on the re-weighted data set, hence the agents are not restricted to any particular family of features but can create learners designed to specifically correct the examples that the current model fails.

**2. Describe a potential investigation you would like to pursue for your Quarter 2 Project.**

It would be nice to do the comparison between agent-boosting and standard Haar feature AdaBoost on the same footing in terms of the number of boosting iterations, splitting into training, validation, and test sets, and the evaluation criterion. We will consider the detection rate at different false positive rates (1%, 5%, 10%), number of weak learners needed to achieve certain accuracy, and computational complexity per iteration. Otherwise, we won’t be able to see whether the agents bring any value or just waste time rediscovering Haar features. If the technique proves itself, one can easily extend the idea to our long-term project of detection of humpback whale sounds.

**3. What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**

In our first approach, each of the four team members created an agent that would create an entire, independent cascade, and we would compare the resulting cascades. The difference is that all four agents will compete in every boosting round using the same chain. In every round, each agent creates a weak learner, the agent with the lowest weighted validation error creates the learner, and all agents get feedback based on the re-weighted errors before the next round. It means that the agents will collaborate in one boosting procedure, not compete creating different models.

**4. What other techniques would you be interested in using in your project?**

First, I would like to explore the way the completed chain is segmented into cascade steps, such as the soft cascade method in which the thresholds are set up based on the validation data after the chain is constructed rather than trained individually as described in the original Viola-Jones paper. Second, I would like to see if the diversity of the agents leads to better proposals by using various LLMs (different frontier models and open-weight models), different prompts, and different amounts of context for the misclassified examples.