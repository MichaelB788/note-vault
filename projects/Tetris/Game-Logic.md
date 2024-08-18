# Game Logic

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

> Condition for game to end: Block height reaches limit

## Game Timing

Not particulary concerned with this aspect. I just want a product.

## Handling User Input

h - Move Tetrimino one tile to the left.
j - Increase fall speed of Tetrimino or immediately place it down.
k - Store the block maybe? Not entirely necessary.
l - Move Tetrimino one tile to the right.

r - Rotate Tetrimino clockwise.

## Game Logic

### Collision Detection

Collision detection is a big part of Tetris, and some things we need to consider is
if the current position of the block is valid, making sure this is checked each frame.

The map grid consists of a 11x20 tiles, with each tile being 20px in height and length.
This means that in the screen, the board should be around 220x400 pixels.

It's important to note that when the blocks themselves should have collision, and that
once a block is placed we no longer can move it around. It essentially becomes one with
the field.

So to reiterate, in each frame, we need to check to see if the position of the block
is valid based on the following criteria:

    - A Tetromino position is only valid if none of its tiles overlap
    with another Tetrimino

    - A Tetromino position is invalid if it touches the walls.

    - Once a tetromino reaches the bottom of the map, stop it's fall speed and give
    the player a new tetromino


Once one row of Tetrimino objects is filled, perform the following

- Clear the row

- Give the player points (say 100)

## Render Output

Rendering blocks:

First, we would need an SDL_Rect object so we could modify it to our liking.

Next, we could utilize `SDL_RenderDrawRect()` and `SDL_RenderFillRect()`
can be used in conjunction in order to show the blocks in the screen.

`SDL_RenderDrawRect()` draws the outline, while `SDL_RenderFillRect()`
draws a filled rectangle.

Note that we can change the color we use with `SDL_SetRenderDrawColor()`.
It takes 4 arguments.

`SDL_SetRenderDrawColor(SDL_Renderer* ren, RED, GREEN, BLUE, ALPHA)`
> Values for RGB are form 0-255

Included below is a small sample program from [dev.to](https://dev.to/noah11012/using-sdl2-drawing-rectangles-3hc2)

```CPP
void Application::draw()
{
    SDL_RenderClear(m_window_renderer);

    SDL_Rect rect;
    rect.x = 250;
    rect.y = 150;
    rect.w = 200;
    rect.h = 200;

    SDL_SetRenderDrawColor(m_window_renderer, 255, 255, 255, 255);
    SDL_RenderDrawRect(m_window_renderer, &rect);

    SDL_SetRenderDrawColor(m_window_renderer, 0, 0, 0, 255);

    SDL_RenderPresent(m_window_renderer);
}
```

And here's how it should look example with a filled rect

```CPP
void Application::draw()
{
    ...
    SDL_RenderFillRect(m_window_renderer, &rect);

    ...

    SDL_RenderPresent(m_window_renderer);
}
```
