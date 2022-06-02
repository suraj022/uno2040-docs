# LED fading

In this activity, we'll be controlling brightness of an LED using pwm or **`pulse width modulation`** technique.

!!! info
    Refer to technical jargon page  [HERE](jargon.md) for and explaination to of pwm signal.

## hardware required

| Item                              | Quantity                          |
| --------------------------------- | --------------------------------: |
| **`Raspberry pi pico`**           |  1                                |
| **`Micro USB cable`**             |  1                                |
| **`800pin Breadboard`**           |  1                                |
| **`LED (any colour)`**            |  1                                |
| **`male to male jumpers`**        |  2                                |

<hr>

### circuit diagram

![led circuit](projects/1-1ledblink.png)
<hr/>

!!! note
    The coloured lines represent male to male jumper cables.

### importing libraries

First we need to import 3 libraries namely:


* **time**: Library to impliment time based functions like delays.
* **board**: This library contains all of the pin definitions.
* **pwmio**: code used for generation of digital PWM signals.

we can import these using the syntax

```python
import time
import board
import pwmio
```

### setting up pwm pin

setting up pwm can be done using the following syntax

``` python
led = pwmio.PWMOut(board.GP14, frequency=5000, duty_cycle=0)
```

The arguments for PWMout are as follows:

* **`board.GP14`** : It refers to the pin number that will be used to output pwm signal.

* **`frequency=5000`** : Frequency of the pwm* signal. currently set to 5000hz.

* **`duty_cycle=0`** : It refers to the current the ratio of the ON time of the PWM signal.

!!! info
    The value of duty_cycle consists of a 16-bit integer value. i.e. The value ranges from **`0 to 65536`** where **`0`** is completely **OFF** and **`65536`** being completely **ON**.

### Main loop

The main loop consists of two parts i.e up cycle and down cycle inside the **`#!python while True:`**

#### Up cycle

In this part, the **`duty_cycle`** of the pwm signal increases from **`0 to 65536`** using the following syntax:

```python
for i in range(1000):
    led.duty_cycle = int((i / 1000) * 65535)
    time.sleep(0.001)
```

The loop goes from **`0 to 1000`** with a **`0.001 seconds`** interval hence the complete for loop takes **`1 second`**.

!!! info
    The calculation **`#!python int((i / 1000) * 65535)`** converts the range of **`0 to 1000`** to **`0 to 65535`** which is a 16-bit value.

#### Down cycle

Similar to the [up cycle](./#up-cycle), **`down_cycle`** goes from **`65535 to 0`** using the followinf syntax:


```python
for i in range(1000):
    led.duty_cycle = 65535 - int((i / 1000) * 65535)
    time.sleep(0.001)
```

!!! info
    The calculation **`#!python 65535 - int((i / 1000) * 65535)`** converts the range of **`0 to 1000`** to **`65535 to 0`** which is a 16-bit value.

#### Complete main loop

```python
while True:
        for i in range(1000):
            led.duty_cycle = int((i / 1000) * 65535)
            time.sleep(0.001)
        for i in range(1000):
            led.duty_cycle = 65535 - int((i / 1000) * 65535)
            time.sleep(0.001)
```

## Complete code

Copy the complete code from below

??? example "Complete code" 
    ``` python
    import time
    import board
    import pwmio

    led = pwmio.PWMOut(board.GP25, frequency=5000, duty_cycle=0)

    while True:
        for i in range(1000):
            led.duty_cycle = int((i / 1000) * 65535)
            time.sleep(0.001)
        for i in range(1000):
            led.duty_cycle = 65535 - int((i / 1000) * 65535)
            time.sleep(0.001)
    ```

??? example "Same experiment but using a slightly different code"
    ``` python
    import time
    import board
    import pwmio

    # LED setup for most CircuitPython boards:
    led = pwmio.PWMOut(board.GP14, frequency=5000, duty_cycle=0)

    while True:
        for i in range(65535):
            if i < 32767:
                led.duty_cycle = int(i * 2)  # PWM upcycle
            else:
                led.duty_cycle = 65535 - int((i - 32767) * 2)  # PWM downcycle
            time.sleep(0.0001)

    ```

## Activity

!!! question
    Try adding a second LED and see if you can alternate the Fading sequence between the leds.