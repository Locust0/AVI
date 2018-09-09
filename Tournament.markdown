- [HOME](https://avijr.com)

---

# Tournament
- [Dropbox link](https://www.dropbox.com/s/zwcg1cjyjnwq4h7/Tournament.app.zip?dl=0)
- Aug 2017 – Dec 2017
- Made with Unity and C#

### Project Description
I created a game for the professor of my Computer Graphics class to get credit for the course. It is a 2D game which procedurally generates an obstacle course within an arena that some simple AI try to get through. You bet on how many will make it judging by the course created and are rewarded money based on how accurate your guess is.

### Code Examples
Spawns all the drones on the left using randomized seperations and offsets

```c#
private IEnumerator SpawnDrones ()
{
   while (dronesSpawned < totalDroneCount)
   {
      //Find total distance through which we can spawn drones
      float totalDist = maxX - minX;

      //Find the maximum seperation we can manage with the current
      //number of drones
      float maxSep = totalDist / (groupSize - 1);

      //Pick a seperation value between min and max
      float sep = Random.Range (minSep, maxSep);

      //How much distance will we cover with this seperation?
      float distCovered = (groupSize - 1) * sep;

      //find the maximum dif from which we can start spawning drones
      //(and have them all fit)
      float distDif = totalDist - distCovered;

      //Pick a dif value to start spawning drones
      float dif = Random.Range (0f, distDif);

      //Spawn them drones!
      Vector2 pos = new Vector2(minX + dif, y);
      for (int i = 0; i < groupSize; i++)
      {
         //Spawn drone at the position and then add the seperation
         //to that position
         Instantiate(drone, pos, transform.rotation);
         pos.x += sep;

         //Add these spawned drones to the total
         dronesSpawned++;
         if (dronesSpawned >= totalDroneCount)
            break;
      }

      //Wait before spawning the next bunch
      yield return new WaitForSeconds(groupSpawnDelay);
   }
}
```

Creates a template object which controls the locations, types and orientations of all obstacles on a board
```c#
public List<Obstacle> PickRandomBoard ()
{
   List<Obstacle> board = new List<Obstacle>();

   //find number of x and y spaces
   int ex = Mathf.RoundToInt((xRange.y - xRange.x) / spacing) + 1;
   int wi = Mathf.RoundToInt((yRange.y - yRange.x) / spacing) + 1;
		
   //Create a bool array to keep track of taken spaces
   bool[,] taken = new bool[ex,wi];
		
   int obstaclesSpawned = 0;
   while(obstaclesSpawned < numObstacles)
   {
      //Pick a random slot to spawn an obstacle
      int tempX = Random.Range (0, ex);
      int tempY = Random.Range (0, wi);
			
      //Check if its taken
      if (taken[tempX, tempY])
         continue;

      //Find the real world coordinates
      float x = (tempX - (xRange.y / spacing)) * spacing;
      float y = (tempY - (yRange.y / spacing)) * spacing;
			
      //Note that this is taken
      taken[tempX, tempY] = true;
			
      //Pick an obstacle to spawn
      int pick = Mathf.RoundToInt(Random.Range (-0.5f, 2.49f));

      //Pick a random rotation
      Quaternion rot = transform.rotation;
      Vector3 eulTemp = rot.eulerAngles;
      eulTemp.z = Random.Range (0, 359);
      rot.eulerAngles = eulTemp;

      //Pick a random direction (for magnets exclusively)
      bool dir = (Random.value > 0.5f);

      board.Add(new Obstacle(pick, new Vector2(x, y), rot, dir));

      //Count the obstacles we've created so far
      obstaclesSpawned++;
   }

   return board;
}
```

---

- [HOME](https://avijr.com)
