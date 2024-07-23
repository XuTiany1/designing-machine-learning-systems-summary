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

<img src="Assets/1-overview-of-machine-learning-systems-assets/traditional_software_vs_machine_learning.png" width="200" height="100">

![traditional_software_vs_machine_learning](Assets/1-overview-of-machine-learning-systems-assets/traditional_software_vs_machine_learning.png)






































































