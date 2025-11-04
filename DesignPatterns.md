Standard Design Patterns include: 
Architectural Patterns

Creational Patterns:
    Abstract Factory, Builder, Factory Method, Prototype, Singleton.

Structural Patterns:
    Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy. 

Behavioural Patterns:
    Chain Of Responsibility, Command, Interpreter, Iterator, Mediator,
    Memento, Observer, State, Strategy, Template Method, Visitor.
	
=======================================================================================
Architectural Patterns
https://www.ou.nl/documents/40554/791670/IM0203_03.pdf

1. Layered pattern:
	- Presentation layer(aka UI layer)
	- Application layer (aka service layer)
	- Business logic layer (aka domain layer)
	- Data access layer (aka persistence layer)
2. Client-server pattern
3, Master-slave pattern
4. Pipe-filter pattern
5. Broker pattern
6. Peer-to-peer pattern
7. Event-bus pattern
8. Model-view-controller pattern
9. Data access object pattern
10. Interpreter pattern
=======================================================================================
Singleton:
 - single instance enforcement
 - lazy initialization
 - global access
Now Singleton is an antipattern - it makes applications more brittle and harder to test.
=======================================================================================
it starts out using Factory Method and it evolves toward 
 Abstract Factory,
 Prototype, or
 Builder
=======================================================================================
Factory Method pattern:
	- the factory method is a method
	- it uses inheritance and relies on a subclass to handle the desired object instantiation

Abstract Factory pattern:
	- the abstract factory is an object
	- a class delegates the responsibility of object instantiation to another object via composition
	- one interface for creating a family of products
=======================================================================================
~~~ Builder <-> Abstract Factory ~~~
Builder focuses on constructing a complex object step by step.
                 It parses a complex representation, creates one of several targets.
Abstract Factory emphasizes a family of product objects (either simple or complex).

Builder          returns the product as a final step
Abstract Factory returns the product immediately
=======================================================================================
~~~ Adapter <-> Bridge ~~~
Adapter makes things work after  they're designed.
Bridge  makes things work before they're designed.

Adapter: impedance-match a legacy component to a new system
Bridge: decouple interface from implementation; move beyond encapsulation to insulation

Adapter examples in Java:
   java.util.Arrays#asList() (adapts array to List interface)
   java.util.Collections#list(Enumeration) and Collections#enumeration(Collection)
   java.io.InputStreamReader (adapts InputStream to Reader)
   java.io.OutputStreamWriter (adapts OutputStream to Writer)
   java.nio.channels.Channels#newInputStream(ReadableByteChannel) (adapts channel to stream)
   javax.xml.bind.annotation.adapters.XmlAdapter (for XML marshaling/unmarshaling)

Bridge examples in Java:
   java.nio.Buffer (Abstraction) and its views (ByteBuffer, CharBuffer, etc.)
   Logger abstraction and Handler implementations in java.util.logging
   java.sql.Driver (Abstraction) and its implementations (Bridge between JDBC API and database drivers)
   javax.swing.JComboBox (Abstraction) and its ComboBoxModel (Implementation)
   javax.swing.plaf.ComponentUI and Swing components (look-and-feel decoupling)
   java.awt.Graphics (Abstraction) and underlying OS-specific drawing (Implementation)
=======================================================================================
~~~ Adapter <-> Proxy <-> Decorator <-> Facade ~~~
  Adapter provides a different interface to its subject.
    Proxy provides    the same interface.
Decorator provides an enhanced interface.
Facade    provides   a simpler interface.
=======================================================================================
Recursive composition patterns: Composite, Decorator, and Chain of Responsibility.

Composite: recursive composition by coupling the aggregate class to a common abstraction
Decorator: recursive wrappering that supports client-specified incremental embellishment

Composite examples in Java:
   java.util.List (when used to build tree structures, e.g., List<List<...>>)
   javax.swing.JComponent
   java.awt.Container
   org.w3c.dom.Node

Decorator examples in Java:
   java.util.logging.Logger (Logger can be decorated with Handlers and Filters to add additional behavior)   
   java.util.Collections#checkedList, synchronizedList, unmodifiableList (decorates lists with additional behavior)
   java.io.InputStream, java.io.OutputStream, java.io.Reader, java.io.Writer
      (e.g., BufferedInputStream, FilterInputStream, DataInputStream chain decorators over InputStream)
   java.nio.channels.Channels.newInputStream/newOutputStream (wraps and decorates channels as streams)
   jakarta.servlet.http.HttpServletRequestWrapper, HttpServletResponseWrapper (servlet API wrappers decorate requests/responses)
   java.awt.Component (the java.awt.ScrollPane decorates a component to add scrolling)

Chain of Responsibility examples in Java:
   java.util.logging.Handler (logging events passed through a chain of handlers)
   jakarta.servlet.Filter and jakarta.servlet.FilterChain ( FilterChain::doFilter(servletRequest, servletResponse)' )
   java.nio.file.FileVisitor (the visitFile and related methods are called in a chain for file tree traversal)
   java.util.stream.Stream processing pipelines (each intermediate operation forms a chain)
   java.lang.invoke.MethodHandle combinators (method handles can be chained for dynamic invocation)
   java.util.concurrent.Flow.Processor (in reactive streams, processors form a chain between publishers and subscribers)
=======================================================================================
~~~ Command <-> Memento ~~~
They act as magic tokens to be passed around and invoked at a later time.
In Command the token represents a request.
In Memento the token represents the internal state of an object at a particular time.

Memento - restore an object back to its previous state (e.g. "undo" or "rollback" operations)

Command examples in Java:
   Runnable, Callable, Executor, ExecutorService
   Lambda expressions implementing commands (Runnable/Callable)
   java.awt.event.ActionListener
   javax.swing.AbstractAction
   SwingUtilities.invokeLater

Memento examples in Java:
   java.io.Serializable (object state snapshot/restore)
   java.nio.ByteBuffer.mark/reset
   java.util.Stack (for saving/restoring states)
   java.util.prefs.Preferences API backup/restore
   javax.swing.UndoManager, UndoableEdit
=======================================================================================
~~~ Template Method <-> Strategy ~~~
Template Method uses inheritance to vary part of an algorithm.
Strategy        uses delegation  to vary the entire algorithm.

Template Method examples in Java:
   AbstractList, AbstractSet, AbstractCollection,
   InputStream, OutputStream, Reader, Writer
   
Strategy examples in Java:
   Comparator
   Function, Predicate, Consumer, Supplier
   Executor, ExecutorService
   NumberFormat, DateFormat
   
Collections.sort and Arrays.sort accept a Comparator as a parameter to define the sorting strategy:
	Arrays.sort(T[] a, Comparator<? super T> c)
	Collections.sort(List<T> list, Comparator<? super T> c)
=======================================================================================
~~~ Factory Method <-> Prototype ~~~
Factory Method: dynamic (decoupled) creation through inheritance
     Prototype: dynamic (decoupled) creation through delegation	 
	 
Prototype examples in Java:
   Object#clone()
   Cloneable
   Date (via clone())
   ArrayList (via clone())
=======================================================================================
~~~ Factory Method <-> Template Method ~~~
Template Method
 - BEHAVIORAL pattern
 - defines the steps of an algorithm
 - leaves the task of implementing them to subclasses
 
Factory Method
 - CREATIONAL pattern
 - A superclass defines an interface to create an object
 - subclasses decide which concrete class to instantiate
=======================================================================================
~~~ Strategy <-> State ~~~
Strategy is a bind-once pattern, whereas State is more dynamic.

State examples in Java:
   java.util.Iterator (internal state machine: hasNext/next)
   java.util.Scanner (internal parsing states)
   javax.swing.JToggleButton (state transitions)
   javax.swing.text.JTextComponent (caret and selection states)
=======================================================================================
Visitor implements "double dispatch".
Element.accept()             --> ElementOne.accept()
Visitor.visit(ElementOne eo) --> VisitorOne.visit(ElementOne eo)

Visitor examples in Java:
   java.nio.file.FileVisitor
   javax.lang.model.element.ElementVisitor
   javax.lang.model.type.TypeVisitor
   javax.lang.model.util.ElementScanner
   javax.lang.model.util.SimpleElementVisitor
   javax.lang.model.util.SimpleTypeVisitor
=======================================================================================
Observer: java.beans.PropertyChangeSupport or the Flow API.
Deprecated are java.util.Observable and java.util.Observer and will be removed in a future release.
=======================================================================================
Flyweight: use sharing to optimize the use of lots of "little" objects
=======================================================================================
Design Patterns used in the Spring Framework:
    Singleton: Singleton-scoped beans
    Factory: Bean Factory classes
    Prototype: Prototype-scoped beans
    Adapter: Spring Web and Spring MVC
    Proxy: Spring Aspect Oriented Programming support
    Template Method: JdbcTemplate, HibernateTemplate, etc.
    Front Controller: Spring MVC DispatcherServlet
    Data Access Object: Spring DAO support
    Model View Controller: Spring MVC
=======================================================================================
Inversion of Control can be achieved through various mechanisms such as:
 - Strategy design pattern
 - Service Locator pattern
 - Factory pattern
 - Dependency Injection
=======================================================================================
D:\DOC\Architecture\Design Patterns\Design Class Diagrams.htm
https://refactoring.guru/design-patterns/catalog
https://www.baeldung.com/tag/pattern
http://www.vincehuston.org/dp/
https://www.journaldev.com/1827/java-design-patterns-example-tutorial
=======================================================================================
Command Query Responsibility Segregation (CQRS https://martinfowler.com/bliki/CQRS.html)
Query Model reads from database
Command Model updates database

A common example of an application that uses Event Sourcing is a version control system.
=======================================================================================
A pattern language for MICROSERVICES:
https://microservices.io/patterns/index.html
=======================================================================================
https://en.wikipedia.org/wiki/SOLID
http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod
~~~ S.O.L.I.D. design principles ~~~
1. The Single Responsibility Principle
	A class should have one, and only one, reason to change.
2. The Open Closed Principle
	You should be able to extend a classes behavior, without modifying it.
3. The Liskov Substitution Principle
	Derived classes must be substitutable for their base classes.
4. The Interface Segregation Principle
	Make fine grained interfaces that are client specific.
5. The Dependency Inversion Principle
	Depend on abstractions, not on concretions.
 
~~~ Package cohesion principles ~~~
1. The Release Reuse Equivalency Principle
	The granule of reuse is the granule of release.
2. The Common Closure Principle
	Classes that change together are packaged together.
3. The Common Reuse Principle
	Classes that are used together are packaged together.
	
Component Cohesion https://devlead.io/DevTips/PrinciplesOfComponentCohesion	
 
~~~ Couplings between packages principles ~~~
1. The Acyclic Dependencies Principle
	The dependency graph of packages must have no cycles.
2. The Stable Dependencies Principle
	Depend in the direction of stability.
3. The Stable Abstractions Principle
	Abstractness increases with stability.
	
Component Coupling https://devlead.io/DevTips/PrinciplesOfComponentCoupling
	
---------------------------------------------------------------------------------------------
Dependency Inversion Principle:
1. High level modules should not depend upon low level modules. Both should depend upon abstractions. 
2. Abstractions should not depend upon details. Details should depend upon abstractions
=======================================================================================
Best: HIGH cohesion and LOW coupling

Types of cohesion:
 - Coincidental cohesion (low) 
 - Logical cohesion
 - Temporal cohesion
 - Procedural cohesion
 - Communicational/informational cohesion
 - Sequential cohesion
 - Functional cohesion (high)

https://en.wikipedia.org/wiki/Coupling_(computer_programming)
Types of coupling:
 - Content coupling (high)
 - Common coupling
 - External coupling
 - Control coupling
 - Stamp coupling
 - Data coupling
 - Message coupling (low)
=======================================================================================
* knowledge about cloud *
The common patterns in distributed systems:
 - configuration management
 - service discovery
 - circuit breakers
 - intelligent routing
 - micro-proxy
 - control bus
 - one-time tokens
 - global locks
 - leadership election
 - distributed sessions
 - cluster state
=======================================================================================

