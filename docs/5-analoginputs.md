# Analog inputs

Inputs from potentiometer and display its output on screen or control an led's brightness.
Interfacing a 10k potentiometer and control and led brightness 

## hardware required

| Item                              | Quantity                          |
| --------------------------------- | --------------------------------: |
| **`Raspberry pi pico`**           |  1                                |
| **`Micro USB cable`**             |  1                                |
| **`800pin Breadboard`**           |  1                                |
| **`LED (any colour)`**            |  1                                |
| **`10k potentiometer`**           |  1                                |
| **`male to male jumpers`**        |  5                                |

### Circuit diagram

![led circuit](projects/5-1analoginputs.png)
<hr/>

!!! info
    Raspberry pi pico only has three analog inputs (ADC) channels available on pins **`GP26_A0`**, **`GP27_A1`** and **`GP28_A2`**


### Importing libraries

First we need to import 4 libraries namely:

* **board**: This library contains all of the pin definitions.
* **time**: Library to impliment time based functions like delays.
* **pwmio**: code used for generation of digital PWM signals.
* **analogio**: code used to input analog values and convert them to digital values.

we can import these using the syntax

``` python
import board
import time
import pwmio
import analogio
```

### Setting up inputs and outputs

Setting up pwm output can be done using the following syntax

``` python
led = pwmio.PWMOut(board.GP14, frequency=5000, duty_cycle=0)
```

The arguments for PWMout are as follows:

* **`board.GP14`** : It refers to the pin number that will be used to output pwm signal.

* **`frequency=5000`** : Frequency of the pwm* signal. currently set to 5000hz.

* **`duty_cycle=0`** : It refers to the current the ratio of the ON time of the PWM signal.

!!! info
    The value of duty_cycle consists of a 16-bit integer value. i.e. The value ranges from **`0 to 65536`** where **`0`** is completely **OFF** and **`65536`** being completely **ON**.


Next thing is defining analog input pin using the following syntax.

```python
analog_in = analogio.AnalogIn(board.GP26_A0)
```

!!! info 
    Raspberry pi pico supports three analogIn channels as stated [above](#circuit-diagram).

!!! note
    Raspberry pi pico has 12-bit analog channels but the code **`analogio.AnalogIn(board.GP26_A0)`** returns 16-bit integer value which ranges from **`0 to 65535`**. Due to the conversion of **`12-bit`** to **`16-bit`**, the true range will never be truely **`0`** and **`65535`** but will be apporx. **`300`** to **`65400`**.

### Main loop

Inside our main loop `#!python while True:`, We'll create a local variable called `aInput`. 

!!! info 
    A variable name can be anything but should not start with a number.

We'll store our analog value into this variable using the syntax:

```python
aInput = analog_in.value
```

Next, We'll assign this value to the **`duty_cycle`** of the led and simultaneously print the values on the serial monitor. the complete main loop is as follows:

```python
while True:
    aInput = analog_in.value
    led.duty_cycle = aInput
    print(aInput)
    time.sleep(0.1)
```

!!!note
    The numeric value in inside `#!python time.sleep()` can be increased or decreased to simultaneously decrease or increase the sampling rate.

If you want to plot a graph of analog values with respect to time, we'll have to change the print command to:

```python
print((aInput,))
```

After making the changes, click on plotter icon from the top menu.

![led circuit](projects/5-2analoginputs.png)
<hr/>


Serial plotter graph will appear on the bottom which will display analog values with respect to time.

![led circuit](projects/5-3analoginputs.png)
<hr/>

## Complete code

Copy the complete code from below

??? example "Complete code"
    ```python
    import time
    import board
    import pwmio
    import analogio

    led = pwmio.PWMOut(board.GP14, frequency=5000, duty_cycle=0)

    analog_in = analogio.AnalogIn(board.GP26_A0)

    while True:
        aInput = analog_in.value
        led.duty_cycle = aInput
        print(aInput)
        time.sleep(0.1)
    ```


## Activity

!!! question
    Add a second potentiometer and control the on board LED while also controlling the first LED connected to pin **`GP14`**.