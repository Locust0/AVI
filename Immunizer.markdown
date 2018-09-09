- [HOME](https://avijr.com)

---

# Immunizer
- [Dropbox Link](https://www.dropbox.com/s/syenji5x857jasm/Immunizer.app.zip?dl=0)

Jan 2018 – May 2018	(Made using Unity and C#)

### Project description
Created a game for my AI For Game Programming course. You play as a white blood cell within the veins and arteries of a very sick person. The game is 2D with multiple seamlessly connected layers that were modeled by myself after the actual blood vessels of humans. As you move around, there is a current of red blood cells and platelets pushing you through the body. Once an infection appears, it will show up on your mini map so you can head there to quickly to fight off whatever infection has sprung up. All infections are placed randomly and feature 1 of 6 possibly diseases.

### Code Examples
The function which pushes red blood cells away from eachother
```c#
private void PushAway (numRays)
{
	float angle = 0f;
	Vector2 dir = new Vector2(0, 0);
	Vector3 net = Vector3.zero;
	
	//Loop through all rays starting with angle = 0
	for (int i = 0; i < numRays; i++)
	{
		//Find direction of ray
		dir.x = Mathf.Cos (angle);
		dir.y = Mathf.Sin (angle);

		//Cast ray in that direction
		RaycastHit hit;
		if (Physics.Raycast(transform.position, dir, out hit, rayDist, collisionMask))
		{
			//Adjust net force to be applied by the distance to the target
			net += hit.normal * (rayDist - hit.distance) / rayDist;
		}

		angle += Mathf.PI * 2 / numRays;
	}
	//Apply force
	rb.AddForce(net * pushForce);
}
```

The function which causes all red blood cells, platelets, and the player to be affected by the flow of the blood stream at their location.

Note that this only pushes the player if they are moving in the of the blood stream.
```c#
public void OnFrame ()
{
	foreach (GameObject red in reds)
	{
		red.GetComponent<Rigidbody> ().AddForce (GetFlow(red.transform) * flowForce);
	}
	foreach (GameObject plat in plats)
	{
		plat.GetComponent<Rigidbody> ().AddForce (GetFlow(plat.transform) * flowForce * 0.85f);
	}
	if (player)
	{
		Vector2 dir = GetFlow(player.transform);
		//Apply flow force to player if they are moving in the direction of the flow
		if (playerMan.getInput().magnitude > 0 && Vector2.Dot(playerMan.getInput(), dir) > 0)
			playerRig.AddForce (dir * flowForce * 9f);
	}
}
```

---

- [HOME](https://avijr.com)
