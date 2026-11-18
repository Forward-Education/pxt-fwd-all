# Line-Following Robot

```package
fwd-fifa=github:Forward-Education/pxt-fwd-fifa#v0.1.7
fwd-sonar=github:Forward-Education/pxt-fwd-modules/fwd-sonar#v1.1.12
fwd-line=github:Forward-Education/pxt-fwd-modules/fwd-line#v1.1.12
```

```template
input.onButtonPressed(Button.A, function () {
    IsDrivingEnabled = true
})
input.onButtonPressed(Button.B, function () {
    IsDrivingEnabled = false
})
let IsDrivingEnabled = false
basic.forever(function () {
    if (IsDrivingEnabled) {
        if (fwdSensors.sonar1.isPastThreshold(0.15, fwdEnums.OverUnder.Under)) {
            fwdMotors.stopDriving()
        } else if (fwdSensors.line2.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(30, 30)
        } else if (fwdSensors.line1.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(0, 30)
        } else if (fwdSensors.line3.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(30, 0)
        }
    } else {
        fwdMotors.stopDriving()
    }
})
```

## Welcome! @showdialog

Robots in warehouses and factories often follow lines on the floor to move goods from place to place. They also need to stop safely when something, or someone, is in the way.

Today you will code a **mobile robot** that follows a line and stops for obstacles.

Build your robot before you start. You will also need a dark line on a light floor, like black electrical tape.

## Three Parts @showdialog

This tutorial has three parts:

1. **Use:** Your code is ready. Get your robot following the line.
2. **Modify:** Change the code to tune how your robot drives.
3. **Create:** Invent something new on your own.

You can stop after any part. Your work is saved.

## Get Ready @showdialog

Turn on your breakout board. Plug your micro:bit into your computer.

## Pair Your micro:bit @showdialog

Click the three dots beside the `|Download|` button. Click **Connect Device**. Follow the steps to pair your micro:bit.

## Download

Click `|Download|` to send the starter code to your micro:bit.

## Part 1: Use @showdialog

Your robot's code is already in the workspace. Let's find out how it works.

1. Follow the instructions at the top of the screen.
2. Click **Tell me more!** for more information.
3. Click the lightbulb for help with the code.

## Use Step 1

Look at your robot. Can you name its parts? What does each one do?

~hint Tell me more!
- The **micro:bit** is the brain. It runs the code and makes decisions.
- The **breakout board** is the backbone. It connects the micro:bit to everything else and holds the battery.
- The **line sensor** and **sonar sensor** are sense organs. They tell the robot what's around it.
- The **motors and wheels** are the limbs. They move the robot.
hint~

## Use Step 2

Look under the front of your robot. The line sensor has **three** small sensors in a row: **line1**, **line2**, and **line3**.

Why do you think it needs three?

~hint Tell me more!
- Each sensor checks whether it's over the line.
- **line2** is in the middle. If it sees the line, the robot is on track.
- **line1** and **line3** are on the sides. If one of them sees the line, the robot is drifting off, and needs to turn back.
hint~

## Use Step 3

Look at the code in ``||basic:forever||``. What do you think the robot will do when:

- the middle sensor sees the line?
- a side sensor sees the line?
- something is in front of the robot?

```blocks
basic.forever(function () {
    if (IsDrivingEnabled) {
        if (fwdSensors.sonar1.isPastThreshold(0.15, fwdEnums.OverUnder.Under)) {
            fwdMotors.stopDriving()
        } else if (fwdSensors.line2.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(30, 30)
        } else if (fwdSensors.line1.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(0, 30)
        } else if (fwdSensors.line3.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(30, 0)
        }
    } else {
        fwdMotors.stopDriving()
    }
})
```

## Use Step 4

Let's test it! Unplug your robot. Put it on the line, with the line under the middle of the line sensor.

Press **A** to start. Press **B** to stop.

Does it follow the line? Was your prediction right?

## Use Step 5

Look at ``||fwdMotors:drive left 0 % right 30 %||``. Why would that make the robot turn?

~hint Tell me more!
- The left wheel stops and the right wheel keeps going, so the robot turns **left**.
- When both wheels go the same speed, like **left 30 % right 30 %**, the robot drives straight.
hint~

## Use Step 6

Now put an obstacle, like a book or your hand, on the line in front of the robot. What happens?

~hint Tell me more!
- ``||fwdSensors:sonar1 is under 0.15 m||`` checks for anything closer than 0.15 m (15 cm).
- If something is there, the robot stops driving. When it's gone, the robot keeps following the line.
hint~

## Use Step 7

The sonar check comes **first** in the code, before the line sensors. Why do you think that matters?

~hint Tell me more!
- The micro:bit checks each rule in order, and runs the **first** one that's true.
- Checking for obstacles first means the robot always stops for something in the way, even when it's on the line. Safety comes first!
hint~

## Checkpoint: You Did It! @showdialog

Your robot follows a line and stops for obstacles!

**Think:** Where else could a line-following robot be useful?

You can stop here. Or click **Next** to go on to **Part 2: Modify**.

## Part 2: Modify @showdialog

Now you will tune how your robot drives.

After each change:

1. Plug in your micro:bit and click `|Download|`.
2. Unplug it and test your robot on the line.

## Modify Step 1

What if the robot stopped **farther** from obstacles?

Change **0.15** in ``||fwdSensors:sonar1 is under 0.15 m||`` to **0.3**. Test it.

~hint Tell me more!
- Now the robot stops 0.3 m (30 cm) away.
- What's a safe distance for a real robot working near people?
hint~

```blocks
basic.forever(function () {
    // @highlight
    if (fwdSensors.sonar1.isPastThreshold(0.3, fwdEnums.OverUnder.Under)) {
        fwdMotors.stopDriving()
    }
})
```

## Modify Step 2

Let's try a faster robot. In ``||fwdMotors:drive left 30 % right 30 %||``, change both numbers to **50**. Test it.

Does it still stay on the line?

~hint Tell me more!
- A faster robot can overshoot the line before the sensors notice.
- Try a few speeds. Which is the fastest one that still follows the line?
hint~

```blocks
basic.forever(function () {
    if (fwdSensors.line2.isLineSensorState(fwdEnums.OnOff.On)) {
        // @highlight
        fwdMotors.tank(50, 50)
    }
})
```

## Modify Step 3

Does your robot lose the line on sharp curves?

Make the turns **sharper**. Change **0** to **-20** in both turning blocks, so one wheel goes backward while the other goes forward.

~hint Tell me more!
- **left -20 % right 30 %** spins the robot left more quickly.
- **left 30 % right -20 %** spins it right more quickly.
- Sharper turns help on tight curves, but can make the robot wobble on straight lines. Test to find the best numbers.
hint~

```blocks
basic.forever(function () {
    if (fwdSensors.line1.isLineSensorState(fwdEnums.OnOff.On)) {
        // @highlight
        fwdMotors.tank(-20, 30)
    } else if (fwdSensors.line3.isLineSensorState(fwdEnums.OnOff.On)) {
        // @highlight
        fwdMotors.tank(30, -20)
    }
})
```

## Modify Step 4

Real robots let people know what they're doing. Let's show an arrow on the micro:bit.

Open ``||basic:Basic||``. Add ``||basic:show arrow||`` inside each line-sensor section: **North** for straight, **West** for left, and **East** for right.

~hint Tell me more!
- Now anyone watching can tell which way the robot is about to go.
hint~

```blocks
basic.forever(function () {
    if (fwdSensors.line2.isLineSensorState(fwdEnums.OnOff.On)) {
        fwdMotors.tank(30, 30)
        // @highlight
        basic.showArrow(ArrowNames.North)
    } else if (fwdSensors.line1.isLineSensorState(fwdEnums.OnOff.On)) {
        fwdMotors.tank(0, 30)
        // @highlight
        basic.showArrow(ArrowNames.West)
    } else if (fwdSensors.line3.isLineSensorState(fwdEnums.OnOff.On)) {
        fwdMotors.tank(30, 0)
        // @highlight
        basic.showArrow(ArrowNames.East)
    }
})
```

## Challenge Time! @showdialog

Right now, your robot waits forever if something blocks the line.

**Challenge:** Make it turn around and go back the way it came.

## Challenge Step 1

Open ``||fwdMotors:Motors||``. Drag ``||fwdMotors:turn right for 90 °||`` under ``||fwdMotors:stop driving||`` in the sonar section. Change **90** to **180**.

~hint Tell me more!
- The motors count how far the wheels turn, so the robot can turn an exact number of degrees.
- **180°** is a half turn, so the robot ends up facing back the way it came.
hint~

```blocks
basic.forever(function () {
    if (fwdSensors.sonar1.isPastThreshold(0.3, fwdEnums.OverUnder.Under)) {
        fwdMotors.stopDriving()
        // @highlight
        fwdMotors.turnFor(FwdFifaTurn.Right, 180)
    }
})
```

## Challenge Step 2

Add a short wait before the turn, so people can see the robot has stopped.

Drag ``||basic:pause (ms)||`` between ``||fwdMotors:stop driving||`` and the turn. Set it to **1000** ms (1 second).

```blocks
basic.forever(function () {
    if (fwdSensors.sonar1.isPastThreshold(0.3, fwdEnums.OverUnder.Under)) {
        fwdMotors.stopDriving()
        // @highlight
        basic.pause(1000)
        fwdMotors.turnFor(FwdFifaTurn.Right, 180)
    }
})
```

## Challenge Step 3

Test your robot. Put an obstacle on the line.

Does it stop, wait, turn around, and find the line again? What would you change?

## Checkpoint: Great Work! @showdialog

Your robot can now handle a blocked path on its own!

**Think:** What other problems might a real delivery robot run into?

You can stop here. Or click **Next** to go on to **Part 3: Create**.

## Part 3: Create @showdialog

Now it's your turn to invent!

**Challenge:** How could your robot be safer, faster, or more helpful? Add your own idea to the code.

There are no steps this time. Test your ideas, change them, and test again. Click the lightbulb if you need ideas.

## Create

Add your own idea to your robot. Download and test it.

~hint Need ideas?
- **Slow down near obstacles:** drive more slowly when something is closer than 0.5 m, and stop when it's closer than 0.15 m.
- **Delivery stops:** when the robot finds a cross line (all three sensors see the line), stop for 3 seconds, then keep going.
- **Battery check:** use ``||fwdSensors:battery level||`` to show a warning icon when the battery is low.
- **Lap counter:** count how many times the robot passes a cross line, and show the total when you press **B**.
hint~

## Reflection @showdialog

Think about your project:

- What was one challenge? How did you solve it?
- What is one thing you want to learn more about?

## Finished! @showdialog

Great work! Click `|Done|` to finish the tutorial.
