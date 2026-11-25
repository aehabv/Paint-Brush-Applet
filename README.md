# Paint Brush

![Java](https://img.shields.io/badge/Java-007396?style=flat&logo=openjdk&logoColor=white)
![AWT](https://img.shields.io/badge/GUI-AWT%20Applet-5382A1?style=flat)
![License](https://img.shields.io/badge/License-CC%20BY--NC%204.0-0a2c46?style=flat)

A small MS Paint clone, written as a Java applet to practise object-oriented design. You pick a colour and a tool, then draw lines, rectangles, ovals or freehand, with optional fill and dotted outlines.

![A drawing made with Paint Brush](done.png)

*Hooray, it works.*

## What it does

| Control | What it does |
|---|---|
| **Pencil** | Freehand drawing while you drag |
| **Line**, **Rect**, **Oval** | Drag from one corner to the other. The shape follows the mouse until you let go |
| **RED**, **GREEN**, **BLUE** | Pick the colour for the next shape |
| **Fill** | Draw rectangles and ovals filled instead of as outlines |
| **Dotted** | Draw outlines with a dotted stroke instead of a solid one |
| **Eraser** | Rub out parts of the drawing |
| **Clear All** | Wipe the canvas |
| **Load** | Put a picture (`pain.jpg`) on the canvas to draw over |

## How it's built

All of it is in `Painter.java`:

- **An abstract `Shape` class** with a `draw(Graphics g)` method, and three subclasses: `Line`, `Rectangle` and `Oval`. Each one knows how to draw itself, solid or dotted, filled or not.
- **A list of shapes.** Every finished shape goes into an `ArrayList<Shape>`, and repainting just asks each one to draw itself. That's polymorphism doing the work: the applet never needs to know which kind of shape it's drawing.
- **A mouse adapter** that tracks press, drag and release to build the shape in progress.
- **The eraser** is a small white rectangle that gets added to the list as you drag.
- **Dotted strokes** use Java 2D's `BasicStroke` with a dash pattern.

## Caveats

- **Applets are dead.** Browsers dropped Java applet support years ago, and Java 11 removed the `appletviewer` tool, so you need Java 8 to run it as it is. The same code would port easily to a Swing `JPanel`.
- **The eraser paints white.** It doesn't remove anything, so erasing over the loaded picture leaves white marks.
- **No undo, and no saving your drawing.**

## How to run

You need Java 8, because it includes `appletviewer`.

```bash
javac Painter.java
appletviewer Painter.html
```

## What I'd like to do next

Move it to Swing so it runs on modern Java, and add undo, a colour picker and "save as PNG".
