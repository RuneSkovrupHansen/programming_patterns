# programming_patterns
Repository for notes and examples of programming patterns

https://refactoring.guru/design-patterns


## Abstract Factory

Abstract Factory is a creational design pattern that lets you produce families of related objects without specifying their concrete classes.

Use of interfaces for objects to ensure compliance between different implementation of objects.

Use of interface for factories to ensure compliance between different implementation of factories. These factories will return abstract types, i.e. ones defined in the interface for objects.

An implementation of the factory will then define the specific behavior including the objects it returns.


Abstract interfaces for the factory and the objects it produce.

A concrete factory adheres to the interface of the abstract factory, and produces concrete objects which adheres to the interface of the abstract objects.


Example,

A GUI factory *gui_factory* which returns buttons of type *button*. gui_factory is an abstract factory, which returns the abstract type *button*.

The gui_factory can have several implementations for example *linux_gui_factory* or *win_gui_factory*. The factories still implement the general interface for a factory. Each factory can return an implementation of the button interface, for example *linux_button* or *win_button*.

As long as the correct factory is created the application can handle everything by interacting through the gui_factory and button interfaces.


Remember dependency injection when passing a created factory.


The pattern is like an extension of the factory method where the factory also uses an abstract interface so that multiple factories can be created.


## Factory Comparison

A *factory* can refer to many things. Common to refer to an object that creates other objects.

*Creation method*, wrapper around a constructor call. Sometimes called factory method.

The term *static factory method* goes against the factory pattern which relies on inheritance. Instead *static creation method* is more appropriate, since it is a creation method which can be called outside of the class constructor, an alternative to the constructor.

A *simple factory* can refer to a class which simply returns another type based on a single conditional.

A *factory method* pattern is a creational pattern that provides an interface for creating objects, but allows subclasses to alter the type of object that will be created.

The abstract class implements some common functionality but also has abstract functions which must be defined in subclasses.

An *abstract factory* is a creational design pattern that allows producing families of related or dependent objects without specifying their concrete classes.


## Builder

Complex objects can be difficult to construct, either requiring a large constructor or many subclasses.

An alternative is a *builder* to build the complex object.

Helps split the construction of a complex object into smaller pieces. Not all steps have to be called, and instead the object can be constructed for a specific purpose.

Object is not accessible while the builder is constructing the object.

Sometimes a *director* is used. A separate class to specify the order in which the builder is called. For example, for a HouseBuilder, a HouseDirector, could have methods to build different types of houses, createPalace() calling the builder with all required calls to build a house to that specification.

A directory makes it easy to use specific configurations of products.

The builder class can be abstracted to have different types of builders.

Remember that dependency injection is a good idea.

A pattern for creating complex objects.


## Prototype

Creational design pattern that lets you copy existing objects without making your code dependent on their classes.

Can be difficult if a class has important information stored in private members, it cannot readily be copied. Additionally, if manual copying is implemented, the logic of the class leaks into the code where the copy occurs, since it needs to know how to copy the class.

The prototype pattern delegates the cloning process to the objects that are being copied. 

Cloning interface which has a single `clone` method. Since it is the object being cloned that is implementing the functionality, all members are readily available.



