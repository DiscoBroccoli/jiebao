---
layout: project
type: project
published: True
image: images/prod_diss.gif
title: Turbulent Kinetic Energy Production and Dissipation
permalink: projects/micromouse
# All dates must be YYYY-MM-DD format!
date: 2020-11-01
labels:
  - Turbulence
  - TKE Transport Equation
  - RANS
summary: Discussion of a detailed deconstruction of the critical TKE Production and Dissipation Equations.
---

<div>
  <img class="ui image" src="../images/micromouse-robot.png">
</div>

<div align="center">
  <img class="ui image" src="../images/Production.gif">
</div>

Micromouse is an event where small robot “mice” solve a 16 x 16 maze.  Events are held worldwide.  The maze is made up of a 16 by 16 gird of cells, each 180 mm square with walls 50 mm high.  The mice are completely autonomous robots that must find their way from a predetermined starting position to the central area of the maze unaided.  The mouse will need to keep track of where it is, discover walls as it explores, map out the maze and detect when it has reached the center.  having reached the center, the mouse will typically perform additional searches of the maze until it has found the most optimal route from the start to the center.  Once the most optimal route has been determined, the mouse will run that route in the shortest possible time.

For this project, I was the lead programmer who was responsible for programming the various capabilities of the mouse.  I started by programming the basics, such as sensor polling and motor actuation using interrupts.  From there, I then programmed the basic PD controls for the motors of the mouse.  The PD control the drive so that the mouse would stay centered while traversing the maze and keep the mouse driving straight.  I also programmed basic algorithms used to solve the maze such as a right wall hugger and a left wall hugger algorithm.  From there I worked on a flood-fill algorithm to help the mouse track where it is in the maze, and to map the route it takes.  We finished with the fastest mouse who finished the maze within our college.

Here is some code that illustrates how we read values from the line sensors:

```js
byte ADCRead(byte ch)
{
    word value;
    ADC1SC1 = ch;
    while (ADC1SC1_COCO != 1)
    {   // wait until ADC conversion is completed   
    }
    return ADC1RL;  // lower 8-bit value out of 10-bit data from the ADC
}
```

You can learn more at the [AGARD-R-819](https://www.sto.nato.int/publications/AGARD/Forms/AllItems.aspx?RootFolder=%2Fpublications%2FAGARD%2FAGARD%2DR%2D819&FolderCTID=0x0120D5200078F9E87043356C409A0D30823AFA16F60B00B8BCE98BB37EB24A8258823D6B11F157&View=%7B7E9C814C-056A-4D31-8392-7C6752B2AF2B%7D).



