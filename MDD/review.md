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

Question 1
Models can be more easily analysed than full programs because...
They provide meaningful abstractions that can be directly used in the analysis.

Question 2
Select all items that are characteristics of models.
Pragmatics
Purpose
Abstraction
Reduction

Question 3
When modelling on the whiteboard, we use models as sketches.
UML class diagrams are typically used as models as blueprints.
Our Gridgame language allowed using models as programs.

Question 4
Which of the below is NOT a valid model representation?
Mental
*IS a model representation: Textual, Graphical, Tabular

Question 5
A class diagram is used as part of the domain analysis; that is, understanding the
concepts relevant to a particular problem domain. What are the pragmatics of this
model?
→Descriptive

Question 1
Development effort in a model-driven development approach is typically front‐loaded 前置性的

Question 2
When would you recommend using an MDE-based approach?
1. When contributions from domain experts are key to the successful development of a software system
Domain-specific modelling languages can often be useful to help domain experts express their domain knowledge. It is important to be careful though and consider
the effort required for developing these DSMLs in relation to the benefits obtained.
2. When developing multiple similar but different systems -- 
here a domain-specific modelling language can be used to capture the difference between systems This is probably the most typical use case for MDE.
3. For a one-off development of a complicated system
For complicated systems, introducing a model-based approach may reduce the cognitive load for developers and make it easier to build the system.

Question 3
Which technologies have been key for bringing MDE out of the trough of disillusionment 幻灭感?
1. Language workbenches
2. DSMLs


## principles of modelling
<img width="608" alt="image" src="https://user-images.githubusercontent.com/57675566/167010174-1fc4c2a7-1c9c-4cab-96e2-31a6aa2d20b8.png">
The abstract syntax captures the concepts of a modelling language and the links between these. This is often done in a so-called metamodel, which captures concepts as classes and links as associations.
The concrete syntax is based on the abstract syntax and defines what the language looks like to the user and how users interact with the model. This can take many forms, from graphical and textual to tabular or more exotic forms as appropriate for the domain and purpose.
Finally, a modelling language needs a semantics defining what each possible model means. This can be defined fairly informally, but may need to be defined more formally to enable compilation and analysis of the models.
![image](https://user-images.githubusercontent.com/57675566/167010267-d4de5f8e-edb5-4ed9-b06f-fdff14eada38.png)


Question 1
To make models useful, modelling tools enforce that each model is expressed in a well‐defined modelling language.

Question 2
Which of the below are part of the concrete syntax of a modelling language?
Specification of how the user interacts with the language
Specification of what language concepts look like

Question 3
Which of the below are part of the abstract syntax of a modelling language?
Language concepts
Links between concepts

Question 4
UML is a general‐purpose modelling language

Question 5
Models are turned into realisation artefacts using transformations that
execute transformation definitions.

Question 6
Which of the below are part of the semantics of a modelling language?
Specification of what the language concepts mean
 
# week2 building first textual language
## one reference link http://dsl-course.org/xtext-writing-a-grammar/
## week2-1 developing eclipse plugins
### week2-quiz1 reference link:https://www.vogella.com/tutorials/EclipsePlugin/article.html
1.To test an Eclipse plugin, the following steps are needed. Bring them into the right order:
   -Create a plugin project in your Eclipse workspace.
   -Write the plugin code.
   -Select Run As from the plugin project's context menu.
   -Select Eclipse Application from the context menu.
   -Test the plugin in the new Eclipse instance

2.Eclipse plugins are...
   -the core constituent components of Eclipse.(Core. Pretty much any functionality provided by Eclipse is implemented in a      plugin. Many plugins come installed with Eclipse by default.)
   -individual software components adding functionality to the Eclipse IDE.
   -developed in Java in plugin projects in a regular Eclipse workspace.(Correct. Eclipse projects contain regular Java code and a few configuration files. Other programming languages can also be used as long as they eventually produce Java code. We will use an extension of Java called Xtend.)

3.An Eclipse run configuration specifies...
   -the set of plugins to be included.(Correct. By default, all plugins installed in the original Eclipse and open in the current workspace are included.)
   -environment variables and command line parameters, controlling such things as available stack and heap space.
   -the directory where Eclipse keeps its workspace files, including configuration and preference settings.(Correct. This is called the Eclipse workspace and is also where Eclipse keeps projects created.)
   
## week2-2 a basic grammar

**textual language**--GPLs(general programming language) --Java, C++, C#, Haskell, COBOL, They can be Can be used from any text editor, but proper IDE support helps a lot

**parse(解析)**
Textual languages are processed through parsing
Parser takes text and produces an internal object structure to be analysed and further processed
Parsing involves taking a piece of text and turning it into an internal object structure that can be further analysed later on. In doing this, parsers also check the syntactic validity of a program or model.
Different kinds of parsing algorithms exist. One of the most commonly used algorithms is LR parsing. If you have never come across LR parsing, you should read up on it and its limitations.
> (解析涉及到将一段文本转化为内部对象结构，以后可以进一步分析。在此过程中，解析器还检查程序或模型的句法有效性。
存在不同种类的解析算法。最常用的算法之一是LR解析。如果你从来没有接触过LR解析，你应该阅读一下它和它的限制)

**use grammar to disctribe textual language**
> These describe the rules to which a piece of text must adhere to be a valid instance of the language.

1. Noam Chomsky introduced four types of languages
2. Textual languages are typically defined as context-free languages
3. Can be written in a variety of notations: We will use something based on Backus/Naur form  ,Embedded in the Xtext language workbench

**a basic grammar in Xtext**
```
grammar org.xtext.example.testlang.TestLang with org.eclipse.xtext.common.Terminals

generate testLang "http://www.xtext.org/example/testlang/TestLang"

Model:
	greetings+=Greeting*
;

Greeting:
	'Hallo' name=ID '!'
;
```
> - grammar: Keyword starting a language definition
> - 紧跟着grammar的是自己新建语言的名称（language name）
> - with :使用 "with "关键词，我们可以导入一个现有的基础语法。这里，我们要导入一些标识符、字符串和数字的标准定义(Import some standard definitions (comments etc)
> - generate 语句给了 Xtext 一些关于生成过程的更多信息。我们将暂时忽略这一点。
> - model: The first rule is the so-called start rule. It defines the structure of a complete model.
> - greeting: 这里是subrule。（Other rules define sub-parts of the language and can be used (directly or indirectly) from the start rule.）
> - ‘hallo’单引号中的字是expected text， 在规则的主体中，我们可以有字面文本，指定我们期望看到的一点文本，就像这里输入的那样。
> - ID：call out to seperate rules( references to other rules.)我们还可以找到对其他规则的引用。这基本上意味着。"在这里，我希望看到任何符合称为（本例中的ID）的规则的东西"。
> - name: assign result of rule call(assign the result of any rule call to a local variable)

**some typical Xtext grammar**
1. 'text'-Expect to find this exact string at this point in the model
2. RuleName-Expect to find anything that fits the description in rule RuleName at this position
3. (...) Group sub-parts of a rule; useful for indicating repetitions etc of larger parts of the rule对规则的子部分进行分组；对表示规则中较大部分的重复等非常有用
4. <...>? some part of rule is optional
5. <...>* 表示规则的某些部分可以任意频繁地出现（包括从不出现）。 
6. <...>+ 表示规则的某些部分可以任意频繁地出现（**至少一次**）。
7. <..A> | <..B> 表示期待与<...A>或<...B>匹配的东西
8. Identifier=RuleName 表示任何与RuleName匹配的东西都应该被捕获到一个叫做Identifier的变量中；如果这是在*或+子句中，则使用+=。
```
Greeting:
	greeting=TypeOfGreeting name=ID '!'
;
enum TypeOfGreeting:
	hello='Hello' | hi='Hi'
;
```

greeting 是normal rule, 带enum的是enumeration rules，只能包含a set of alternative texts(它只能包含一组备选文本，每个文本都有一个标签。例如，这对于定义一组可用于模型或程序中某一特定位置的备选关键词很有用。)

### week2-2-quiz
1. Textual languages use **parsing** to translate **text**  into **an in‑memory object structure**  for **further analysis** 
2. A textual language can be specified using a grammar, which consists of **rules** (**Rules are the top-level elements of any grammar.**)
3. Grammar rules in Xtext can contain...
   - **assignments**(上文 name=ID里的nameFor most rule calls, you will need to include an assignment to capture the result of the rule call..）
   - rule calls: Rule calls are used to define more complex languages.
   - text literals: Text literals specify the precise text we expect to see in a particular location in each model.
   - repetition and optionality markers(Markers like *, +, or ? can be used to indicate repetition and optionality.)
4. In an Xtext grammar, the start rule is...
      - **the first rule that appears in the grammar.**
      - the rule that captures the structure of the complete model. Any valid model must match the structure defined by the start rule. To define more complex structures, the start rule can call out to other rules.

5. When making changes to an Xtext grammar, what needs to be done to try out the new version of the language?
   - Regenerate the language infrastructure from the grammar.** Whenever you have made a change to the grammar, you must regenerate the language infrastructure for the changes to take effect.**
   - Start a runtime Eclipse and create / edit a text file with the correct file extension. ** Because Xtext generates plugins, you must start a runtime Eclipse before you can test out your changes.**

## week2-3 testing your language
使用Xpect测试的好处是：write our tests as if we were writing normal files in our language.（像在写自创语言的正常文件一样写测试）
1. **In the runtime Eclipse instance, create a “plugin” project- A special kind of Java project**

2. 将自创语言，自创语言.ui，Xpect.xtext.lib 放入依赖，如下图：（Add Xpect and our language project to the dependencies of the new project
![image](https://user-images.githubusercontent.com/57675566/151247978-d6570574-a5ce-4739-971b-594e9d869f0a.png)
）
![image](https://user-images.githubusercontent.com/57675566/151247925-5fb649b6-4ef9-4e5e-9c82-10108c0079e2.png)

3. 在新建的plug-in project的src文件夹下创建Junit类，（就是新建一个java class），这是为了与标准的jUnit框架挂钩，但对于你想测试的任何语言，代码都是一样的。，代码如图：![JD`NI7QM$SC%FXQ(ZHU1KGE](https://user-images.githubusercontent.com/57675566/151248387-727f505e-2ab7-45e5-b900-bdc056cf8578.png)

4. 在你放置空测试类的同一文件夹中，我们现在可以开始编写我们的实际测试。为此，我们**创建新的文件并使用双扩展名：最后的扩展名需要是.xt**，这样Xpect才能正确识别文件。在这之前的扩展名需要是你为你的语言定义的。这里是 "ggames"，而在我们的 "Turtles "例子中是 "turtles"

5. 实际测试类的第一行是 /* XPECT_SETUP XPectTests就会找到class 然后加上 END_SETUP */

6. 选中实际测试类，右击，run as -junit test

## week 2-4 adding cross-reference

交叉引用对于文本语言是必不可少的。几乎所有的语言都需要允许他们的用户给可重复使用的规范部分命名，以便它们可以从模型的其他地方被引用。在编程语言中，你会知道像变量、函数等东西，所有这些都是使用名称和交叉引用的例子。事物的名称可以通过使用神奇的变量名称 "name "来识别。通常，这与ID规则的调用相对应
在语法中，我们可以说模型的另一部分可以通过将规则名称放在角括号中来交叉引用[...] 。该规则应包含一个名为name的变量，该变量被赋予一个ID值

**scope**
scope命令表示我们即将定义一个关于作用域的期望--作用域是指在一个特定的地方可以引用的所有对象的术语。你可能以前听说过变量的作用域。在一个箭头符号后指出我们对范围的期望。我们可以说我们期望什么在作用域中，什么不在作用域中，以及表明我们是否已经指定了完整的作用域。

### week2-4-quiz
1. A language element can be named in Xtext by **using the magic variable name "name" in the rule body**
2. Cross-references are needed in textual languages to ...
   - allow the definition of reusable blocks of code (允许定义可重复的代码块)(Functions are an example.)
   - allow referencing things defined in a different part of the code （允许引用在代码的不同部分定义的东西）(Variable declarations are an example.)
3. A cross-reference can be defined in Xtext by using angular brackets [ and ] around a rule call in a rule body 

# week 3
## week 3-1


### week 3-1-quiz
1. How many layers does MOF define? 4 (MOF defines 4 layers labeled M0 to M3.)
2. Classes on a layer of the MOF architecture...
	- are objects instantiating classes at the layer above. For example, M2 meta-classes are instances of M3 meta-meta-classes. (一层上的每个模型元素都是其上一层的类的一个实例。)
	- are called meta-classes if they are defined at layer M2.(M2 中的类是元类，M3 中的类是元元类。)
	- represent concepts in the domain a level below.
> **things in the real world / in a running system exist at layer ------ M0**

> **Concepts in an actual model are defined at layer ------ M1**

> **Concepts for defining models are defined at layer ------ M2**

> **Concepts for defining modelling tools and languages are defined at layer ------ M3**

3. **What does MOF stand for? Meta-Object Facility**
4. A meta-model describes **the abstract syntax of a modelling language**

# week 5
## week 5-1


### week 5-1-quiz
1. In Xtend extension methods are...：
   - methods that can be invoked as if they were defined in the class of their first argument
   - a mechanism for adding behaviour to existing classes where the source code of the existing class cannot be edited directly.
   - methods defined in one class that behave as if they were defined in another class
2. When designing code generators, we care about...：
   -ariability. All variable code goes into the generator, all constant code goes into a platform library.
   
3.Consider the following method definitions.： Method A
![F9{AF(}JI8GPE3K4Y 1LYLL](https://user-images.githubusercontent.com/57675566/153971213-b7c0d616-25ed-461c-b77a-2cf3a5ec0c37.png)

**4. Consider the following method definitions. Method B**
![TD9}SO~)(X4N7$FT1M1A2 E](https://user-images.githubusercontent.com/57675566/153971327-778af52f-af72-473f-bbae-f8569f921259.png)
这里的声明是int 但是后面的实例是eINSTANCE.createAddition 所以产生的实例是addition

5. "Method dispatch" refers to how an object-oriented language selects the specific method to invoke in response to a method call depending on the run-time type of objects and parameters.

## week 5-2
