# Tetris, the Idea
Here's a "blueprint" I've created for myself in order to break the mold and take a
deep dive into the creation of games I love; more specifically, Tetris.

The goal of this project is to use C++ and SDL2 and learn a thing or two. This is
also my first time using Markdown to organize my thoughts in an elegant format.

New technologies and techniques aside, I just want to have some good old fun writing
code and creating projects. :)

## The Heart of Video Games

Before I delve into this project, I want to keep the philosophy of video games here.
It should look something like this.

```C++
while (conditionUntilGameEnds)
{
    // Handle game timing (smooth experience for all platforms)
    GAME TIMING

    // Handle user input
    INPUT

    // Handle game logic
    GAME LOGIC

    // Render the output
    RENDER OUTPUT
}
```

What you see above is pseudo-code for a game loop, the heart of a video game. The
components I've listed inside the game loop are what 95% of video games use to create
their games.

## The Start
1. Since SDL is the centerpiece of this project, one must
[initialize SDL](https://wiki.libsdl.org/SDL2/CategoryInit).

2. Next, I'll need to [create a window](https://wiki.libsdl.org/SDL2/CategoryVideo),
otherwise how will I see my beautiful progress?

3. Did I create a window without losing sanity? If so, time to draw!
	- There are many things I want to display on screen, but to start I'll focus on
    drawing some Tetrimino, otherwise it wouldn't be Tetris right? Below are some
    helpful links related to drawing:
        - [Pixels](https://wiki.libsdl.org/SDL2/CategoryPixels)
        - [Renderer](https://wiki.libsdl.org/SDL2/CategoryRender)
        - [Surface](https://wiki.libsdl.org/SDL2/CategorySurface)
        - [Rectangles](https://wiki.libsdl.org/SDL2/CategoryRect)

        <br>

4. This could come in much later in development, but at some point having
[audio](https://wiki.libsdl.org/SDL2/CategoryAudio) will be a nice touch.

## Tetris, the Game
### What I want in the starting menu:

1. The Tetris logo in the center of attention (gotta have players know what game they're
playing).

2. Dark background, because nobody likes light mode.

3. Button which starts the game (could also be started by pressing the Enter key).

4. Section to display the high score, perhaps somewhere in the corner.

**Some potentially useful links**: [Event Handlers](https://wiki.libsdl.org/SDL2/CategoryEvents)
and [Keyboard Support](https://wiki.libsdl.org/SDL2/CategoryKeyboard).

<br>

### Game events & objects
1. For any game to start, we need to create a [game loop](https://thatgamesguy.co.uk/cpp-game-dev-1/).
Otherwise players will just be staring at a still screen, and that's not very fun at all!

2. Tetrimino objects make Tetris... Well, Tetris. There are four Tetrimino total.
    
    - These Tetrimino Objects could be stored in an array.
    
    - This will allow me to use an algorithm which randomly selects Tetrimino to draw.

    - A good understanding of Objects and namespaces in C++ will be essential for this
    project!

    > The above method is subject to change, but it's just an idea.

3. There needs to be a way to store Tetrimino and display the next Tetrimino. 
    
    - Perhaps two objects are randomly selected at once?
<br><br>
4. Display the current score count, which increases as more rows are cleared.

    - A global score variable will be useful, especially when updating the high score.
<br><br>
5. Finally, and most unfortunately, we need the game to end. There's a couple
of potential scenarios which can achieve this.

	1. Gameover, which occurs when the **rows** of Tetrimino exceeds the **capacity**.

	2. User quits the game, a GUI and a button should be provided to allow this.
