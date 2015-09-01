## Part 6: Setting up your FlappyBird (Part 2: Touch Began)

This time, write some code yourself: Write the header and brackets for one non-overriding function called `flap` with no parameters.

In flap, we want to make it so that every time we call the flap method, that the flappy bird jumps. Thus, let's apply some force to the bird. In between the brackets of flap(), add these lines of code:

```
self.physicsBody.applyImpulse(ccp(0, 700))
self.physicsBody.applyAngularImpulse(5000)
```

`ccp()` is the same thing as `CGPointMake()` or `CGPoint(x:, y:)`. It's a shorter way of initializing a CGPoint. These first line applies a "jump" force to the bird. The second line applies an angular force that makes the bird point upwards.

Now we'll implement the touching mechanism. Whenever you touch the screen, you call a function called `touchBegan()`. Code implemented in `touchBegan()` will be executed **every touch**. Add a new function called `touchBegan()` in MainScene.swift below your other functions and call the `flap()` function on `hero` inside the body of `touchBegan()`:

```
override func touchBegan(touch: CCTouch!, withEvent event: CCTouchEvent!) {
    // move up and rotate
    hero?.flap()

    //resets the time so that the bird doesn't rotate immediately after jumping
    sinceTouch = 0;
}
```

In gameplay we have a sinceTouch variable to delay the tilt of the bird until after a certain period of time after a `flap()` call. Don't ask why, it just makes your game feel like the original thing.

Run the program. Every time you tap you should see your bird flap!

#### Understanding Optionals ? and !

The optional `?` notes that if hero is `nil`, `NULL` or has no value, `flap()` will not be executed--which makes sense because if flappy bird doesn't exist, there is no reason we should call `flap()` on a null object. The special part of `?` is that the program continues gracefully and doesn't call that function. Using `?` is equivalent to using an if statement to check if `hero` exists, i.e. `if (hero != nil)`.

This is different to the forced optional `!`, where if hero is `nil`, the program will return an error and crash. Using optionals is a key aspect of dealing with objects in Swift and allows for specialized error checking. In this case, even if the flappy bird doesn't exist and I tap on the screen, the program will not crash and continue fine. If I had `hero!.flap()` and hero was not initialized, the program would crash and show what went wrong.

When you're done go to the [next step, part 7](../P7/part7.md)
