## Part 8: Setting up your Obstacles (Part 2: Update)

When you ran the program, did you notice how pipes don't automatically spawn continuously? How do we know when to spawn another pipe? We use a function called `update()`.

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
            obstacles.removeAtIndex(obstacles.indexOf(obstacle)!)

            // for each removed obstacle, add a new one
            spawnNewObstacle()
        }
    }
}
```

This will make it so that every time a pipe goes off screen, you remove the pipe from the scene using `obstacle.removeFromParent()`, and add a new one by calling `spawnNewObstacle()`. Remember that to add, you use `addChild()`, and to remove you use `removeFromParent()`. You can also use `removeChild()` but it's not as safe because you can run into some `nil` issues. There's also other methods like `removeAllChildren()`, or `removeChildByName()`, but it's up to you to research the documentation and figure out what works best.

Run the program and your pipes should spawn infinitely.

When you're done go to the [next step, part 9](../P9/part9.md)
