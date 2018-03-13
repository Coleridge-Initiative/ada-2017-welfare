# Machine Learning

## Motivation
You've probably heard about machine learning, artificial intelligence, etc. It's 
an integral part of data science. So we'll teach you the basics about ML: the 
process, formulating a problem in a machine learning setting, feature generation,
model selection and evaluation, and how to interpr features et results before eventually deploying the models. 

Doing machine learning in a social science setting: People coming from social science or statistics might be alarmed at throwing every possible predictor. It's important to know that the predictors are being used for a specific purpose (say prediction) and not necessarily a probability of an event.

- Mapping a social science problem to an ML problem 
  - Defining the goals
  - Setting up an objective function
  - Ethical questions 
  - Potential for misuse 
  - Implicit and explicit assumptions
  - Sources of bias in sample and labels
- Data Acquisition and Integration
- Feature Generation
- Modeling
  - supervised vs unsupervised
  - which set of models to use
  - which hyperparameters
- Evaluation
  - Offline (based on historical data)
    - Metrics
      - AUC/precision/recall
      - Deciding on a reasonable metric (ranked list/precision at top K)
    - Methodology
      - in sample
      - out of sample
        - Constructing training/test split
        - Generalizability 
        - Cross Validation
          - Temporal CV and Leakage
          - Choosing granularity/observation level
          - Choosing prediction date
          - Difference between training window and aggregation window (features)
- Deployment
  - How does model update when more data is added  
