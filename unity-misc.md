# Unity Misc:

## Setting object properties:
Set object position:
```c#
public class MyObject : MonoBehaviour
{
    private void RandomizePosition()
    {
        Bounds bounds = this.gridArea.bounds;

        float x = Random.Range(bounds.min.x, bounds.max.x);
        float y = Random.Range(bounds.min.y, bounds.max.y);

        this.transform.position = new Vector3(Mathf.Round(x), Mathf.Round(y));
    }
}
```

<br>

Set object rotation:
```c#
public class MyObject : MonoBehaviour
{
    private void Start()
    {
        // Random rotation on Z-axis
        this.transform.eulerAngles = new Vector3(0.0f, 0.0f, Random.value * 360.0f);
    }
}
```

<br>

Set object scale:
```c#
public class MyObject : MonoBehaviour
{
    public float size = 1.0f;
    public float minSize = 0.5f;
    public float maxSize = 1.5f;

    private void Start()
    {
        // Random scale
        this.transform.localScale = Vector3.one * size;
    }
}
```

<br>

Set random sprite:
```c#
public class MyObject : MonoBehaviour
{
    public Sprite[] sprites;
    private SpriteRenderer m_spriteRenderer;

    private void Awake()
    {
        m_spriteRenderer = GetComponent<SpriteRenderer>();
    }

    private void Start()
    {
        m_spriteRenderer.sprite = sprites[Random.Range(0, sprites.Length)];
    }
}
```

<br>
<br>

## Instantiate:
Constantly spawn object:
```c#
public class Manager : MonoBehaviour
{
    public MyObject myObjectPrefab;
    public float spawnStartTime = 0.0f;
    public float spawnRate = 2.0f;

    private void Start()
    {
        InvokeRepeating(nameof(SpawnObject), spawnStartTime, spawnRate);
    }

    private void SpawnObject()
    {
        myObject = Instantiate(myObjectPrefab, this.transform.position, this.transform.rotation);
    }
}
```

<br>
<br>

## Destroy:
Destroy object after specific time:
```c#
    private float m_maxLifetime = 10.0f;
    Destroy(this.gameObject, m_maxLifetime);
```
