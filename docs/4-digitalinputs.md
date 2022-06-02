# Digital inputs

In this activity, We'll be interfacing with tactile switches as digital inputs while controlling leds with them and also displaying some messages on the serial terminal.

## hardware required

| Item                              | Quantity                          |
| --------------------------------- | --------------------------------: |
| **`Raspberry pi pico`**           |  1                                |
| **`Micro USB cable`**             |  1                                |
| **`800pin Breadboard`**           |  1                                |
| **`LED (any colour)`**            |  2                                |
| **`Push buttons`**                |  2                                |
| **`male to male jumpers`**        |  9                                |

<hr>

## Interfacing with LEDs

In this part, We'll be using two buttons and two LEDs. The LEDs will be turned on and off by using two tacticle buttons shown in the ciruit diagram.

We'll program both tacticle switches in two ways: **`Momentary mode`** and **`on/off mode`**.

### Circuit diagram

![led circuit](projects/4-1digitalinputs.png)
<hr/>

!!! note
    The coloured lines represent male to male jumper cables.

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

### Boolean variable to store button state

The following variable stores the state of the button latch

```python
state = False
```

### Setting pins as output

The next thing we need to do is to define the pins as outputs using the following syntax.

```python
led1 = digitalio.DigitalInOut(board.GP12)
led1.direction = digitalio.Direction.OUTPUT

led2 = digitalio.DigitalInOut(board.GP13)
led2.direction = digitalio.Direction.OUTPUT
```

### Setting up digital input

Next thing is to setup a digital input pin using the following syntax

```python
switch1 = digitalio.DigitalInOut(board.GP14)
switch1.direction = digitalio.Direction.INPUT
switch1.pull = digitalio.Pull.UP

switch2 = digitalio.DigitalInOut(board.GP15)
switch2.direction = digitalio.Direction.INPUT
switch2.pull = digitalio.Pull.UP
```

### Main loop

In the main loop inside **`#!python while True:`** there are two control statements:

#### Momentary switching

Momentary Switch requires a simple **`if else`** control statement where the condition is switch1's value and depending on it the led1 turns on or off. Syntax for the same is as follows:

```python
if switch1.value:
    led1.value = False
else:
    led1.value = True
```

#### Latching switch

Latching switch alternates the state of the LED by turning it on and off from each subsequent key presses. Each button press alternates the value of **`state`** variable from **`True`** to **`False`** and vice versa and set the led1's value accordingly. The syntax is as follows:

```python
if not switch2.value:    
    if state == False:
        state = True
    else:
        state = False

led2.value = state
```

!!!info 

    `not` is used in above if statement because the default state of input is set to pull-up. Hence, using `not` inverts the logic.
    Alternatively we can also write the statement as `#!python if switch2.value == False:` which will yield the same result.

After that a small debounce delay is added to prevent rapid switching of LEDs.

```python
time.sleep(0.2)  # debounce delay, Sleep for 0.2 seconds or 200 ms
```


### Complete code

??? example "Complete code" 
    ```python
    import time
    import board
    import digitalio

    state = False

    led1 = digitalio.DigitalInOut(board.GP12)
    led1.direction = digitalio.Direction.OUTPUT

    led2 = digitalio.DigitalInOut(board.GP13)
    led2.direction = digitalio.Direction.OUTPUT

    switch1 = digitalio.DigitalInOut(board.GP14)
    switch1.direction = digitalio.Direction.INPUT
    switch1.pull = digitalio.Pull.UP

    switch2 = digitalio.DigitalInOut(board.GP15)
    switch2.direction = digitalio.Direction.INPUT
    switch2.pull = digitalio.Pull.UP

    while True:
        if switch1.value:
            led1.value = False
        else:
            led1.value = True
            
        if not switch2.value:    
            if state == False:
                state = True
            else:
                state = False
    
        led2.value = state
        
        time.sleep(0.2)  # debounce delay, Sleep for 0.2 seconds or 200 ms
    ```

## Interfacing with Serial monitor

Second part is about interfacing buttons (tactile switches) with your pc (computer/laptop). We'll use the same 2 buttons

### Circuit diagram

![led circuit](projects/4-2digitalinputs.png)
    <hr/>

!!! note
    The coloured lines represent male to male jumper cables.

### Serial communication

!!! info
    Refer to technical jargon page [HERE](jargon.md) for and explaination to of Serial communication.

In this activity, We'll use two tactile switches to send two different data to the computer using serial module. An example syntax is as follow:

A simple text information can be sent using:

```python
print("hello world")
```

Similarly, We can also display variable values like:

```python
variable1 = 128

print("value of variable1 is", variable1)
```

### Importing libraries 

In addition to the 3 libraries used above, we'll also use the following library. It's use will be explained below.

* **microcontroller**: This library contains microcontroller specific functions.

we can import by using the following statement.

``` python
import microcontroller
```

### Setting up digital input

!!! info
    same as [above](#setting-up-digital-input)

### Main loop

We'll use switch number 1 to print a simple text message and switch number 2 to print pico's current CPU temperature in degree celsius.

```python
while True:
    if not switch1.value:
        print("helloworld")
    if not switch2.value:
        print("Current CPU temperature is:", microcontroller.cpu.temperature)
    time.sleep(0.2)
```
## Complete code

Copy the complete code from below

??? example "Complete code"
    ```python
    import microcontroller
    import board
    import digitalio
    import time

    switch1 = digitalio.DigitalInOut(board.GP14)
    switch1.direction = digitalio.Direction.INPUT
    switch1.pull = digitalio.Pull.UP

    switch2 = digitalio.DigitalInOut(board.GP15)
    switch2.direction = digitalio.Direction.INPUT
    switch2.pull = digitalio.Pull.UP

    while True:
        if not switch1.value:
            print("helloworld")
        if not switch2.value:
            print("Current CPU temperature is:", microcontroller.cpu.temperature)
        time.sleep(0.2)
    ```
## Activity

!!! question
    Constantly print both the switch's value on the serial terminal.