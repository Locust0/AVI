- [HOME](https://avijr.com)

---

# Immunizer
- [Dropbox Link](https://www.dropbox.com/s/syenji5x857jasm/Immunizer.app.zip?dl=0)

Jan 2018 – May 2018

### Project description
Created a game for my AI For Game Programming course. You play as a white blood cell within the veins and arteries of a very sick person. The game is 2D with multiple seamlessly connected layers that were modeled by myself after the actual blood vessels of humans. As you move around, there is a current of red blood cells and platelets pushing you through the body. Once an infection appears, it will show up on your mini map so you can head there to quickly to fight off whatever infection has sprung up. All infections are placed randomly and feature 1 of 6 possibly diseases.

### Code Example
The function which pushes red blood cells away from eachother
```c#
private void PushAway ()
	{
		float angle = 0f;
		Vector2 dir = new Vector2(0, 0);
		Vector3 net = Vector3.zero;

		for (int i = 0; i < numRays; i++)
		{
			dir.x = Mathf.Cos (angle);
			dir.y = Mathf.Sin (angle);

			//Debug.DrawRay(transform.position, dir * rayDist);
			RaycastHit hit;
			if (Physics.Raycast(transform.position, dir, out hit, rayDist, collisionMask))
			{
				net += hit.normal * (rayDist - hit.distance) / rayDist;
			}

			angle += Mathf.PI * 2 / numRays;
		}
		//Debug.DrawRay(transform.position, net, Color.blue);
		rb.AddForce(net * pushForce);
	}
```

---

- [HOME](https://avijr.com)
