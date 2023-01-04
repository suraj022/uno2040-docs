# LED fading

In this activity, we'll be controlling brightness of an LED using pwm or **`pulse width modulation`** technique.

!!! info
    Refer to technical jargon page  [HERE](jargon.md) for and explaination to of pwm signal.

## hardware required

| Item                              | Quantity                          |
| --------------------------------- | --------------------------------: |
| **`UNO 2040 `**                   |  1                                |
| **`UNO 2040 USB cable`**          |  1                                |
| **`800pin Breadboard`**           |  1                                |
| **`LED (any colour)`**            |  1                                |
| **`male to male jumpers`**        |  2                                |

<hr>

### circuit diagram

![blink led circuit](assets/blinkled.png)
<hr/>

!!! note
    The coloured lines represent male to male jumper cables.

### defining the pin and required variable 

Use of variable in this code 

* **int led**: the PWM pin the LED is attached to
* **int brightness**: how bright the LED is
* **int fade**: how many points to fade the LED by

we can make variable using this the code

```c++
int led = 13;        
int brightness = 0;  
int fade = 5;  

```
### Defining led pin as output

defining the led pin

```c++
void setup() {
  pinMode(led, OUTPUT);
}
```

### Main loop
```c++
void loop() {
  // setting the brightness of pin 13:
  analogWrite(led, brightness);
  // change the brightness for next time through the loop:
  brightness = brightness + fade;
  // reverse the direction of the fading at the ends of the fade:
  if (brightness <= 0 || brightness >= 255) {
    fade = -fade;
  }
  // wait for 30 milliseconds 
  delay(30);
}
```
## Complete code

Copy the complete code from below

??? example "Complete code" 
```c++
int led = 9;         
int brightness = 0;  
int fadeAmount = 5;
void setup() {
  pinMode(led, OUTPUT);
}
void loop() {
  analogWrite(led, brightness);
  brightness = brightness + fadeAmount;
  if (brightness <= 0 || brightness >= 255) {
    fadeAmount = -fadeAmount;
  }
  delay(30);
}
```
## Activity

!!! question
    Try adding a second LED and see if you can alternate the Fading sequence between the leds.
