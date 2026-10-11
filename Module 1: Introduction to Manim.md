# Module 1: Introduction to Manim

Beginner Notes • Python • VS Code • Jupyter Notebook

## 1. What is Manim?

Manim (Mathematical Animation Engine) is a Python library used to create animations for educational videos, mathematics, programming, and technical explanations.

With Manim, you can write Python code to control objects, text, shapes, formulas, graphs, and their movements on screen.

For example, a teacher can use Manim to animate how a Python loop works, how an operating system schedules processes, or how a mathematical equation is solved step by step.


### What can you create with Manim?

* Mathematical formulas and geometry animations

* Python, C, and C++ programming tutorials

* Data structures and algorithm visualizations

* Operating system concepts, such as CPU scheduling

* Animated graphs and data analytics explanations

* Educational videos for YouTube and classroom teaching

Important: Manim generates rendered videos from code. It is not primarily a drag-and-drop video editor.

## 2. How does Manim work?

The basic workflow is:

Step 1: Write Python code

Define text, shapes, and animations.

Step 2: Manim renders the scene

Converts your instructions into video frames.

Step 3: Export the video

Produces an MP4 video you can play or share.

For example, the Python instruction `self.play(Write(title))` tells Manim to animate the appearance of a title.

## 3. Manim Community Edition vs. other versions

There are two commonly discussed versions:

| Feature             | Manim Community Edition    | ManimGL                                   |
| ------------------- | -------------------------- | ----------------------------------------- |
| Python-based        | Yes                        | Yes                                       |
| Main command        | `manim`                    | `manimgl`                                 |
| Typical workflow    | Rendered scenes and videos | Interactive OpenGL-based rendering        |
| Learning resources  | Large community ecosystem  | Different API and workflow                |
| Best starting point | Recommended for beginners  | Useful for specific interactive workflows |

Recommendation: Start with Manim Community Edition (ManimCE). It is suitable for structured lessons, classroom videos, mathematical animations, and programming tutorials.

Code written for one version may need changes to run in the other.

## 4. Installing Python, FFmpeg, and Manim

### Step 1: Check Python

Open Command Prompt or the VS Code terminal.

Bash

```
python --version
```

If Python is installed, you should see a version number. If the command is not recognized, install Python from the official website: [python.org](https://www.python.org/downloads/).

### Step 2: Install FFmpeg

FFmpeg helps Manim process and export video and audio.

On Windows, if `winget` is available, run:

PowerShell

```
winget install Gyan.FFmpeg
```

Close and reopen the terminal, then verify:

Bash

```
ffmpeg -version
```

If Windows cannot find FFmpeg, check that its executable directory is included in your system `PATH`.

### Step 3: Create a virtual environment

Create a folder for your Manim course and open a terminal inside it.

Bash

```
python -m venv manim_env
```

Activate the environment on Windows:

PowerShell

```
.\manim_env\Scripts\activate
```

Install Manim:

Bash

```
python -m pip install --upgrade pip
python -m pip install manim
```

Verify the installation:

Bash

```
manim --version
```

Windows note: Manim's dependencies can require additional system packages. If installation fails, consult the official [Manim Community installation guide](https://docs.manim.community/en/stable/installation.html).

## 5. Setting up Manim in VS Code

1. Install [Visual Studio Code](https://code.visualstudio.com/).

2. Install the Python extension published by Microsoft.

3. Open your Manim project folder.

4. Open the terminal and activate `manim_env`.

5. Select the Python interpreter from `manim_env`.

6. Create a file named `first_animation.py`.

Your folder structure can look like this:

```
Manim_Course/
│
├── manim_env/
├── first_animation.py
└── media/
```

The `media` folder is normally created by Manim when it renders animations.

## 6. Understanding the basic structure of a Manim program

Every basic Manim animation has three important parts:

Python

Run

```
from manim import *

class FirstAnimation(Scene):
    def construct(self):
        title = Text("Hello, Manim!")

        self.play(Write(title))
        self.wait(2)
```

Let's understand each line.

| Code                           | Explanation                              |
| ------------------------------ | ---------------------------------------- |
| `from manim import *`          | Imports Manim classes and functions.     |
| `class FirstAnimation(Scene):` | Defines an animation scene.              |
| `def construct(self):`         | Defines what happens in the scene.       |
| `Text("Hello, Manim!")`        | Creates a text object.                   |
| `self.play(Write(title))`      | Animates the writing of the text.        |
| `self.wait(2)`                 | Keeps the scene visible for two seconds. |

### Important Manim terminology

* Scene: A section of your animation.

* Mobject: An object that Manim can display and animate.

* Animation: An action that changes how an object appears or behaves.

* Render: The process of generating the video frames and final output.

## 7. Practical: Create your first animated text video

Project 1 • Estimated time: 20–30 minutes

The objective is to create a video that displays a title, moves it to the top, and then displays a subtitle.

### Complete Python code

Save this code in `first_animation.py`.

Python

Run

```
from manim import *

class FirstAnimation(Scene):
    def construct(self):

        # Step 1: Create the title
        title = Text(
            "Welcome to Manim",
            font_size=48,
            color=BLUE
        )

        # Step 2: Animate the title
        self.play(Write(title), run_time=2)
        self.wait(1)

        # Step 3: Move the title to the top
        self.play(title.animate.to_edge(UP))
        self.wait(1)

        # Step 4: Create a subtitle
        subtitle = Text(
            "Python Animation Engine",
            font_size=30,
            color=YELLOW
        )

        # Step 5: Display the subtitle
        self.play(FadeIn(subtitle, shift=UP))
        self.wait(2)

        # Step 6: Remove everything
        self.play(
            FadeOut(title),
            FadeOut(subtitle)
        )
        self.wait(1)
```

### Render your animation

Run this command in the VS Code terminal:

Bash

```
manim -pql first_animation.py FirstAnimation
```

The flags mean:

* `-p`: Preview the video after rendering.

* `-q`: Set rendering quality.

* `l`: Use low quality for faster testing.

For higher quality, use:

Bash

```
manim -pqh first_animation.py FirstAnimation
```

The rendered MP4 will be saved under a path similar to:

```
media/videos/first_animation/480p15/FirstAnimation.mp4
```

The exact folder depends on the rendering settings and Manim version.

## 8. Setting up Manim in Jupyter Notebook

You can also write and render animations directly in a Jupyter Notebook.

### Step 1: Install Jupyter

Activate the same virtual environment where you installed Manim, then run:

Bash

```
python -m pip install notebook ipykernel
```

Start Jupyter:

Bash

```
jupyter notebook
```

### Step 2: Load the Manim extension

In a notebook cell, run:

Python

Run

```
%load_ext manim
```

### Step 3: Create an animation in a notebook cell

The `%%manim` command must be the first line in the cell.

Python

Run

```
%%manim -pql NotebookAnimation

from manim import *

class NotebookAnimation(Scene):
    def construct(self):
        text = Text("Learning Manim in Jupyter")

        self.play(Write(text))
        self.wait(2)

        self.play(text.animate.scale(1.3))
        self.wait(1)
```
