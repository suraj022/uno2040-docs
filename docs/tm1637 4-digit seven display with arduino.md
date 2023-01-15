# Tm1637 4-digit seven display with arduino

Showing some pattern Tm1637 4-digit seven display with the help of arduino

## hardware required

| Item                              | Quantity                          |
| --------------------------------- | --------------------------------: |
| **`UNO 2040 `**                   |  1                                |
| **`UNO 2040 USB cable`**          |  1                                |
| **`tm1637 4-digit seven display`**|  1                                |
| **`male to male jumpers`**        |  4                                |

<hr>


### circuit diagram

![blink led circuit](assets/dth.png)
<hr/>

!!! note
    The coloured lines represent male to male jumper cables  <br>
   

### defining the pin , display and libary

```c++
#include <TM1637.h>
int dio_pin = 3;
int clk_pin = 2;
TM1637 tm(clk_pin, dio_pin);
```
 defining display pin , display and  the libary

!!! note
    Please Install TM1637 libary


### Setting up sensor and brightness of display
 
setting up display and brightness of display

```c++
void setup(){
    tm.begin();
    tm.setBrightness(7);}
```

### Main loop
```c++
void loop(){
    tm.display(1234);
    delay(1000);
    tm.display(12.43);
    delay(1000);
    tm.display("CODE");
    delay(1000);}
```
Showing some different digits and text on display 

## Complete code

Copy the complete code from below

??? example "Complete code" 
```c++
#include <TM1637.h>
int dio_pin = 3;
int clk_pin = 2;
TM1637 tm(clk_pin, dio_pin);
void setup(){
    tm.begin();
    tm.setBrightness(7);}
void loop(){
    tm.display(1234);
    delay(1000);
    tm.display(12.43);
    delay(1000);
    tm.display("CODE");
    delay(1000);}
```
## Activity

!!! question
    Try to show some different things on it 
