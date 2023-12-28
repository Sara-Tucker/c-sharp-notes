# Unity Physics

## Rigidbody:
A component that allows a GameObject to be affected by the physics engine. The rigidbody allows the GameObject to be affected by gravity and it can be controlled from scripts using forces.  
If a collider component is added the GameObject will also respond to collisions with other objects.

### Body Types:
| Body type | Description |
| --- | --- |
| Dynamic | designed to move under simulation |
| Kinematic | designed to move under simulation but only from explicit user control |
| Static | designed to not move under simulation at all and behaves like an immovable object |

https://docs.unity3d.com/Manual/rigidbody2D-body-types.html

### Rigidbody GameObjects without physics-based movement:
There are some cases where you might want the physics system to detect a GameObject, but not to control it. For example, you might want Colliders to detect a GameObject, but you intend to control that GameObject’s movement and position via its Transform.  
Movement in Unity that is not physics-based is called kinematic motion. The Rigidbody component has the property Is Kinematic which, when enabled, defines the attached GameObject as non-physics-based, and removes it from the control of the physics engine. This allows you to move it kinematically via the Transform without Unity’s physics simulation calculations overriding the changes.  
A kinematic Rigidbody can apply physics-based force to physics-based Rigidbody GameObjects, but does not receive physics-based force. For example, a kinematic Rigidbody can collide with and “push” a Rigidbody that has physics-based movement, but a Rigidbody with physics-based movement cannot “push” a kinematic Rigidbody.

<br>
<br>

## Collider:
Colliders define the shape of a GameObject for the purposes of physical collisions.  
Note: Although Rigidbody 2Ds are often described as colliding with each other, it’s the Collider 2Ds attached to each of those bodies which collide. Rigidbody 2Ds can't collide with each other without Colliders.
```c#
private void OnCollisionEnter2D(Collision2D collision)
{
}
```
https://docs.unity3d.com/ScriptReference/Collider.OnCollisionEnter.html
https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnCollisionEnter.html

### Triggers
The scripting system can detect when collisions occur and initiate actions using the OnCollisionEnter function. However, you can also use the physics engine simply to detect when one collider enters the space of another without creating a collision. A collider configured as a Trigger (using the Is Trigger property) does not behave as a solid object and will simply allow other colliders to pass through. When a collider enters its space, a trigger will call the OnTriggerEnter function on the trigger object’s scripts.
```c#
private void OnTriggerEnter2D(Collider2D other)
{
    // Gets called whenever another Collider collides with this object.
    // other is the reference for the object that collided with it.
}
```
https://docs.unity3d.com/ScriptReference/Collider.OnTriggerEnter.html
https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnTriggerEnter.html