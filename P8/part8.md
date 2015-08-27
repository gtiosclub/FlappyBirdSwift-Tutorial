##

Go ahead and run the program and you'll see that now the pipes are in their proper place.

<!-- Insert picture here -->

But notice how pipes don't automatically spawn continuously? How do we know when to spawn another pipe? We use a function called `update()`.

The iPhone runs at 60fps. This means that every frame, or 1/60th of a second, the function `update()` is called on every `CCNode` object. By default, the update function does nothing. We can use `update()` to check every frame if a pipe has moved across the screen.

 In `MainScene.swift`, add these lines of code as a new function in the class:

```
override func update(delta: CCTime) {
    super.update(delta)

    //checking for removeable obstacles
    for obstacle in obstacles.reverse() {
        let obstacleWorldPosition = _gamePhysicsNode.convertToWorldSpace(obstacle.position)
        let obstacleScreenPosition = convertToNodeSpace(obstacleWorldPosition)

        // obstacle moved past left side of screen?
        if obstacleScreenPosition.x < (-obstacle.contentSize.width) {
            obstacle.removeFromParent()
            obstacles.removeAtIndex(find(obstacles, obstacle)!)

            // for each removed obstacle, add a new one
            spawnNewObstacle()
        }
    }
}

```
