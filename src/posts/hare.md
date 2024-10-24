---
title: The 100-year Programming Language
description: In this article we'll explore Hare, a systems programming language that aims to be stable over a very long period of time.
date: '2024-10-22'
categories:
  - hare
  - systems-programming
published: true
---

### So what is Hare?

If you're looking for yet another systems programming language that is trying to substitute C, here is Hare for you!
From the official website:

*["One of Hare’s explicit design goals is to produce a programming language which will be stable over a very long period of time, exceeding the lifetime of its authors: 
I think of Hare as a 100-year programming language."](https://harelang.org/blog/2023-11-08-100-year-language/)*

They also describe it as a simple and robust systems programming language:

*["Hare is a systems programming language designed to be simple, stable, and robust. Hare uses a static type system, manual memory management, and a minimal runtime."](https://harelang.org)*

In this article we'll explore the setup, the basics, and create a simple GUI demo project using Hare.

### Setup

For the sake of reproducibility, we'll be using Arch Linux. The instructions presented here should not be too different in other systems so you'll be able to easily figure out what you need to do in your specific system.

First of all, what we want to do is install the Hare compiler. 

**As you can imagine, Hare is available on the AUR!** That means you can just install it using your favorite AUR helper just like you would with any other program that is available on the AUR. 

We'll use [baph](contact) here, but you can use any AUR helper:

```
baph -i hare
```

You can check where Hare got installed by running `whereis hare`.

If you're using Windows or macOS, however, I have some bad news from the official [Hare documentation](https://harelang.org/documentation/faq.html#will-hare-support-windows-or-macos):

"*Hare does not and will not officially support proprietary operating systems upstream.*"

You can find further explanation in the documentation if you want to read more on this subject. Let's move on to creating a project.

As far as I know, the Hare toolchain doesn't provide us any command for initializing a project, as you would see in many modern programming languagens. This doesn't bother me as I like building my own project structures.

Let's now create a directory called `hare-gui-demo` (yes we are making a GUI application) and `cd` into it:

```bash
mkdir hare-gui-demo
cd hare-gui-demo
```

To create a GUI application, we need a proper GUI library. For this demo, I've chosen to use raylib. Be aware that Raylib is recommended for making games and not any general purpose GUI application. It shouldn't be a problem since *we're just creating a demo.* 

On Arch Linux, you can install raylib via Pacman:

```
pacman -S raylib
```

And that's it.

Let's now create a Makefile, to save our fingers from writing the full `hare build` command everytime.

`Makefile`

```makefile
build:
	hare build -L. -lraylib -lm main.ha
run:
	./main

.PHONY: build run
```

`make build` will build the project, and `make run` will run our project. Very convinient, huh?

As you saw in the Makefile, we'll be creating a **main.ha** file. Hare source files end with **.ha**:

```bash
touch main.ha
```

We won't open this file for now. First, we need to creating a `raylib` directory and `cd` into it:

```bash
mkdir raylib
cd raylib
```

In Hare, a directory defines a module. We'll see the implications of this when editing the `main.ha` file.

Here, let's create a `raylib.ha` file where we'll define symbols to call C code from Hare, i.e the functions from raylib. Inside this file, let's start to write our first Hare program.

### Using Hare + Raylib

To call C code from Hare, we need the C types defined. let's import then, or *use* them:

`raylib.ha`

```rust
use types::c;
```

Apparently the Hare language loves semicolons so get used to it. Let's create a type Color so we can easily create new RGBA color objects:

`raylib.ha`

```js
export type Color = struct {
    r: u8,
    g: u8,
    b: u8,
    a: u8
};
```

We need to put a `export` before the type definition because we're going to use it outside this file. The rest of the code should be readable for most C programmers. Also, think of `type` as being the same as a `typedef`.

One of the most essential raylib functions is InitWindow. it accepts a width, a height, and a string literal as paremeters. The thing is that string literals in Hare are of type `str` and not `const char*`. Fortunately, Hare has a function called `fromstr` defined in the `types::c` module. Let's use it.

`raylib.ha`

```js
export fn InitWindow(width: size, height: size, title: str) void = {
	init_window(width, height, c::fromstr(title));
};

@symbol("InitWindow") fn init_window(size, size, *c::char) void;
```

The init_window function refers to the actual InitWindow function from raylib. The InitWindow function we defined wraps this function, just to convert from a `str` to a `const char*`. This way, we would be able call InitWindow like this:

```js
InitWindow(800,800,"Hello World");
```

Let's export the other raylib functions that we'll want to use:

`raylib.ha`

```js
export @symbol("CloseWindow") fn CloseWindow() void;
export @symbol("WindowShouldClose") fn WindowShouldClose() bool;
export @symbol("BeginDrawing") fn BeginDrawing() void;
export @symbol("EndDrawing") fn EndDrawing() void;
export @symbol("ClearBackground") fn ClearBackground(color: Color) void;
export @symbol("DrawRectangle") fn DrawRectangle(x: int, y: int, w: int, h: int, color: Color) void;
export @symbol("GetColor") fn GetColor(color: int) Color;
export @symbol("IsKeyDown") fn IsKeyDown(key: int) bool;
export @symbol("GetFrameTime") fn GetFrameTime() f32;
```

And now we're done with the `raylib.ha` file. Let's go back to the `main.ha` file.

### Finishing the project

Here, we'll import our raylib module:

`main.ha`

```rust
use raylib;
```

And then define constants for the red and white colors:

`main.ha`

```js
const RED = raylib::Color {
	r = 255,
	g = 0,
	b = 0,
	a = 255,
};

const WHITE = raylib::Color {
	r = 255,
	g = 255,
	b = 255,
	a = 255,
};
```

Note that variables declared as `const` are actually *immutable*.

Finally, let's create our `main` function. *Yes, there's a main function just like C's main function.* Note that it must be "exported" so that the Hare runtime can use it. Also, it accepts no paremeters and returns no values:

`main.ha`

```js
export fn main() void = {
};
```

Now it's time to finally write the logic of our little project. What we'll want to do is:

- Initialize a window with a red background
- Display a white colored box
- Be able to move the box by pressing 'D'.

Let's create the variables `x` and `y` to store the position of the box. Then initialize the window:

`main.ha`

```js
let x: f32 = 0.0;
let y: f32 = 0.0;
raylib::InitWindow(800, 600, "Hello from hare");
```

When using functions defined in another module, you should use the `module_name::function()` syntax.

Let's create the classic raylib loop and close the window properly when we reach out of the loop:

`main.ha`

```js
	for (!raylib::WindowShouldClose()) {
	};
	raylib::CloseWindow();
```

Then, we're going to check if the 'D' key is pressed, and increment `x` if that's the case. I've set 100.0 as the box's speed.

`main.ha`

```js
	for (!raylib::WindowShouldClose()) {
		if (raylib::IsKeyDown('D')) {
			x += 100.0*raylib::GetFrameTime();
		};
	};
```

What we need to do now is actually draw the box and the background:

`main.ha`

```js
	for (!raylib::WindowShouldClose()) {
		if (raylib::IsKeyDown('D')) {
			x += 100.0*raylib::GetFrameTime();
		};
		raylib::BeginDrawing();
		raylib::ClearBackground(RED);
		raylib::DrawRectangle(x: int, y: int, 100, 100, WHITE);
		raylib::EndDrawing();
	};
```

Note that the first 2 paremeters of the DrawRectangle function accepts two ints but `x` and `y` are of type f32. No problem! we converted the types using `:` and specified we want to use them as ints.

The last thing we should do is obviously build and run the project, by running `make build` and `make run`.

And voilà! A ugly red screen with a white box should appear in your screen.

### Overview

Overall, I really liked using Hare and it definitely seems a promising language. It looks like C but has some [type safety](https://harelang.org/tutorials/introduction#thinking-in-terms-of-ownership) features, as well as modules, a built-in build command, etc. 

Would I use it in a future project? Yes. Would I recommend it? Yes, if you're looking for something like C but with much better tooling, safety, and modules, while still being minimal, fast, and elegant. 

It's true that I've been looking for such a language for quite some time, but I really wanted it to be multi-plataform *(that is, I want it to run on Windows and macOS).* If you don't care about this, yeah, Hare is definitely for you.

I'm looking forward to see how the language will evolve and if it's really going to be a 100 year language.

Also feel free to [contact me.](contact)

As always, stay <i>safe</i>.

