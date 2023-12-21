# Unity Notes

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

**GameObject:**  
GameObjects are containers for components and the base class for all entities (objects?) in Unity.  
For example a Light Object is just a GameObject with a Light component attached.  
Every GameObject has a Transform component.

<br>

**ScriptableObject:**  
ScriptableObjects are data containers that are saved as an Asset file in your project files.  
You define and store that data in the assets in the editor instead of in the code, which makes the game designer-friendly.  
They are used for things that are only meant to store data or execute code.  
You can not attach a ScriptableObject to a GameObject. Instead, you need to save them as Assets in your project.  
They are globally accessible and scene-independent.

<br>

**Component:**  
Components are classes.  
The base class for everything attached to GameObjects.

<br>

**Behaviour / Script:**  
Behaviour components are scripts. A script is a component that you make yourself to add functionality to your game.  
Your code will never directly create a Component, instead you write script code and attach the script to a GameObject.

<br>

**MonoBehaviour:**  
The base class from which every (many?) Unity script derives. To use MonoBehaviour you must explicitly derive from it.  
MonoBehaviours always exist as a Component of a GameObject.  
Has the functions: Start(), Update(), etc  
Has the messages: Awake, OnApplicationPause, OnCollision, etc

<br>
<br>

## Awake() vs Start():
Awake - Called when the script is loaded.  
Start - Called when the script is enabled, right before calls to Update happen.  

You should use Awake to set up references between scripts, and use Start to pass any information back and forth.

### Awake():
- Awake is the constructor of a script and is called when the script instance is being loaded.
- Awake is used to initialize any variables or game state before the game starts.
<br>
Awake is called only once during the lifetime of the script instance. A script's lifetime lasts until the Scene that contains it is unloaded.  
Each GameObject's Awake is called in a random order between objects. Because of this, you should use Awake to set up references between scripts, and use Start to pass any information back and forth.  
Awake is called even if the script is a disabled component of an active GameObject.  
Awake is called either when an active GameObject that contains the script is initialized when a Scene loads, or when a previously inactive GameObject is set to active, or after a GameObject created with Object.Instantiate is initialized.

### Start():
- Start is called on the frame when a script is enabled just before any of the Update methods are called the first time.
<br>
Like the Awake function, Start is called exactly once in the lifetime of the script. However, Awake is called when the script object is initialised, regardless of whether or not the script is enabled. Start may not be called on the same frame as Awake if the script is not enabled at initialisation time.
The Awake function is called on all objects in the Scene before any object's Start function is called. This fact is useful in cases where object A's initialisation code needs to rely on object B's already being initialised; B's initialisation should be done in Awake, while A's should be done in Start.

### Update():
Update is called every frame.

### FixedUpdate():
FixedUpdate is called every physics timestep.

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

### Finding GameObjects by name or tag:
```c#
// Find by name
player = GameObject.Find("MainHeroCharacter");

// Find first object by type
m_gameBoard = GameObject.FindObjectOfType<Board>();
m_spawner = GameObject.FindObjectOfType<Spawner>();

// Find by tag
// This method is much faster than FindObjectOfType.
m_gameBoard = GameObject.FindWithTag("Board").GetComponent<Board>();
m_spawner = GameObject.FindWithTag("Spawner").GetComponent<Spawner>();
```

<br>
<br>

### Instantiating as GameObject vs Transform:
```c#
// Instantiate as Transform:
Transform prefabTransform = Instantiate(prefab);
prefabTransform.position = new Vector3(0, 0, 0);

// Access GameObject from Transform:
prefabTransform.gameObject

// Destroy Transform
Destroy(prefabTransform.gameObject)


// Instantiate as GameObject:
GameObject prefabGameObject = Instatitate(prefab);
prefabGameObject.transform.position = new Vector3(0, 0, 0);

// Access Transform from GameObject:
prefabGameObject.transform

// Destroy GameObject
Destroy(prefabGameObject)
```

<br>
<br>

### ScriptableObject
```c#
[CreateAssetMenu(menuName=ScriptableObjects/MyScriptableObject)]
public class MyScriptableObject : ScriptableObject
{
    public string myString;
}


public class Test : MonoBehaviour
{
    [SerializeField] private MyScriptableObject myScriptableObject;

    private void Start()
    {
        Debug.Log(myScriptableObject.myString)
    }
}
```

<br>
<br>

**Fields:**  
Variables at the top of the class need to be set in the inspector. They are usually only declared at the top, not set there.  
Fields that aren't assigned when declared will automatically be assigned to null, but local variables aren't automatically set to null.

<br>

**Misc:**  
perpendicular - two lines that make a 90 degree angle  
vertex - a point where lines intersect  
vertices - a group of points where lines intersect

<br>

**Vectors:**  
A line from the origin to a transform point that has magnitude (size) and direction. The length of the line shows its magnitude and the arrow shows the direction. If you were to copy a vector and put it somewhere else, the two vectors would still be equal, just in different positions.  
https://docs.unity3d.com/Manual/UnderstandingVectorArithmetic.html  
https://docs.unity3d.com/Manual/DirectionDistanceFromOneObjectToAnother.html

<br>
<br>

---

<br>
<br>

### [System.Serializable] and [HideInInspector] Attributes:
I think public variables will always show in the editor, but they aren't serializable (can be changed in the inspector) unless you add the [Serializable] attribute. I think. Or maybe you only serialize classes, then the entire class is/becomes serializable? Also I think [HideInInspector] only hides the value it doesn't make it nonserializable and to do that you need to use the [System.NonSerializable] attribute when declaring the variable.

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

### Prefabs and Instantiating them
https://docs.unity3d.com/Manual/Prefabs.html  
https://docs.unity3d.com/ScriptReference/Object.Instantiate.html  
https://docs.unity3d.com/Manual/InstantiatingPrefabs.html
The prefab asset type allows you to store a GameObject with components and settings. The prefab acts as a template from which you can create new object instances in the scene. Any edits made to a prefab asset are immediately reflected in all instances produced from it but you can also override components and settings for each instance individually. This could be used for trees, bullet shells, swords, etc. Prefabs only exist as unused GameObjects in the asset folder, but instatiated prefabs exist as GameObjects in the scene.

```c#
// Instantiate a prefab
public GameObject prefabName;
GameObject instObjName = Instantiate(prefabName, new Vector3(x,y,z), Quaternion.identity) as GameObject;

// Quaternion.identity - means no rotation
// there is a transform parent parameter you can add in declaration but idk how
```

<br>

Instantiation examples:
```c#   
public GameObject tilePrefab;

void SetupTiles()
{
    for (int i = 0; i < width; i++)
    {
        for (int j = 0; j < height; j++)
        {
            GameObject tile = Instantiate(tilePrefab, new Vector3(i, j, 0), Quaternion.identity) as GameObject;

            tile.name = "Tile ("+i+","+j+")"; // The object in the hierarchy will have the name "Tile (i,j)"

            m_allTiles[i, j] = tile.GetComponent<Tile>(); // m_allTiles[i,j] == the current object being instantiated
            // ^ example: m_allTiles[2,6] == the Tile (2,6) GameObject aka the tile at 2,6

            tile.transform.parent = transform;
            // it's technically "= GameObject.transform" but if you do "= transform" it will use the GO this component is attached to
            // this current instantiated tile's parent becomes the GameObject's transform (the GO being the GO this board component is attached to)
            
            m_allTiles[i, j].Init(i, j, this); // m_allTiles is an object of the Tile class and calls the Init method from it
            // this = the current component, which would be the current instance of this board class.
        }
    }
}



void Awake()
{
    cells = new HexCell[height * width];

    //loops through all x values first, z stay 0 until x is done.

    for (int z = 0, i = 0; z < height; z++)
    {
        for (int x = 0; x < width; x++)
        {
            CreateCell(x, z, i++);
        }
    }
}

void CreateCell(int x, int z, int i)
{
    Vector3 position;
    position.x = x * 10f;
    position.y = 0f;
    position.z = z * 10f;
    // [0] = 0,0    [1] = 10,0    [2] = 20, 0

    HexCell cell = cells[i] = Instantiate<HexCell>(cellPrefab);
    cell.transform.SetParent(transform, false);
    cell.transform.localPosition = position;
}
```

<br>
<br>

### Coroutine:
When you call a function, it runs to completion before returning. This means that any action taking place in a function must happen within a single frame update; a function call can’t be used to contain a procedural animation or a sequence of events over time. As an example, consider a function that gradually reducing an object’s alpha (opacity) value until it becomes completely invisible. The function will execute in its entirety within a single frame update and the intermediate values will never be seen and the object will disappear instantly.

A coroutine is like a function that has the ability to pause execution and return control to Unity but then to continue where it left off on the following frame.

It is essentially a function declared with a return type of IEnumerator and with the yield return statement included somewhere in the body. The yield return line is the point at which execution will pause and be resumed the following frame.
```c#
IEnumerator FunctionName()
{
    for (condition) // put a loop in the coroutine
    {
        // code
        yield return null; // wait until the next frame
        yield return new WaitForSeconds(n); // wait until n seconds
        yield return StartCoroutine(); // starts new coroutine; used for chaining sequential events
    }
}

void Update()
{
    if(condition)
    {
        StartCoroutine(CoroutineName);
    }
}
```

<br>

Coroutine example:
```c#
void Update ()
{
    if (Input.GetKeyDown(KeyCode.RightArrow))
    {
        Move((int)transform.position.x + 1, (int)transform.position.y, 0.5f);
    }
}


public void Move(int destX, int destY, float timeToMove)
{
    if (m_isMoving == false)
    {
        StartCoroutine(MoveRoutine(new Vector3(destX, destY, 0), timeToMove));
    }
}


IEnumerator MoveRoutine(Vector3 destination, float timeToMove)
{
    Vector3 startPosition = transform.position;
    bool reachedDestination = false;
    float elapsedTime = 0f;
    m_isMoving = true;

    while(reachedDestination == false)
    {
        // execute if statement if we are close enough to destination
        if (Vector3.Distance(transform.position, destination) < 0.01f)
        {
            reachedDestination = true;
            transform.position = destination; // make sure our position is exact integers of destination and not a float.
            SetCoord((int)destination.x, (int)destination.y);
            break;
        }

        elapsedTime += Time.deltaTime;
        float t = elapsedTime / timeToMove;
        transform.position = Vector3.Lerp(startPosition, destination, t); // move the game piece

        yield return null; // wait until next frame
    }
    m_isMoving = false;
}
```

<br>
<br>

### UnityEvent:
UnityEvent - a way of sending messages from one component to another.

A UnityEvent is added to a MonoBehaviour and when it is invoked it broadcasts a signal to any listening components. There is the Broadcaster and the Listeners. Other MonoBehaviours that are Listeners run an Action once they receive the signal. Actions are set up in the inspector. Each Listener can run any Action or do what they see fit and aren't dependant on the other Listeners.

UnityEvents are useful because the Broadcaster doesn't care what the Listeners do, it just broadcasts the signal. Actions are useful because they persist if you save and reload scenes.

An Event implements the design pattern: Observer Pattern.

<br>

```
https://docs.unity3d.com/Manual/UnityEvents.html
https://unity3d.college/2016/10/05/unity-events-actions-delegates/
```

<br>
<br>

### Canvas:
The Canvas is the area that all UI elements should be inside. The Canvas is a Game Object with a Canvas component on it. All UI elements must be children of a GameObject that has a Canvas component attached. UI elements in the Canvas are drawn in the same order they appear in the Hierarchy. Children at the top are in the background, children at the bottom are in front.

<br>

Render modes:
```
https://docs.unity3d.com/Manual/UICanvas.html
https://docs.unity3d.com/Manual/class-Canvas.html
```

<br>
<br>

### Naming convention:
Member variables (fields?) at the top of the class should be prefixed with `m_` so that you know they belong to the class.
```c#
class MyClass
{
    int m_height;// Named with m_ so you know it is different than other variables

    SomeFunction(int height)
    {
    }
}
```


<!---

Check the Unity manual and then the Unity scripting api.


having lots of images/sprites on one image is a lot more performance efficient.

is displaying an entire map on one large image more efficient than having all the assets on one small image where each asset is only on the image once, separated by selected sprites?




fields should be private and are named as _ then camel case:  
string _fieldName;

--->
