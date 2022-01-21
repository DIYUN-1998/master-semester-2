# week1
## 1.1 modelling and model
Modelling means using models to develop software

model characteristics：
1. abstraction : Models never represent every detail of the real world, **model focus on particular properties.**
2. reduction : Models never represent the completeness of reality. (模型不代表现实世界的完整性)Instead, **focus on one part of the real world** . the one that is most important for us at the moment. **reduction is different from abstraction: Abstraction reduces the amount of detail, reduction reduces the amount of world we model**
3. purpose : A model is created for a particular purpose. We are**trying to design a specific system to satisfy particular requirements** or **we may want to learn about a particular property of a real-world system.** (模型的目的：设计特定的系统满足要求或者为了了解已经存在的属性)The purpose of the model determines all other characteristics: what part of the world to look at, what details to abstract away from, how to represent the model, etc.
4. Representation. **Models aren’t models until they are written down in some way. You can have a mental model of something, but that’s not the kind of model we are interested in: mental models are different for everybody and, in fact, change continuously.（要确定的模型，不要心理模型这种不断变化的）** We need a more robust representation of our models so that they can be shared and understood by multiple stakeholders in a software development project. We will use modelling languages to define the way in which models can be represented.
5. Pragmatics. Models can be used and interpreted in different ways – this is called the models pragmatics. For example, **models can be descriptive like a scientific model that describes some observable reality. Models can also be prescriptive as in the case of a design model specifying what the final system should look like. Models can describe a vision of what reality should be like and they can be predictive** – for example a model predicting the weather for the next days.
Sum up：A model is an **abstraction** of a part of the real world **for a purpose**. Models are **represented in a modelling language.** Models can have different **pragmatics**: they can be descriptive or prescriptive, or describe a vision of what reality should be like (to-be).
## 1.2 types of models
1. sketches (草图，比如手绘那种)：
   - Rough, incomplete models
   - Often on paper or whiteboard
   - Good for better communication
   - maybe on whiteboard.The main purpose of these models is to be used for communication between software engineers (or sometimes between software engineers and other stakeholders). They are not meant to be complete, or even fully correct, but to convey some key point at a high level of abstraction.
2. blueprints(随着开发的深入): 
   - Detailed models
   - Often, but not always, produced digitally
   - Handed to programmers to be manually implemented
   - Models can be analysed more easily than full programs
   - these are prescriptive models showing what the software implementation should look like. Most of you will have created UML class diagrams and state-machine diagrams to specify some system behaviour before implementing it. These models can be handed to programmers to implement the software system described and to check that they have implemented it correctly.Where the models have been captured digitally, it may even be possible to automatically analyse them.Note that because of the abstraction they bring, models can be analysed more easily than full programs.
3. programs
   - Detailed, electronic models
   - Formalised semantics – models can be executed by computer
     - Interpretation or compilation (e.g., generation of Java code)
  -More efficient programming; developers work at higher abstraction level
   - Depends on abstraction gap: 
     - Low for UML: need to give almost as much detail as in a program
     - High for more domain-specific modelling languages (e.g., our grid-games language): need to give only absolute minimum of information
   - Finally, if we add enough detail in the model, we can use models as programs; that is, we can execute them directly.the specification, together with the compiler I have implemented, provides enough detail to produce a fully working Java program, that can be directly executed. In the IDE, this works as if you were executing the model directly.Even GPL programs are models as per our definition. However, their abstraction level is very low, requiring you to fill in many details. On the other hand, **a well-designed modelling language can be sufficiently detailed to be executable, while still being compact and abstract.**

## 1.3 MDE hype cycle
### A hype cycle describes the visibility and adoption of a technology over time.
![{XQT1A5EXURGY7({BG3_UJ9](https://user-images.githubusercontent.com/57675566/150521621-9a8d2a2b-f553-4916-a203-118168be9509.png)
1. (上半个图)：new technology trigger->more people try out the new technology, expectations eventually peak and people start to realise that the technology has drawbacks as well as benefits.-->the technology enters the trough of disillusionment-->many technologies make it onto the slope of enlightenment, where a more balanced understanding of the benefits and drawbacks is achieved, leading eventually to a sustainable plateau of productive usage. 
2. (下半个图)： 
3. MDE started with the introduction of the Unified Modelling Language in the mid 1990s. New standards were defined atop this, reaching the peak of inflated expectations with the model-driven architecture and its promise of automated software development. Many of these promises never came to pass with UML, as the language’s abstraction level was too low. But with the introduction of domain-specific modelling languages and language workbenches, we are beginning to climb the slope of enlightenment.

 
