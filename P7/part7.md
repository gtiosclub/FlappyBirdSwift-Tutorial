## Part 7: Setting up your Obstacles (Part 1: SpriteBuilder)

Now that you have your bird flappin', we gotta set up the obstacles, the pipes.

**Let** (haha pun) us set some constants first. above `didLoadFromCCB()`, right underneath the class header, add these "let" variables:

```
let firstObstaclePosition: CGFloat = 200
let distanceBetweenObstacles: CGFloat = 160
```

Then, we gotta write a `spawnNewObstacle()` function. Since we already have most of `Obstacle.swift` written for you, go ahead and add a new function to `MainScene.swift`

```
func spawnNewObstacle() {
    var prevObstaclePos = firstObstaclePosition
    if obstacles.count > 0 {
        prevObstaclePos = obstacles.last!.position.x
    }

    // create and add a new obstacle
    let obstacle = CCBReader.load("Obstacle") as! Obstacle
    obstacle.position = ccp(prevObstaclePos + distanceBetweenObstacles, 0)
    obstacle.setupRandomPosition()
    obstacles.append(obstacle)

    //add to scene
    _gamePhysicsNode.addChild(obstacle)
}
```

If you get errors about firstObstaclePosition or distanceBetweenObstacles, you probably put your "let" variables in the wrong place.

Then in the body of `didLoadFromCCB()`, add 3 pipes using the `spawnNewObstacle()` function using a for-loop.

```
// spawn the first obstacles
for i in 1...3 {
    spawnNewObstacle() //have them look this up on how to do a for loop
}
```

Go ahead and run the program now. What do you see?

</br>
<img src="part7-pipe-in-front.png" style="width: 50%; height: 50%">
</br>

We can see that the pipes are loaded in front of the ground. That is because the `zOrder` of the pipes is higher than the `zOrder` of the ground. The zOrder represents the draw order and the way that the layers are rendered in Cocos2D. When we added the pipes to `_gamePhysicsNode`, by default the `zOrder` of the pipe made it so that it shows up on top of the grounds. Every `CCNode` has a `.zOrder` property that we can manipulate and in SpriteBuilder you manipulate the .zOrder property directly by dragging the order in which objects are drawn. More information about `zOrder` can be found [here](http://www.learn-cocos2d.com/files/cocos2d-essential-reference-sample/Influencing_the_Draw_Order.html).

So how do we fix the draw order so that the pipes are in front of the background but behind the ground? We can add Obstacles to **a layer** that will be between the background and ground. Open up SpriteBuilder and open up `MainScene.ccb`. Drag a new `CCNode` inside of the `CCPhysicsNode`(remember that all pipes have to be a child of CCPhysicsNode to be a physics object) right above the two ground objects:

<!-- Insert _obstacle Layer photo here -->
