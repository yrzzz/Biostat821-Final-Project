# Weight sampler

# Index:
  * [TrainablePosteriorDistribution](#class-TrainablePosteriorDistribution)
  * [PriorDistribution](#class-PriorDistribution)

---
## class TrainablePosteriorDistribution
### BayesianNeuralNetwork.modules.weight_sampler.TrainablePosteriorDistribution(mu, rho)
Creates a weight sampler in order to introduce uncertainity on the layers weights.
#### Parameters:
  * mu - torch.tensor with two or more dimensions: mu parameter of the Gaussian weight sampler
  * rho - torch.tensor with two or more dimensions: rho parameter of the Gaussian weight sampler

#### Methods:
  * sample():
  
    Returns a torch.tensor corresponding to the sampled weights of the layer. Also stores the current distribution sigma and weights internally for further use.
  * log_likelihood_posterior():
  
    Returns the torch.tensor corresponding to the summed log-likelihood of the sampled weights given its mu and sigma parameters, considering it follows a Gaussian distribution.
    
---

## class PriorDistribution
### BayesianNeuralNetwork.modules.weight_sampler.PriorDistribution(pi, sigma1, sigma2)
Creates a log-likelihood calculator for any matrix w passed on the log_prior method, considering a Scaled Gaussian Mixture model of N(0, sigma1) with weight pi (parameter) and N(0, sigma2) with weight (1-pi) parameter for each distribution.
#### Parameters:
  * pi - float corresponding to a factor for scaling the mixture models; AND
  * sigma1 - float corresponding to the standard deviation for the first Gaussian Model of the mixture; AND
  * sigma2 - float corresponding to the standard deviation for the second Gaussian Model of the mixture; OR

  * dist - torch.distributions.distribution.Distribution corresponding to a prior distribution different than a normal / scale mixture normal; if you pass that, the prior distribution will be that one and sigma1 and sigma2 and pi can be dismissed. - Note that there is a torch issue that may output you logprob as NaN, so beware of the prior dist you are using.

#### Methods:
  * log_likelihood_prior(w):
  
    Returns the torch.tensor corresponding to the summed log-likelihood of the matrix of weights "w" given PriorWeightDistribution object scaled Gaussian Mixture model parameters.
    ##### Parameters:
      * w - torch.tensor
---
