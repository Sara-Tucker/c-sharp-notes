# Finite State Machine

**Abstract:**  
The abstract modifier indicates that the thing being modified has a missing or incomplete implementation. The abstract modifier can be used with classes, methods, and properties. Use the abstract modifier in a class declaration to indicate that a class is intended only to be a base class of other classes, not instantiated on its own.  
You cannot create an instance of an abstract class, it must be inherited from another class.

**Interface:**  
An interface defines a contract. Any class or struct that implements that contract must provide an implementation of the members defined in the interface. An interface may define a default implementation for members.  
An interface is a completely abstract class, which can only contain abstract methods and properties (with empty bodies).  
It is considered good practice to start with the letter "I" at the beginning of an interface, as it makes it easier for yourself and others to remember that it is an interface and not a class.  
By default, members of an interface are abstract and public.  
Note: Interfaces can contain properties and methods, but not fields.

<br>
<br>

## State:
What it is: the current condition of an object or system
What it does: decides the behavior of an object or system

States:  
Idle  
Move/Moving  
Jump/Jumping  
Fall/Falling

States (apple):  
Growing  
Whole  
Chewed  
Rotten

<br>

## The State Pattern:
An object-oriented way for an object to change its behaviour on the fly based on the inputs it receives.
- Each state is self-contained, changes to one state won't impact other states

1. Create a generic State interface
    - Abstract methods for everything
2. Implement the interface with a class per state
    - Create a class for each state and implement abstract methods
3. Let the parent entity delegate logic to the active state
4. Provide a way for states to transition to one another

<br>

## Finite State Machine:
Rules:
1. There are a finite number of states
2. The machine can only be in one state at a time
3. The state designates object behavior; Each state is responsible for doing one thing only
4. States include transitions to other states
    - The active state receives logical (not key) inputs and responds by following its own rules of when to transition to another state
    - Each state has a set of transitions, each associated with an input and pointing to a state

<br>

## Three parts of a FSM:

Manager / Context:
- Creates instances of concrete states
- Passes data to currently active state
- Contains currently active state
- Inherits from MonoBehaviour

Abstract state:
- A blueprint/prototype class for concrete states
- Defines methods used in all concrete states
- The type definition of the current state handled in the manager/context

Concrete states:
- The individual self-contained states with their own specific behavior
- Implements the abstract methods

<br>
<br>

Simple FSM using enums:
```c#
class Player:
    enum States {
        Idle,
        Walking,
        Falling,
        Jumping
    }

States currentState = States.Idle;

private void Input(event)
{
    switch currentState:
        States.Idle:
            input_idling(event)
        States.Walking:
            input_walking(event)
        States.Falling:
            input_falling(event)
        States.Jumping:
            input_jumping(event)
}
```

<br>
<br>

AppleStateManager.cs - Manager
- This script gets added to the apple prefab
```c#
using UnityEngine;

public class AppleStateManager : MonoBehaviour
{
    // Reference to the active state; State machines can only be in one state at a time.
    AppleBaseState currentState;

    // States
    public AppleGrowingState GrowingState = new AppleGrowingState();
    public AppleWholeState WholeState = new AppleWholeState();
    public AppleChewedState ChewedState = new AppleChewedState();
    public AppleRottenState RottenState = new AppleRottenState();

    void Start()
    {
        // Initial state.
        currentState = GrowingState;
        // Passes the AppleStateManger, which all of our abstract methods expect.
        currentState.EnterState(this);
    }

    void Update()
    {
        currentState.UpdateState(this);
    }

    public void ChangeState(AppleBaseState state)
    {
        currentState = state;
        currentState.EnterState(this);
    }

    void OnCollisionEnter(Collision other)
    {
        currentState.OnCollisionEnter(this);
    }
}
```

AppleBaseState.cs - Abstract State
```c#
using UnityEngine;

public abstract class AppleBaseState
{
    public abstract void EnterState(AppleStateManager apple);

    public abstract void UpdateState(AppleStateManager apple);

    public abstract void OnCollisionEnter(AppleStateManager apple);
}
```

States
```c#
using UnityEngine;

public class AppleGrowingState : AppleBaseState
{
    public override void EnterState(AppleStateManager apple)
    {
        
    }

    public override void UpdateState(AppleStateManager apple)
    {
        if (true)
        {
            // Do state stuff
        }
        else
        {
            apple.ChangeState(apple.WholeState);
        }
    }

    public override void OnCollisionEnter(AppleStateManager apple)
    {
        
    }
}
```

<br>
<br>

Manager
```c#
using UnityEngine;

public class EnemyBrain : MonoBehaviour
{
    [SerializeField] private string initState;// Example: PatrolState
    [SerializeField] private FSMState[] states;
    public FSMState CurrentState { get; set; }

    private void Start()
    {
        ChangeState(initState);
    }

    private void Update()
    {
        CurrentState?.UpdateState(this);
    }

    public void ChangeState(string newStateID)
    {
        FSMState newState = GetState(newStateID);
        if (newState != null)
        {
            CurrentState = newState;
        }
    }

    private FSMState GetState(string newStateID)
    {
        foreach (FSMState state in states)
        {
            if (state.ID == newStateID)
            {
                return state;
            }
        }

        return null;
    }
}
```

State
```c#
using System;

[Serializable]
public class FSMState// Example: AttackState
{
    public string ID;// state name
    public FSMAction[] Actions;// Example: MoveAction, AttackAction, ...
    public FSMTransition[] Transitions;

    public void UpdateState(EnemyBrain enemyBrain)
    {
        ExecuteActions();
        ExecuteTransitions(enemyBrain);
    }

    private void ExecuteActions()
    {
        foreach (FSMAction action in Actions)
        {
            action.Act();
        }
    }

    private void ExecuteTransitions(EnemyBrain enemyBrain)
    {
        if (Transitions == null || Transitions.Length == 0)
            return;

        foreach (FSMTransition transition in Transitions)
        {
            bool value = transition.Decision.Decide();
            if (value)
            {
                enemyBrain.ChangeState(transition.TrueState);
            }
            else
            {
                enemyBrain.ChangeState(transition.FalseState);
            }
        }
    }
}

```

Action
```c#
using UnityEngine;

public abstract class FSMAction : MonoBehaviour
{
    public abstract void Act();
}

```

Decision
```c#
using UnityEngine;

public abstract class FSMDecision : MonoBehaviour
{
    public abstract bool Decide();
}
```

Transition
```c#
using System;

[Serializable]
public class FSMTransition
{
    public FSMDecision Decision;// Example: PlayerInRangeOfAttack -> True or False
    public string TrueState;// Example: CurrentState -> AttackState
    public string FalseState;// Example: CurrentState -> PatrolState
}
```