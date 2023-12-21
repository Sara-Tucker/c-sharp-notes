# Events

Publisher has an event.  
Subscribers subscribe to that event.


Events enable a class or object to notify other classes or objects when something of interest occurs.  
The class that sends (or raises) the event is called the publisher and the classes that receive (or handle) the event are called subscribers.

**Publisher:**  
- the publisher determines when an event is raised

**Subscribers:**  
- the subscribers determine what action is taken in response to the event.
- An event can have multiple subscribers. A subscriber can handle multiple events from multiple publisher.


**Publisher:**  
A publisher is an object that contains the definition of the event and the delegate. The event-delegate association is also defined in this object. A publisher class object invokes the event and it is notified to other objects.

**Subscriber:**  
A subscriber is an object that accepts the event and provides an event handler. The delegate in the publisher class invokes the method (event handler) of the subscriber class.


<br>

Put the Publisher class and Subscriber class on the same GameObject.
```c#
public class EventPublisherClass : MonoBehaviour
{
    public event EventHandler OnSpacePressed;// The event

    private void Update()
    {
        if (input.GetKeyDown(KeyCode.Space))
        {
            // Invokes/Raises the event
            OnSpacePressed?.Invoke(this, EventArgs.Empty);
        }
    }
}


public class EventSubscriberClass : MonoBehaviour
{
    private void Start()
    {
        EventPublisherClass eventPublisherClass = GetComponent<EventPublisherClass>;
        // Subscribe to the event
        eventPublisherClass.OnSpacePressed += Function_OnSpacePressed;
    }

    private void Function_OnSpacePressed(object sender, EventArgs e)
    {
        Debug.Log("Pressed space.");
    }
}
```

<br>
<br>
<br>

Single class example:
```c#
public class EventClass : MonoBehaviour
{
    public event EventHandler OnSpacePressed;// The event

    private void Function_OnSpacePressed(object sender, EventArgs e)
    {
        Debug.Log("Pressed space.");
    }

    private void Start()
    {
        // Subscribe to the event
        OnSpacePressed += Function_OnSpacePressed;
    }

    private void Update()
    {
        if (input.GetKeyDown(KeyCode.Space))
        {
            // Invokes/Raises the event
            OnSpacePressed?.Invoke(this, EventArgs.Empty);
        }
    }
}
```