# Overview of Machine Learning Systems

## High level overview of chapter
Ok.
Quickly.
When I tell you 'machine learning system', what do you think of?
Well, most people (like me when I was reading this book) automatically connects with specific ML algorithms that can be used such as:
- Logistic regression
- Neural nets

However.

Algorithm is only a small part of ML system in production!

Just to name a few, other critical aspects of the system would also be:
1. business requirements, that gave birth to the ML project in the first place
2. interface where users and developers interact with system
3. data stack
4. logic for developing, monitoring, and updating models
5. infrasstructure that enables the delivery of said logic


## Structure of chapter 1
The first chapter of the book aims to give you an overview of what it takes to bring an ML model to production

This chapter addresses the following: 
1. address the fundamental question of when and when not to use ML
2. discuss the challenges of deploying ML systems
3. compare ML in research vs traditional software

## When to use/not use machine learning

#### What question to ask prior starting ML project?
The first thing that you need to get into your head is this: **ML IS NOT A MAGIC TOOL THAT CAN SOLVE ALL PROBLEMS**

In fact, even for problems where ML can solve, ML solutions might not be the optimal solution.

Hence, something important for you to do before starting an ML project is to ask:
> :question: **_Question_** Whether ML is necessary or cost-effective

#### What ML can do?
The following quote taken from the book summarizes it pretty well
> :memo: **_Quote_** Machine learning is an approach to (1) learn (2) complex patterns from (3) existing data and use these patterns to make (4) predictions on (5) unseen data.

Diving into more details on each one of them:

**1. Learn: the system has the capacity to learn** 
In most cases, ML systems learn from data.

Now, just to illustrate an example of what is NOT an ML system, consider a relational database. 
A relational database isn’t an ML system because it doesn’t have the capacity to learn. You can explicitly state the relationship between two columns in a relational database, but it’s unlikely to have the capacity to figure out the relationship between these two columns by itself.

**2. Complex patterns: there are patterns to learn, and they are complex** 
ML solutions are only useful when there are patterns to learn.

**A situation of when NOT to use ML because of a lack of pattern -> Rolling a dice**
- sane people don’t invest money into building an ML system to predict the next outcome of a fair die because there’s no pattern in how these outcomes are generated.

**A situation of when ML could work -> predicting stock prices based on patterns**
- There are patterns in how stocks are priced, and therefore companies have invested billions of dollars in building ML systems to learn those patterns.

Whether a pattern exists might not be obvious, or if patterns exist, your dataset or ML algorithms might not be sufficient to capture them. 
- For example, there might be a pattern in how Elon Musk’s tweets affect cryptocurrency prices. However, you wouldn’t know until you’ve rigorously trained and evaluated your ML models on his tweets. Even if all your models fail to make reasonable predictions of cryptocurrency prices, it doesn’t mean there’s no pattern.

**A situation of when non-ML would work -> predicting stock prices based on patterns**
- Consider a website like Airbnb with a lot of house listings; each listing comes with a zip code. 
    - If you want to sort listings into the states they are located in, you wouldn’t need an ML system. Since the pattern is simple—each zip code corresponds to a known state—you can just use a lookup table.


**Fundamental Difference Between Traditional Software and Machine Learning**
Perhaps, the most obvious difference between traditional software and that of machine learning is that instead of requiring hand-specified patterns to calculate outputs, ML solutions learn patterns from inputs and outputs.
This is illustrated in this figure
![traditional_software_vs_machine_learning](Assets/1-overview-of-machine-learning-systems-assets/traditional_software_vs_machine_learning.png)

**3. Existing data: data is available, or it’s possible to collect data** 

Now, there are three types of learning possible and each depends on a different type/amount of data:

1. Zero Shot learning (few-shot learning)
    - Here, it’s possible for an ML system to make good predictions for a task without having been trained on data for that task. 
    - However, this ML system was previously trained on data for other tasks, often related to the task in consideration.
2. Continual Learning
    - Here, we launch mL system without data
    - They will learn from incoming data in production
    - However, serving insufficiently trained models to users comes with certain risks, such as poor customer experience.
3. Fake-it-til-you-make-it
    - many companies follow a “fake-it-til-you make it” approach: launching a product that serves predictions made by humans, instead of ML models, with the hope of using the generated data to train ML models later.

**4. Predictions: it’s a predictive problem** 
- ML models make predictions, so they can only solve problems that require predictive answers

> :bulb: **NOTE** Whatever question you might have, you can always frame it as: “What would the answer to this question be?” regardless of whether this question is about something in the future, the present, or even the past.

Compute-intensive problems are one class of problems that have been very successfully reframed as predictive. Instead of computing the exact outcome of a process, which might be even more computationally costly and time-consuming than ML, you can frame the problem as: “What would the outcome of this process look like?” and approximate it using an ML model. The output will be an approximation of the exact output, but often, it’s good enough. You can see a lot of it in graphic renderings, such as image denoising and screen-space shading.

**5. Unseen data: unseen data shares patterns with the training data** 
- In technical terms, it means your unseen data and training data should come from similar distributions.


#### In what tasks do ML excel at?
Due to the way most ML algorithms today learn, ML solutions will especially shine if your problem has these additional following characteristics:

1. HIGHLY REPETITIVE!

2. Cost of wrong predictions is relatively low
    - ML is especially suitable when the cost of a wrong prediction is low.
    - If one prediction mistake can have catastrophic consequences, ML might still be a suitable solution if, on average, the benefits of correct predictions outweigh the cost of wrong predictions
        - Consider self-driving cars as an example

3. It’s at scale
    - “At scale” means different things for different tasks, but, in general, it means making a lot of predictions.
    - ML solutions often require nontrivial up-front investment on data, compute, infrastructure, and talent, so it’d make sense if we can use these solutions a lot.

4. The patterns are constantly changing
    - Figuring how your problem has changed so that you can update your handwritten rules accordingly can be too expensive or impossible. Because ML learns from data, you can update your ML model with new data without having to figure out how the data has changed.


#### In what tasks should I avoid ML?
Most of today’s ML algorithms shouldn’t be used under any of the following conditions:

- It’s unethical. 

- Simpler solutions do the trick. 

- It’s not cost-effective.

Now, even if ML can’t solve your problem, it might be possible to break your problem into smaller components, and use ML to solve some of them.















































