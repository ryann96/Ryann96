---
toc: true
comments: false
layout: post
title: Sprite Animation 2
description: Animating Sprites
type: hacks
courses: { compsci: {week: 5} }
---

<body>
    <div>
        <canvas id="spriteContainer"> <!-- Within the base div is a canvas. An HTML canvas is used only for graphics. It allows the user to access some basic functions related to the image created on the canvas (including animation) -->
            <img id="characterSprite" src="/Ryann96/images/Sprites.png">  // change sprite here
        </canvas>
        <div id="controls"> <!--basic radio buttons which can be used to check whether each individual animaiton works -->
            <input type="radio" name="animation" id="forward" checked>
            <label for="forward">Forward</label><br>
            <input type="radio" name="animation" id="left">
            <label for="left">Left</label><br>
            <input type="radio" name="animation" id="right">
            <label for="right">Left</label><br>
        </div>
    </div>
</body>

<script>
    // start on page load
    window.addEventListener('load', function () {
        const canvas = document.getElementById('spriteContainer');
        const ctx = canvas.getContext('2d');

        //change numbers
        const SPRITE_WIDTH = 76;  // matches sprite pixel width
        const SPRITE_HEIGHT = 65; // matches sprite pixel height
        const FRAME_LIMIT = 4;  // matches number of frames per sprite row, this code assume each row is same

        const SCALE_FACTOR = 2;  // control size of sprite on canvas
        canvas.width = SPRITE_WIDTH * SCALE_FACTOR;
        canvas.height = SPRITE_HEIGHT * SCALE_FACTOR;

        class Character {
            constructor() {
                this.image = document.getElementById("characterSprite");
                this.x = 0;
                this.y = 0;
                this.minFrame = 0;
                this.maxFrame = FRAME_LIMIT;
                this.frameX = 0;
                this.frameY = 0;
            }

            // draw character object
            draw(context) {
                context.drawImage(
                    this.image,
                    this.frameX * SPRITE_WIDTH,
                    this.frameY * SPRITE_HEIGHT,
                    SPRITE_WIDTH,
                    SPRITE_HEIGHT,
                    this.x,
                    this.y,
                    canvas.width,
                    canvas.height
                );
            }

            // update frameX of object
            update() {
                if (this.frameX < this.maxFrame) {
                    this.frameX++;
                } else {
                    this.frameX = 0;
                }
            }
        }

        // character object
        const character = new Character();

        // update frameY of dog object, action from idle, bark, walk radio control
        const controls = document.getElementById('controls');
        controls.addEventListener('click', function (event) {
            if (event.target.tagName === 'INPUT') {
                const selectedAnimation = event.target.id;
                switch (selectedAnimation) {
                    case 'forward':
                        character.frameY = 0;
                        break;
                    case 'left':
                        character.frameY = 1;
                        break;
                    case 'right':
                        character.frameY = 2;
                        break;
                    default:
                        break;
                }
            }
        });

        
    // Animation control variables
    const frameInterval = 200; // Adjust this value for the desired frame rate (e.g., 100ms for 10 frames per second)
    let lastFrameTime = 0;

    // Animation recursive control function
    function animate(currentTime) {
        // Calculate the time elapsed since the last frame
        const deltaTime = currentTime - lastFrameTime;

        // Only update and draw a new frame if enough time has passed
        if (deltaTime >= frameInterval) {
            // Clears the canvas to remove the previous frame.
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draws the current frame of the sprite.
            character.draw(ctx);

            // Updates the `frameX` property to prepare for the next frame in the sprite sheet.
            character.update();

            // Store the current time as the last frame time
            lastFrameTime = currentTime;
        }

        // Uses `requestAnimationFrame` to continue the animation loop.
        requestAnimationFrame(animate);
    }

    // Start the animation loop immediately after the page has loaded.
    requestAnimationFrame(animate); 
    });
</script>