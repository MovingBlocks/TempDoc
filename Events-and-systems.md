# Events and systems
## Summary
Events are sent to exactly 1 entity. Systems can define methods, that get called when specific events get sent to entities with certain components.

## Processing events with events with systems.
To make a class a system you annotate it with the @RegisterSystem annotation. If a system implements certain engine interfaces like UpdateSubscriberSystem, then the methods of that itnerface will automatically be called by the engine. In addition to that, systems can declare methods that get called when certain events occured at certain entities. 

Event processing methods must have the following method signature:
* They must have a @ReceivEvent annotation
* They must be public
* The type of the first argument must implement Event
* The second argument must be of type EntityRef
* The rest of the arguments if there are some must implement Component

The signature determines when the method will be called
* The first argument controlls, for which type of event the method will be called.
* The @ReceiveEvent has an optional attribute called components which takes a array of component classes. The method will only be called, if the entity has all those components.
* If there are optional component arguments, then the method will only be called if the event receiving entity has all of those components (like with the components attribute of @ReceiveEvent).
* The @ReceiveEvent annotation has also a priorty attribute. It specifies the order in which this event will be procssed by systems that have registered for the same event.
* The @ReceiveEvent annotation has also a netFilter attribute, if the event should be processed simply spoken only on the server, only on the client or on both. see javadoc RegisterMode for how it actually works..

All parameters will be filled when the event occurs:
* The first argument will be filled with the event that occurred.
* The second argument will be filled with the entity at which the event occured.
* The remaining arguments will be filled with the components of the entity, at which the event occurred. As the existence of the components is a requirement for the method to be called, all arguments will be filled out.

Example:
```java
@ReceiveEvent(components = {MyComponent.class, LocationComponent.class})
public void onMyComponentAdded(OnAddedComponent event, EntityRef entity, MyComponent myComponent) {
```
The example method gets called, when the OnAddedComponent event occurs at an entity, which has all of the following components: MyComponent, LocationComponent. The listing of MyCompoent both in @ReceiveEvent and in the component arguments is redundant, but increased readablity in the upper case.

Note: Some events like the OnAddedComponent event are implicitly linked to a component and will be only offered for handlings to methods that require those arguments. In the upper case the event fires only when LocationComponent got added while MyComponent was present or when MyComponent got added while LocationComponent was present. When another component gets added, while MyComponent and LocationComponent is present, the method won't be called.

The following core events are linked to to a component and require handling methods to require them:
* OnAddedComponent 
* OnActivatedComponent
* OnChangedComponent
* BeforeDeactivateComponent
* BeforeRemoveComponent

All other core events and probably all module events aren't linked to a component. Please read the javadoc of any event you make a system for.

## Event sending
The recommended way of sending events is via the send method of entities (see EntityRef#send)
```java
entity.send(new MyEvent(myArg1, myArg2));
```
## Event definition
An event is a class that implements the interface Event.

It's fields should be private and should be made accessible via public getters. The event should have no setters but a constructor that takes the values for all fields and sets them.

For events that are inntend for network transfer, a protected default constructor should be provided.

See also the next chapter for annotations that are necessary for having an event be transferred over the network.

## Network and components
To be written: Should explain @ServerEvent, @BroadcastEvent and @OwnerEvent and the meaning of the RegisterMode constants. Also the concept of having a request + event should be explained.