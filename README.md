# reimagined-design-patterns

Give a summary description of Four design patterns that you choose from the following design patterns: **Adapter,  Builder, Composite, Decorator, Observer, Interpreter, State, Mediator, Memento, Prototype, Proxy**. In your summaries say:

- what kind of problem(s) you can solve with that pattern and when you use it, maybe with a short example
- how the pattern works, what the basic idea of the pattern is
- what the main advantage and what the the main disadvantage is of using this pattern
- Write a short summary for each of the four patterns, about half a page for each pattern (rather less than more). 

> Do not add diagrams, and do not try to give a complete description of the patterns as found in the books. Rather think of how you would explain the essential ideas of these patterns in a few sentences to a colleague while drinking coffee.


## Observer Pattern
There are two things here
1. Notifier
2. Observer(s)

If there are multiple clients (Observers) looking for some data then the notifier updates all of them as soon as there is a change in the data.  
Observer need not poll to check if there is change in the data / New data.  
Observer can just sit and relax while notifier updates all the observers.  
The data needed by different observers may be in different format then we can also add hooks to observer so that whenever notifier updates the observer
it can call the hooks and convert the value in the needed format.

**Example:**
[Watch example present in this link](https://www.adamtornhill.com/Patterns%20in%20C%204,%20OBSERVER.pdf)    
*my own example:*  
Not sure how this happens in real life  
The data fetching from network to all the registered clients in Network layer in a ECU **may** contain observer pattern.  
Mulitple observers waiting for multiple messages. So as soon as the ECU recieves the message stack it updates  
all the observers with the new data.
Cons:
specific usecase Embedded systems: There might be a multiple observers for a single ADC channel then
Say if our notifier runs at every 1msec but the observer code runs at 20msec or 50msecs. then it will be a waste of CPU time to notify 
all the observers even when there is no need. polling works best resource wise.

## Adapter Pattern
When there are some entities that speak complelety different language but now need to work together to make the job done
then adapters will be a lot of helpful.
Neither of these classes or entities need to be changed just to work with one another class.
We thus prevent sub class explosion problem.[Link](https://python-patterns.guide/gang-of-four/composition-over-inheritance/#problem-the-subclass-explosion)
When something in either of the entities change then the other entity is not effected. Only adapter is affected.
Not sure of any personal examples here.

## Mediator pattern 
When working in embedded i think its pretty much easy to observe the mediator pattern.
Multiple components want to interact with hardware in their own style and leads to this problem.
They either need to talk to each other what every other is doing stay in sync and then perform the actions
which is hard to design. A software unit can change at any point of time and if one unit changes then all the
other units may change.
So a mediator among all the components helps a lot here.
Scenarios which i have seen:
Its mostly with the hardware access, there will be multiple people who will be waiting to control hardware
during their startup tests and not every one get the access. Also sometimes there can be some system reactions
which needs to be taken care of as soon as they show up or else the system might get damaged.
In this case all the components need not only know about the other components but also about systems weird scenarios
which at bring up code duplication too.
So in this case mediator pattern helps.



## Decorator Pattern
This pattern is really interesting.
With the help of decorator pattern we can exptent a particular object of a class with additional functionality.
### Example from book
The example provided in the gangs of four book is really a simple one and easy to understand.
A Text view getting extended with scroll bar and border line 
### The Examples I thought
I have personally never used this pattern.
But a simple website who sells a webpage for money may use decorator pattern. 
Say the company has multiple plans  
1. plan A - A webpage with feature A , B and C => cheap plan
2. plan B - A webpage with feature X , Y and Z => costly plan
They can have mutliple instance of a class called webpage. But they can use this decorators design  
pattern to create a webpage with just feature A or with A and B or with A and B and C.
They need not change the class for adding the features. 
At first i was confused with inheritance concept but it is far more than that.
The beautiful thing is one can apply the same decorator any number of times to class.
I know a little python, while surfing in the net i found the following link to be 
interesting . [LINK](https://python-patterns.guide/gang-of-four/decorator-pattern/)
Even the reference links are interesting too.

The example in the link says its a decorator pattern but it doesnt looks like one. Correct me if i am wrong.
[stackoverflow](https://stackoverflow.com/questions/35996960/c-decorator-design-pattern-using-the-pizza-example)
Moreover i have my reason in the comment section of the only answer





## State pattern
I am writing this pattern down as i never understood any of the examples.  
I am listing this down so i can get your help in understanding this concept.  
The name is very obvious.
I have written a few statemachines myself and i have seen a statemachine which uses a table of commands.   
The table of commands is a very different from the table present in patterns in c but does the exact same job.  
But i dont know what i am missing but i never understood the example given in the [link](https://www.adamtornhill.com/Patterns%20in%20C%202,%20STATE.pdf)  
May be its too small for a statemachine. For a small state machine like that the code is crazily complicated.  
Even the GOF example sounds incomplete to me. The state transition is done simply by assigning some variable.   
No state transition code ever shown. Its like some one already know to what state one has to go and which method has to execute.  
*Somethings which i understood:*  
One has to seperate the states behavior from transition behavior or else one will create inter dependices which is bad.
1. One can place the transition in the form of tables (never thought of it). 
But it has its own disadvantage as even though it eleminates the conditional logic
changing the table might become too difficult
1. Seggregating the states behavior from statemachine helps us to add new states easily.
1. One can localize the state transition logic so it only worries about the next possible states
1. Or One can also include the state transition in the state logic but this is bad as it brings up dependencies.

Even after knowing all these points i really did not understood the importance of the examples provided
in patterns of C or in the GOF.
i did not saw a way of eleminating conditional logic only a way to seggregate stuff. The way as of now looks complicated
as i was not able to link the examples provided in the books.
None of the examples provided the below case is (correct me if i am wrong).
What if there exists a conditional state transiiton. Say there exists a state B , which can be entered only if
State A is succesful else State C needs to get executed. Then state transition logic gets mixed up with the result/outcomes
of the states. Now one more dependency is created between the state transition logic and state logic, isnt it ?



 









