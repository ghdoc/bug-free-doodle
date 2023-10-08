- SINGLE RESPONSIBILITY PRINCIPLE  
    https://deviq.com/single-responsibility-principle/

	- The Single Responsibility Principle (SRP) states that a class should have only one reason to change.  It was first cited in this form by Robert C. Martin in an article that later formed a chapter in his Principles, Patterns, and Practices of Agile Software Development book.
	- The Single Responsibility Principle is closely related to the concepts of coupling and cohesion.  Coupling refers to how inextricably linked different aspects of an application are, while cohesion refers to how closely related the contents of a particular class or package may be.  All of the contents of a single class are tightly coupled together, since the class itself is a single unit that must either be entirely used or not at all (discounting static methods and data for the moment).  When other classes make use of a particular class, and that class changes, the depending classes must be tested to ensure they continue to function correctly with the new behavior of the class.  If a class has poor cohesion, some part of it may change that only certain depending classes utilize, while the rest of it may remain unchanged.  Nonetheless, classes that depend on the class must all be retested as a result of the change, increasing the total surface area of the application that is affected by the change.  If instead the class were broken up into several, highly cohesive classes, each would be used by fewer other elements of the system, and so a change to any one of them would have a lesser impact on the total system.
	- Martin suggests that we define each responsibility of a class as a reason for change.  If you can think of more than one motivation for changing a class, it probably has more than one responsibility.  When these axes of change occur, the class will probably need to have different aspects of its behavior changed, at different times and for different reasons.  However, like other principles, it’s unwise to try and apply SRP to everything from the outset.  If a particular class is stable and isn’t causing needless pain as a result of changes, there is little need to change it. Practice Pain Driven Development.
	- Some examples of responsibilities to consider that may need to be separated include:
	- Persistence
	- Validation
	- Notification
	- Error Handling
	- Logging
	- Class Selection / Instantiation
	- Formatting
	- Parsing
	- Mapping

- OPEN CLOSED PRINCIPLE  
    https://deviq.com/open-closed-principle/

	- The Open-Closed Principle (OCP) states that software entities (classes, modules, methods, etc.) should be open for extension, but closed for modification.
	- In practice, this means creating software entities whose behavior can be changed without the need to edit and recompile the code itself. The simplest way to demonstrate this principle is to consider a method that does one thing. Let’s say it writes to a particular file, the name of which is hard-coded into the method. If the requirements change, and the filename now needs to be different in certain situations, we must open up the method to change the filename. If, on the other hand, the filename had been passed in as a parameter, we would be able to modify the behavior of this method without changing its source, keeping it closed to modification.
	- The Open-Closed Principle can also be achieved in many other ways, including through the use of inheritance or through compositional design patterns like the Strategy pattern.
	- [Modular and Expressive Abstractions](https://blog.symprise.net/articles/open-closed-principle-concerns-about-change-in-software-design)
	
	- High-quality software designs are made of modular and expressive abstractions.
	- Modularity is a design quality at the syntactical level. A design’s abstraction is a module if its internal implementation and external context are coupled only through the specification of its responsibilities.
	- Modular designs enable abstractions to be locally implemented and globally reusable. Modularity facilitates human minds to engineer highly complex and adaptable systems.
	- Expressiveness is a design quality at the semantic level. A design’s abstraction is expressive if its specification represents a domain concept.
	- Expressive designs can easily articulate abstractions that clearly express the relevant concepts, problems and solutions. Expressiveness facilitates understanding and communication that enable human minds to engineer relevant and valid solutions.
	- Identifying, representing and separating relevant concerns is the fundamental principle for our design process.
	- Concerns bridge syntax and semantics to define abstractions and assign responsibilities that compose and decompose modular and expressive designs.

- LISKOV SUBSTITUTION PRINCIPLE  
    https://deviq.com/liskov-substitution-principle/

	- The Liskov Substitution Principle (LSP) states that subtypes must be substitutable for their base types. When this principle is violated, it tends to result in a lot of extra conditional logic scattered throughout the application, checking to see the specific type of an object. This duplicate, scattered code becomes a breeding ground for bugs as the application grows.
	- Most introductions to object-oriented development discuss inheritance, and explain that one object can inherit from another if it has an “IS-A” relationship with the inherited object. However, this is necessary, but not sufficient. It is more appropriate to say that one object can be designed to inherit from another if it always has an “IS-SUBSTITUTABLE-FOR” relationship with the inherited object. A common way to demonstrate this is with a set of geometric classes. Consider a class Rectangle, with properties for Length and Height. Now to model a Square, we will inherit from Rectangle, because of course a Square “IS-A” special case of a Rectangle. When we implement Square, we can simply enforce its “squareness” by forcing both Length and Height to be set whenever one of these properties is set. This ensures our Square will never have Length != Height. However, this violates an invariant of the base class, Rectangle. In this case, the invariant was never explicitly stated, but there is an expectation among clients of class Rectangle that its Height and Width can be set independently of one another, and that doing so will not have any side effects. Imagine now a bit of code that takes in a Rectangle, sets Height and Width to different values (let’s say 3 and 4), and then returns the area of the Rectangle by multiplying its Height by its Width. If one passes in an actual base Rectangle type, the result of this operation will be that the rectangle will have a Height of 3 and a Width of 4 and an area value of 12 will be returned. However, if a Square is passed in, instead, the result of the operation will be a Square with a Height of 4 and a Width of 4 and an area of 16, which is probably not what was expected.
	- A very common violation of this principle is the partial implementation of interfaces or base class functionality, leaving unimplemented methods or properties to throw an exception (e.g. NotImplementedException). In code that you know is only going to be used by one client that you control, this is fine, but if such classes are going to be in a shared codebase, or worse, framework code that is shipped to third parties, such implementations should be avoided. If a given interface has more features than you require, follow the Interface Segregation Principle and create a new interface that includes only the functionality your client code requires, and which you can implement fully.
	- A common code smell that frequently indicates an LSP violation is the presence of type checking code within a code block that should be polymorphic. For instance, if you have a foreach loop over a collection of objects of type Foo, and within this loop there is a check to see if Foo is in fact Bar (subtype of Foo), then this is almost certainly an LSP violation. If instead you ensure Bar is in all ways substitutable for Foo, there should be no need to include such a check.