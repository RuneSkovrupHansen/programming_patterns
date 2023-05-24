# programming_patterns
Repository for notes and examples of programming patterns

https://refactoring.guru/design-patterns

# Overview

Programming patterns are not algorithms but high-level blueprints of solutions for common and recurring problems.

Patterns also server as a common language between engineers, giving name to the common solutions and making them easier to refer to.

Each pattern should be tailored to the specific problem, language and environment, it is not shelf-ware.

Use with care, if all you have is a hammer, everything looks like a nail. Additionally, patterns may cover up for language deficiencies, it could be that another language entirely should be used.


There are different ways to classify and categorize patterns.

Classifying by size, it's a scale, smaller patterns, specific to a problem and language are commonly referred to as idioms, which is a "best-practice" way to do something. 

Higher-level and more general patterns can be referred to as architectural patterns. These can be implemented in any language.


Categorizing by intent there are three overall groups:

* Creational patterns
* Structural patterns
* Behavioral patterns


## Creational Patterns

### Factory Method

Creating objects in a super class.

Objects returned often referred to as products.

The objects must share a common interface. The factor must return object matching this interface.

The code using the factory is called client code.

The client code can use the products by the interface knowing that it will adhere to that interface.


It's important to notice that the products must adhere to an abstract interface, however, the factory must also adhere to a factory interface.

Interface abstraction is used in both the factory and the product which it produces.


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


## Singleton

Singleton is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.

The singleton solves the two problems of:

* Ensuring only a single object a type exist, usually used to control access to shared resource
* Provide global access to the instance. A singleton has more access control than global variables


Singleton implementation:

* Make the default constructor private, to prevent other objects from using the `new` operator with the Singleton class.
* Create a static creation method that acts as a constructor. Under the hood, this method calls the private constructor to create an object and saves it in a static field. All following calls to this method return the cached object.


Requires thread handling to avoid creating multiple singleton objects at the same time.


# Structural Patterns

## Adapter

Adapter is a structural design pattern that allows objects with incompatible interfaces to collaborate.

An adapter converts the interface of an object, so that it is compatible with the interface of another.


In the example the adapter is passed an instance of the object which must be adapted. The adapter then serves as a wrapper around the object, providing the correct interface for use.


The adapter wraps the object which must be used by another component. The adapter implements an interface which describes how the component would like to consume the interface. The adapter is then used to implement whatever is required to call the service like the interface describes.


An adapter changes the interface to an existing object where a decorator enhances an object without changing its interface.


## Bridge

Lets you split abstraction and implementation. Supposedly.

Instead of adding all implementation to a single class, the implementation can be made in another class, and a reference can be made to that class. In this way part of the complexity of the class is abstracted away.

Remember that dependency injection is a good thing.

Think about dimensions of a class. If a class is extending in multiple dimensions it is possible that one dimension should be abstracted into another class. A class should have a single focus, and complexity handling variations should be abstracted away.

Bridge pattern could also be referred to as an interface pattern.

Single Responsibility Principle.


## Composite

Can be used when a problem or topic can be structured like a tree, i.e. with leafs and composites.

An interface can be created so that each leaf and composites perform an action.

Example of boxes (with boxes ...) with components. In composite pattern each could adhere to interface of calculating cost, making it easy. The composite action on a box would be to calculate cost of all nested boxes.

Graphical program like Figma example. Interface of move and draw, composite can hold multiple objects.


The Composite pattern provides you with two basic element types that share a common interface: simple leaves and complex containers. A container can be composed of both leaves and other containers. This lets you construct a nested recursive object structure that resembles a tree.


Useful when complex objects can be made up of many small objects.


## Decorator

Wrap an object according to an interface to allow consumers to rely on the interface. Wrapping allows the logic to be modified slightly.

Used to extend the behavior of a class.

Common to use dependency injection to wrap objects. The object to be wrapped is passed to a wrapper class.


## Facade

A facade is a wrapper around a complex system to provide a limited but simplified interface for usage. This serves to hide unnecessary information and complexity.


## Flyweight

https://refactoring.guru/design-patterns/flyweight

Flyweight is a structural design pattern that lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object.


Objects *intrinsic* state, the static state that is immutable. Example of bullet size and color.

Objects *extrinsic* state, the non-static state that is mutable. Example of position and speed.


The patterns suggests that you stop storing the intrinsic state in an object since it takes up memory.

An object that only stores the intrinsic state is called a flyweight object.


Objects storing the mutable state, the extrinsic state can reference flyweight objects. Doing this, the flyweight objects only need to be stored once, rather than for each object.

The flyweight should be immutable. Do not expose setters or public fields.


Factory Flyweight:

Convenient way to handle flyweight is to have a factory which can store the flyweight objects and then produce extrinsic state mutable objects which reference the pool of flyweight objects.

This echo's the notion that a class should only members which are meant to be modified. Any constant or static fields on an object is dead memory, since all references could point to a single source instead.


The state that is passed to the flyweight object (intrinsic) is called extrinsic. It's common to have the operations of the object be part of the flyweight since they are not unique. The part of the object that is unique / mutable is then passed to the flyweight operations as part of the call.


The context class is what hold both the extrinsic and intrinsic states and performs the operations.


This approach saves RAM but is more CPU intensive, it's a tradeoff.


## Proxy

Proxy is a structural design pattern that lets you provide a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.


You can create a proxy object for a slow service, such as a database, etc. The proxy takes care of all the interaction which allows the clients to not have to implement that code, and run faster since it does not have to block to wait for the service.

Proxies can be used to implement lazy-initialization and caching.


Proxies can be stacked to provide additional functionality, examples:

* Caching
* Lazy-loading
* Protection
* Logging
* Smart reference


Similar to a decorator, just as a structural pattern. A proxy usually manages the lifecycle of an object as opposed to a decorator, which just wraps an existing object.


# Behavioral Patterns

