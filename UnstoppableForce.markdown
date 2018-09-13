[HOME](https://avijr.com)

---

# Unstoppable Force

![Output sample](https://github.com/Polaros/AVI/raw/master/gifs/unstoppable_force.gif)

- [Dropbox Link](https://www.dropbox.com/s/ek98qgnpva1nrzj/UnstoppableForce.app.zip?dl=0)
- October 2017
- Made using Unity and C#

### Project Description
4 teamates and I made this game for a gamejam. I did most of the programming and work with integrating the artists' work into the game. You play as a scared man running from an unstoppable Lovecraftian monster on the left, forcing you right. The game features platforming and a few varieties of enemies plus spike & flame traps.

### Code Example
This is the code for the very basic floating skull enemies. They wait until triggered. Then, they chase you for 1 second and freeze for 1 second until they've exhausted their maximum number of tries. Then they explode.
```c#
void Update ()
{
   //Wait until triggered and not activated
   if (triggered && !hunting)
   {
      hunting = true;
      //Start attacks
      StartCoroutine (delayedAttacks ());
   }
   //If its time for the skull to chase the player
   if (moving)
   {
      //Move towards the player
      transform.Translate (dir * Time.deltaTime);
      
      //Face the player (either left or right)
      Vector3 temp = transform.localScale;
      temp.x = (dir.x < 0) ? -1 : 1;
      transform.localScale = temp;
   }
   //Play a moving animation when chasing the player
   anim.SetBool ("isMoving", moving);
}
   
IEnumerator delayedAttacks ()
{
   //Try the right number of times
   for (int i = 0; i < numTries; i++)
   {
      //Pick the vector to move along for this 1 second interval
      dir = -new Vector3 (transform.position.x - player.position.x, 
         transform.position.y - player.position.y, 0).normalized;
	 
      //Move for 1 second along this vector
      moving = true;
      yield return new WaitForSeconds (1);
      moving = false;

      //Freeze for a number of seconds
      yield return new WaitForSeconds (delay);
   }
   //Die when out of tries
   Die ();
}
```

---

[HOME](https://avijr.com)
