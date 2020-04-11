---
layout: post
title: 'Unity Cheat Sheet'
tags: []
status: publish
type: post
published: true
meta:
---
I've been reading [Unity in Action: Multiplatform Game Development in C#](https://www.amazon.com/Unity-Action-Multiplatform-game-development/dp/1617294969) by Joseph Hocking in my spare time. Like most of the Unity resources out there, it's great as a tutorial, less so as a reference book.

I keep remembering that I saw how to do a thing somewhere in the book, and flipping back and forth trying to find it again. This is true for even the most basic stuff, like instantiating a prefab or accessing components of a `GameObject`. I needed a place I could refer back to for a quick refresher.

<!--more-->

In case you need that, too, I've created this post. Hope it's helpful! It's possible some of the details are technically incorrect; if you spot something let me know in the comments!


# Scripting Essentials


`Debug.Log("hi");`

Log a string to the Console.


`StartCoroutine(MyMethod(myArg))`

Run a method in a coroutine.


`yield return new WaitForSeconds(2.0f);`

Call in a coroutine to return control to the spawning method, but receive it back after 2 seconds.



# Game Objects


`public float speed = 3.0f;`

Create an instance variable named `speed` that can be edited using the object inspector GUI.


`private float _x = 0.0f;`

Create a private instance variable named `_x`.


`[SerializeField] private GameObject myPrefab;`

Create a private instance variable that you can nonetheless drag-and-drop object values into in the inspector.


`Instantiate(myPrefab) as GameObject`

Create a new instance of a prefab.


`myGameObject.GetComponent<MyMonoBehaviour>()`

Get a reference to a `MonoBehaviour` subclass defined in a script attached to a `GameObject`, so you can access its public variables or call its methods.


`GameObject.CreatePrimitive(PrimitiveType.Sphere)`

Create a new sphere.


`Destroy(myObject)`

Mark a `GameObject` as destroyed.



# Locations and Movement


`Time.deltaTime`

The time since the last `Update()` call.


`Random.Range(-10f, 10f)`

Get a random number between -10 and 10.


`transform.Rotate(x, y, z)`

Rotate the `GameObject` in its local coordinates. Add `Space.World` as a 4th argument to use global coordinates.


`transform.Translate(x, y, z)`

Move the object.


`transform.localEulerAngles.y`

Get the `GameObject`'s current y-axis (or x- or z-axis) rotation.


`transform.localEulerAngles = new Vector3(x, y, z)`

Set the `GameObject`'s rotation on all three axes.


# Sprites


`SpriteRenderer renderer = myGameObject.GetComponent<SpriteRenderer>();`

Get a game object's `SpriteRenderer`.


`renderer.color = new Color(1.0f, 0.0f, 1.0f);`

Tint a sprite purple.


``` text
[SerializeField] private Sprite _mySprite;

void Start() {
    GetComponent<SpriteRenderer>().sprite = _mySprite;
}
```

Set the `Sprite` associated with a GameObject.


# Wrap-up

That's all for now because that's all I have need of. I'll update this post as I discover more frequently-used concepts. Let me know if you have suggestions!
