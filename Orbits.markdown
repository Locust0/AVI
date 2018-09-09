- [HOME](https://avijr.com)

---

# Orbits
- [Steampage](https://store.steampowered.com/app/719350/Orbits/)
- Nov 2014 – Mar 2018
- Made with Unity and Javascript

### Project Description
In senior year of high school I started a game that I just finished a few months ago. It's a 2D space arcade game which features 10+ enemies, 100 unique levels featuring those enemies and 20 unique bosses which build on the themes of the surrounding levels. Check out the steam page!

### Code Examples
Possibly my favorite bit of code I've ever written, this puts any object into a perfectly circular orbit around a nearby center of gravity. It also saves the starting velocity and distance of that orbit so they can be corrected if altered.
```c#
function Orbit ()
{
   if (star1 == null && attractor1 == null)
   {
      return;
   }
			
   //Zero out velocity before Orbit
   GetComponent.<Rigidbody2D>().velocity = Vector2.zero;
   GetComponent.<Rigidbody2D>().angularVelocity = 0;
	
   //location with respect to source of gravity
   var ex : double = 0;
   var wi : double = 0;
   var gravity : double = 15f;
	
   ex = transform.position.x - 
      (star1 ? star1.transform.position.x : attractor1.transform.position.x);
   wi = transform.position.y - 
      (star1 ? star1.transform.position.y : attractor1.transform.position.y);
   gravity = (star1 ? star1.gravity : attractor1.gravity);
	
   //Find force for perfect orbit
   var force : double = 62 * Mathf.Sqrt((200 * 
      GetComponent.<Rigidbody2D>().mass * gravity) / 
      (Mathf.Sqrt((ex * ex) + (wi * wi))));
   
   //If the objects are on top of eachother - causing near infinite force
   if (force > 100000)
   {
      return;
   }
	
   //Split the required force into x and y components then apply them
   if (wi >= 0 && autoOrbit && !reverse) {
      GetComponent.<Rigidbody2D>().AddForce (Vector2.right * -force *
         Mathf.Cos(Mathf.Atan(ex / wi)));
      GetComponent.<Rigidbody2D>().AddForce (Vector2.up * force *
         Mathf.Sin(Mathf.Atan(ex / wi)));
   }
   else if (wi >= 0 && autoOrbit && reverse) {
      GetComponent.<Rigidbody2D>().AddForce (Vector2.right * force *
         Mathf.Cos(Mathf.Atan(ex / wi)));
      GetComponent.<Rigidbody2D>().AddForce (Vector2.up * -force *
         Mathf.Sin(Mathf.Atan(ex / wi)));
   }
   else if (wi < 0 && autoOrbit && !reverse) {
      GetComponent.<Rigidbody2D>().AddForce (Vector2.right * force *
         Mathf.Cos(Mathf.Atan(ex / wi)));
      GetComponent.<Rigidbody2D>().AddForce (Vector2.up * -force *
         Mathf.Sin(Mathf.Atan(ex / wi)));
   }
   else if (wi < 0 && autoOrbit && reverse) {
      GetComponent.<Rigidbody2D>().AddForce (Vector2.right * -force *
         Mathf.Cos(Mathf.Atan(ex / wi)));
      GetComponent.<Rigidbody2D>().AddForce (Vector2.up * force *
         Mathf.Sin(Mathf.Atan(ex / wi)));
   }
   yield WaitForSeconds(0.2);
   startingVel = GetComponent.<Rigidbody2D>().velocity.magnitude;
   startingDist = Mathf.Sqrt((ex * ex) + (wi * wi));
}
```

```c#

```

---

- [HOME](https://avijr.com)
