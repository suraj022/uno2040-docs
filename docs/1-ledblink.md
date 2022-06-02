# LED blink circuit

The blinking LED circuit is like the electronics version of the “Hello World”-program. We'll be blinking a single LED with customizable intervals.

## hardware required

| Item                              | Quantity                          |
| --------------------------------- | --------------------------------: |
| **`Raspberry pi pico`**           |  1                                |
| **`Micro USB cable`**             |  1                                |
| **`800pin Breadboard`**           |  1                                |
| **`LED (any colour)`**            |  1                                |
| **`male to male jumpers`**        |  2                                |

<hr>

## Blinking on-board LED

Raspberry pi pico has an on-board led internally connected to GP25 pin. 

### Importing libraries

First we need to import 3 libraries namely:

* **board**: This library contains all of the pin definitions.
* **digitalio**: code for interfacing digital input/output devices.
* **time**: Library to impliment time based functions like delays.

we can import these using the syntax

``` python
import board
import digitalio
import time
```

### Setting pin as output

The next thing we need to do is to define the pin as output using the following syntax.

```python
led = digitalio.DigitalInOut(board.GP25)
led.direction = digitalio.Direction.OUTPUT
```

### Main loop

The last thing to do is to repeatedly turn the led on and off inside **`#!python while True:`** loop.

``` python
while True:
    led.value = True
    time.sleep(0.5)
    led.value = False
    time.sleep(0.5)
```

click on **`save`** icon and the code with automatically start running and you can see the on-board led start blinking.

!!! note

    the number `#!python 0.5` denotes the number of seconds. Increasing the number will make the blinking effect slower and vice versa.

Go ahead and try a different value, something like:

``` python
while True:
    led.value = True
    time.sleep(0.1)
    led.value = False
    time.sleep(1)
```

and click **`save`**. You'll notice a different blink pattern.

<hr/>

Copy the complete code from below.

??? example "Complete code"
    ``` python
    import board
    import digitalio
    import time

    led = digitalio.DigitalInOut(board.GP25)
    led.direction = digitalio.Direction.OUTPUT

    while True:
        led.value = True
        time.sleep(0.5)
        led.value = False
        time.sleep(0.5)
    ```


## blinking an external LED

We'll be connecting an LED (any colour) to GP13 according to the circuit diagram below.

!!! info
    GP13 can be replaced with any available GPIO pin (refer to the [introduction](index.md#pinout-and-pin-definitions) page for full list of available GPIO pins)

### circuit diagram

![led circuit](projects/1-1ledblink.png)
<hr/>

!!! note
    The coloured lines represent male to male jumper cables.

### code changes

we only need to change the GPIO pin number from **`GP25`** to **`GP13`** in the following line.

```python
led = digitalio.DigitalInOut(board.GP13)
```

## Complete code

Copy the complete code from below

??? example "Complete code"
    ``` python
    import board
    import digitalio
    import time

    led = digitalio.DigitalInOut(board.GP13)
    led.direction = digitalio.Direction.OUTPUT

    while True:
        led.value = True
        time.sleep(0.5)
        led.value = False
        time.sleep(0.5)
    ```


## Activity

!!! question
    Try mixing and matching blinking using multiple leds and multiple blink patterns.