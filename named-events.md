# Named events

## Event signatures

###	1) Events with a specialized event argument

The events should be defined with two parameters:

```
sender AS Progress.Lang.Object,
e AS DeveloperFellAsleepEventArgs
```

The sender should be included in any case. For future dynamic event publishing and subscription it’s probably helpful to have a consistent event signature.

Event arguments should inherit from either Consultingwerk.EventArgs or Consultingwerk.CancelableEventArgs

###	2) Events from .NET inherited controls

If possible a matching .NET delegate should be used for defining the event. This allows the event subscriptions to be made from the Visual Designer. If there is no matching .NET delegate, either option 1 or 3 should be implemented

###	3) All other events (ABL events with no argument)

The events should be defined with two parameters as well:

```
sender AS Progress.Lang.Object,
e AS Consultingwerk.EventArgs or Consultingwerk.CancelEventArgs
```

The sender should be included in any case. For future dynamic event publishing and subscription it’s probably helpful to have a consistent event signature.

## Event methods

Named events in classes follow the usual .NET convention: Events will be raised only from within a method called On<EventName>.

```
METHOD PROTECTED VOID OnDeveloperFellAsleep (e AS DeveloperFellAsleepEventArgs):
```

Within the event method it’s either verified (assertion) that the event argument is passed in as a valid argument to the On<EventName> method or the event argument is initialized with a valid default (like Consultingwerk.EventArgs:Empty).

The only other functionality of the Event method (On<EventName> method) is to publish the event and verify, that the event can be published (depending on the state of the object).

```
THIS-OBJECT:<EventName>PUBLISH (THIS-OBJECT,e) .
```

The event method is typically PROTECTED. This allows two things:

1)	The On... method can be overridden and seen as the event handler for child classes. The advantage is that the child classes can determine if their code is executed before or after all other event subscribers. In principle the child classes can also avoid the event from being published this way – if the omit executing the SUPER method from the child method. 

2)	This allows child classes to also raise the event by invoking the PROTECTED On... method.
In exceptions the Event method may be declared as PRIVATE. But this should be explained in a comment.
 

 
