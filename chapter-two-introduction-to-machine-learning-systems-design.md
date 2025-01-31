# Introduction to Machine Learning Systems Design

## High Level Overview of the Chapter

Re-iterating from the first chapter, ML systems design takes a system appraoch to MLOps
>:bulb: MLOps is an ML culture and practice that unifies ML application development (Dev) with ML system deployment and operations (Ops).

In general, there are four requirements that guide the developement of the ML system:
1. Reliability
2. Scalability
3. Maintainability
4. Adaptability


Now, before designing a ML algorithm to solve a problem, the primary important thing is to **frame the problem into a task that ML can solve**. This will be talked in this chapter


Lastly, the last part of this chapter touches on a debate that has consumed much of the ML literature in recent years: which is more important—data or intelligent algorithms?

## Key Takeaways


1. Changing the way you frame your problem might make your problem significantly harder or easier.
2. When there are multiple objectives, it’s a good idea to decouple them first because it makes model development and maintenance easier. 
    - First, it’s easier to tweak your system without retraining models.
    - Second, it’s easier for maintenance since different objectives might need different maintenance schedules.
3. More data doesn’t always lead to better performance for your model. 
    - More data at lower quality, such as data that is outdated or data with incorrect labels, might even hurt your model’s performance.


## Business and ML Objectives

### What is causing short-lived ML projects?
Here is something that needs to be addressed straight out:
>:small_red_triangle_down: most companies don’t care about the fancy ML metrics..... unless it moves some business metrics

A pattern common in many short-lived ML projects is that the data scientists become too focused on hacking ML metrics without paying attention to business metrics

As ML engineers, we should keep in mind that:
- The ultimate goal of any project within a business is **to increase profits**, either directly or indirectly 
For an ML project to succeed within a business organization, it’s crucial to tie the performance of an ML system to the overall business performance. What business performance metrics is the new ML system supposed to influence, e.g., the amount of ads revenue, the number of monthly active users?


## Requirements for ML Systems

### General requirements

Most successful ML systems need to satisfy the following four requirements (more could be needed):
1. Reliability
2. Scalability
3. Maintainability
4. Adaptability


### Reliability
The system should continue to perform the correct function at the desired level of performance even in the face of adversity (hardware or software faults, and even human error).

Something to note here is:
1. “Correctness” might be difficult to determine for ML systems. For example, your system might call the predict function—e.g., model.predict()—correctly, but the predictions are wrong.
2. Unlike traditional software systems that often gets a runtime error / 404, **ML systems can fail silently**
    - End users don’t even know that the system has failed and might have kept on using it as if it were working.



### Scalability

There are multiple ways an ML system can grow, but just to name a few:
1. Grow in complexity -> simple model growing into 100-million-parameter neural net
2. Grow in traffic volume -> 10, 000 daily prediction request into 10 million daily predictions
3. Grow in ML models count -> first you only had a model to detect trending topics. Then you introduce a second model in that use case to filter out NSFW trending tweets.


Whichever way your system grows, there should be reasonable ways of dealing with that growth.

- When talking about scalability most people think of resource scaling, which consists of up-scaling (expanding the resources to handle growth) and down-scaling (reducing the resources when not needed).
- Resource scaling is not the only concern in scalability; so is artifact management. When you have hundreds of models you need a repeatable and programmatic way to monitor, retrain and deploy a model. You can probably do all these manually if you only have a few.
- The book touches more on the topic of scalability in other sections: Distributed Training, Model Optimisation, Resource Management, Experiment Tracking and Versioning, Development Environment.



### Maintainability

People of very different backgrounds, with very different programming languages and tools, and might own different parts of the process for a ML project. 

Hence, the following need to be emphasized for maintainability of the project:
- Code should be documented
- Code, data, and artifacts should be versioned.
- Models should be sufficiently reproducible so that even when the original authors are not around, other contributors can have sufficient contexts to build on their work. 
- More on this topic in the "Team Structure section in Chapter 11".


### Adaptability
Data distributions and business requirements shift fast. Your system needs to be able to adapt to these natural shifts easily.


## Iterative Process

The main emphasis in this secion is: developing an ML system is an iterative and, in most cases, never-ending process. Once a system is put into production, it’ll need to be continually monitored and updated.

This is best illustrated via figure below. 

![ML_iterative_process](Assets/2-introduction-to-machine-learning-systems-design-assets/ML_iterative_process.png)

The process can be summarized as follows:
1. Step 1: Project Scoping
    - laying out goals, objectives, and constraints
2. Step 2: Data Engineering
    - A vast majority of ML models today learn from data, so developing ML models starts with engineering data.
3. Step 3: ML model developement
    - With the initial set of training data, we’ll need to extract features and develop initial models leveraging these features
4. Deployment:
    - After a model is developed, it needs to be made accessible to users. 
5. Monitoring and continual learning
    - Once in production, models need to be monitored for performance decay and maintained to be adaptive to changing environments and changing requirements
6. Business Analysis
    - Model performance needs to be evaluated against business goals and analyzed to generate business insights


## Framing ML Problems

MOST business problems are not directly translatable into an ML problem. 

Hence, it is your job as an ML engineer to use your knowledge of what problems ML can solve to **frame this request as an ML problem**.


There are two things to consider when framing a problem: 
1. the type of ML task you are going to use to model your problem
2. the way you frame your objective function in problems that have multiple ML objectives.


## Types of ML Tasks

The output of your model dictates the task type of your ML problem. 

The most general types of ML tasks are classification and regression. A more general classification is outlined here:

![ML_task_classification](Assets/2-introduction-to-machine-learning-systems-design-assets/ML_task_classification.png)

- In classification, the fewer the clases there are, the simpler the problem. Binary classifiers are the simplest of all and they are widely used by ML practitioners.
- Multi-class: there are more than 2 labels to choose from but each observation can only be assigned one label.
- High cardinality: there are many labels to choose from. For example, diseases names. High cardinality problems are hard.
- Multi-label: each observation can have more than one label. For example, a newspaper article could belong to both the Science and Economy labels. Multi-label classification problems are hard.
- High cardinality multi-class that are also multi-label problems are very hard.

## Funky relationship between classification and regression

**A regression model can easily be framed as a classification model**

>:memo: **For example**, house prediction can become a classification task if we quantize the house prices into buckets such as under $100,000, $100,000–$200,000, $200,000–$500,000, and so forth and predict the bucket the house should be in.


**A Classification model can easily be framed as a regression model**

>:memo: **For example**, the email classification model can become a regression model if we make it output values between 0 and 1, and decide on a threshold to determine which values should be SPAM (for example, if the value is above 0.5, the email is spam)

![regression_vs_classification](Assets/2-introduction-to-machine-learning-systems-design-assets/regression_vs_classification.png)


## Two Approaches to multilabel classification

In general, there are two major approaches to tackle multilabel classification problems:

1. The first is to treat it as you would a multiclass classification.

2. The second approach is to turn it into a set of binary classification problems.

> :bulb: **NOTE** This usually means training multiple binary classification models!


## Importance in framing a problem properly

> :memo: **Quote** Changing the way you frame your problem might make your problem significantly harder or easier.

This will be illustrated via the following motivating example. 
Consider the task of predicting what app a phone user wants to use next.

**Naive and Bad Setup**
A bad setup would be to frame this as a multiclass classification task where:
- Input = {the user’s and environment’s features}
- Ouput = { a vector of the size N, where N = number of apps to recommending to a user}

![naive_bad_setup](Assets/2-introduction-to-machine-learning-systems-design-assets/naive_bad_setup.png)

This is a bad approach because whenever a new app is added, you might have to retrain your model from scratch, or at least retrain all the components of your model whose number of parameters depends on N.


**Better Appraoch: Via Regerssion**
A better approach is to frame this as a regression task.
- Input = {user’s, the environment’s, **and the app’s features**}
- Ouput = {a single value between 0 and 1; the higher the value, the more likely the user will open the app given the context.}

In this framing, for a given user at a given time, there are N predictions to make, one for each app, but each prediction is just a number.

![better_setup](Assets/2-introduction-to-machine-learning-systems-design-assets/better_setup.png)


## Choose Objective Functions via Decoupling Objectives**

To learn, an ML model needs an objective function to guide the learning process. (AKA loss function)

The challenge lies in when you want to: **minimize multiple objective functions**

There are two fundamental appraoches to this:
1. Train one model and modify the loss function
>:bulb: **For Example**, imagine you want to minimize objective_A_loss and objective_B_loss. Then, you would train one model with the following loss:  **loss = (alpha)(objective_A_loss)+  (beta)(objective_B_loss)**
2. Train multiple models(one for each loss function) and then modify the combined loss score
>:bulb: **For Example**, Same example as above Then, you would train two model: objective_A_model, objective_B_model. Then, you will combine the scores as such: **score = (alpha)(objective_A_model_score)+  (beta)(objective_B_model_score)**


## Mind Vs Data

Progress in the last decade shows that the success of an ML system depends largely on the data it was trained on.

Instead of focusing on improving ML algorithms, most companies focus on managing and improving their data.

Despite the success of models using massive amounts of data, many are skeptical of the emphasis on data as the way forward.

|                        | Mind Camp    | Data Camp      |
| -----------            | -----------   | ------------  |
| Latency Requirement    | “Data is profoundly dumb.” -Dr. Judea Pearl   |  “The biggest lesson that can be read from 70 years of AI research is that general methods that leverage computation are ultimately the most effective, and by a large margin.… Seeking an improvement that makes a difference in the shorter term, researchers seek to leverage their human knowledge of the domain, but the only thing that matters in the long run is the leveraging of computation.” -Professor Richard Sutton|
| Accuracy Requirement   | "huge computation and a massive amount of data with a simple learning algorithm create incredibly bad learners" -Professor Christopher Manning | "If you want to use data science, a discipline of which ML is a part of, to improve your products or processes, you need to start with building out your data, both in terms of quality and quantity. Without data, there’s no data science." - Dr Monica Rogati |


The data science hierarchy of needs emphasized by Dr Monica Rogati is shown below.

![data_science_hierarchy_of_needs](Assets/2-introduction-to-machine-learning-systems-design-assets/data_science_hierachy_of_needs.png)













