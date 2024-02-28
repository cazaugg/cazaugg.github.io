---
title: "PCB Design Workflow"
date: 2022-12-09T23:05:51+01:00
description: "How does PCB Design Work? A general view of a typical PCB design workflow."
tags: [Hardware, ECAD, KiCad, PCB]
featured_image: "posts/book-wall.jpg"
---

## Overview

You want to design a PCB? Thats how you do it:

- First you draw a schematic. The schematic answers the questions what a circuit does. It shows its components and how they are supposed to interact.
- Second, you design the actual circuit board. This answers the questions where parts are placed and how the interconnects are layed out.
- Third, you generate documentation und fabrication information. This explains to fabrication engineers and machines how each process of manufacturing your PCB is supposed to work.

## Schematic

When you design a circuit, you use a schematic to make a drawing that shows what this thing should do.

> Schematics are primarily documentation. It explains to you and others what a circuit is supposed to do.

Schematics consist of symbols, wires and Text.

- ECAD Tools give you a library of electrical symbols, so you can easily grab and place a symbols and use it as many times as you want. There is a symbol for a resistor or a capacitor, and all resistors as well as the capacitors will use the same symbol regardless of size, value or manufacturer.
- Wires connect the pins of symbols
- Text adds documentation to help people understand the circuit. For example most ECAD tools let you name wires.

Schematics are idealized and simplified versions of the actual board. It shows your intentions with the circuit. Keep that in mind when drawing it, make it easy for readers to understand your schematic. Generally you don't need to draw a schematic, it is possible to just start laying out a circuit board. However this does not make sense, since it is very hard correctly design and understand a circuit without a schematic documentation. Some tips to draw good schematics

- Use a grid (typically 50mil)
- Place inputs on the left, outputs on the right.
- Label important signals and wire them
- Group wires that belong together with a bus
- Write down important links and hints
- Group components in useful Groups
- When using multiple pages, use hierarchal sheets and use the top level sheet as block diagram

## Board Layout

1. Define the board shape and size. Usually there are some requirements on size and mounting to fit it somewhere.
2. Define the layer stack and copper planes.
3. Setup design rules. Especially track sizes, via diameters and clearances.
4. Place all the parts without routing it. Place the parts in groups where they belong. Identify which wires should be short and place parts accordingly.
5. Connect all the parts. Make wires as thick as necessary, don't make them smaller than you need to.
6. Place references and descriptions on silkscreen
7. Always use DRC

## Documentation and Fabrication

To produce a PCB, you need to hire a factory. They need a set of `Gerber` files that tells them what to do. This is an archive with a file for each step in manufacturing. These are text files with text commands for machines, they are barely readable for humans.

- For each copper layer, there is a file telling the machine where to remove the copper
- There is a file for top and bottom solder mask. It tells the machine where to cover the copper with a (usually) green protection
- There is a file containing the outline of the PCB 
- Optionally, there is a file for top and bottom silkscreen. This is the (usually) white text print

Add a PDF with a drawing or an image of the PCB. Add relevant manufacturing information like PCB thickness, color, surface finish and so on.

To assembly a PCB further documentation is required:

- BOM that tells which parts fit onto the PCB. This is usually in CSV or Excel format, sometimes a PDF.
- For each side that has SMD parts assembled, a solder paste mask is required. This is a Gerber file.
- Pick and Place (PNP) Coordinate File. This is a text, CSV or Excel file that is machine readable and contains the coordinates and rotation of each SMD component. This is used by the PNP Machine to drop components in the correct spot.
- PDF file showing where all parts are placed
