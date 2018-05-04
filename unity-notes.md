# Unity Notes

**GameObject:**  
GameObjects are containers for components and the base class for all entities in Unity.  
For example a Light Object is just a GameObject with a Light component attached.

<br>

**ScriptableObject:**  
A class you can derive from if you want to create something that doesn't need to be attached to a GameObject.  
They are used for things that are only meant to store data or execute code. Examples: Examine, Use, Inventory

<br>

**Component:**  
The base class for everything attached to Game/ScriptableObjects.

<br>

**Behaviour / Script:**  
Behaviour components are scripts. A script is a component that you make yourself to add functionality to your game.  
Your code will never directly create a Component, instead you write script code and attach the script to a GameObject.

<br>

**MonoBehaviour:**  
The base class from which every Unity script derives. To use MonoBehaviour you must explicitly derive from it.  
Has the functions: Start(), Update(), etc  
Has the messages: Awake, OnApplicationPause, OnCollision, etc

<br>

**Inheritance hierarchy:**
```
- Object
    - GameObject
    - ScriptableObject
    - Component
        - Behaviour (Script)
            - MonoBehaviour
```

<br>
<br>

---

<br>
<br>

### Prefab
The prefab asset type allows you to store a GameObject with components and settings. The prefab acts as a template from which you can create new object instances in the scene. Any edits made to a prefab asset are immediately reflected in all instances produced from it but you can also override components and settings for each instance individually. This could be used for trees, bullet shells, swords, etc.

<br>
<br>

### [System.Serializable] and [HideInInspector] Attributes:
I think public variables will always show in the editor, but they aren't serializable (can be changed in the inspector) unless you add the [Serializable] attribute. I think. Or maybe you only serialize classes, then the entire class is becomes serializable? Also I think [HideInInspector] only hides the value it doesn't make it nonserializable and to do that you need to use the [System.NonSerializable] attribute when declaring the variable.

The Serializable attribute lets you embed a class with sub properties in the inspector. You can use this to display variables in the inspector. To do this the class must derive from System.Object.

Be aware that when adjusting values of public variables in the Inspector, at stop time any values changed will overwrite the defaults specified in the script. This mechanism is called serialization and is very useful for letting developers set values from the Inspector. If you want to have a public variable but want it hidden from serialization, you should specify it in front of the declaration.
```c#
[System.Serializable] class MyTestClass : System.Object
{
    [HideInInspector] public int p = 5;
    public Color c = Color.white;
}
```

<br>
<br>

### GetComponent function:
Used to access other components.
```c#
// Get a component from another GameObject
public GameObject gameObjectName; // shows in inspector, drag an object to the variable
datatype variableName = gameObjectName.GetComponent<type>();

// Get a component from the GameObject this script is attached to
datatype variableName = GetComponent<type>();
```

<br>
<br>

### Awake():
Awake is the constructor of a script and is called when the script instance is being loaded. Awake is used to initialize any variables or game state before the game starts. Awake is called only once during the lifetime of the script instance. Each GameObject's Awake is called in a random order between objects. Because of this, you should use Awake to set up references between scripts, and use Start to pass any information back and forth. Awake can not act as a coroutine.

### Start():
Start is called on the frame when a script is enabled just before any of the Update methods are called the first time. Like the Awake function, Start is called exactly once in the lifetime of the script. However, Awake is called when the script object is initialised, regardless of whether or not the script is enabled. Start may not be called on the same frame as Awake if the script is not enabled at initialisation time. The Awake function is called on all objects in the Scene before any object's Start function is called. This fact is useful in cases where object A's initialisation code needs to rely on object B's already being initialised; B's initialisation should be done in Awake, while A's should be done in Start.

<br>
<br>

### Coroutine:
When you call a function, it runs to completion before returning. This means that any action taking place in a function must happen within a single frame update; a function call can’t be used to contain a procedural animation or a sequence of events over time. As an example, consider a function that gradually reducing an object’s alpha (opacity) value until it becomes completely invisible. The function will execute in its entirety within a single frame update and the intermediate values will never be seen and the object will disappear instantly.

A coroutine is like a function that has the ability to pause execution and return control to Unity but then to continue where it left off on the following frame.

It is essentially a function declared with a return type of IEnumerator and with the yield return statement included somewhere in the body. The yield return line is the point at which execution will pause and be resumed the following frame.
```c#
IEnumerator FunctionName()
{
    for (condition) // put a loop here
    {
        // code
        yield return null;
    }
}

void Update()
{
    if(condition)
    {
        StartCoroutine("FunctionName");
    }
}
```




<!---

Check the Unity manual and then the Unity scripting api.



https://www.youtube.com/watch?v=tGmnZdY5Y-E
https://www.youtube.com/watch?time_continue=226&v=AXUvnk7Jws4
https://github.com/stella3d/job-system-cookbook
https://github.com/Unity-Technologies/EntityComponentSystemSamples




having lots of images/sprites on one image is a lot more performance efficient.

is displaying an entire map on one large image more efficient than having all the assets on one small image where each asset is only on the image once, separated by selected sprites?



public and private vars:
declared outside class in just the script

local var:
declared inside a function



fields should be private and are named as _ then camel case:  
string _fieldName;

--->
