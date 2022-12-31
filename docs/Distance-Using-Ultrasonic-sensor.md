# Distance using ultrasonic sensor

We will measure distance using HC-SR04 Ultrasonic Sensor 

## hardware required

| Item                              | Quantity                          |
| --------------------------------- | --------------------------------: |
| **`UNO 2040 `**                   |  1                                |
| **`UNO 2040 USB cable`**          |  1                                |
| **`800pin Breadboard`**           |  1                                |
| **`HC-SR04 Ultrasonic Sensor `**  |  1                                |
| **`male to male jumpers`**        |  4                                |

<hr>

## About HC-SR04 Ultrasonic Sensor
![ultra sonic sensor ](docs/assets/ultrasonicsensor.png)

The HC-SR04 Ultrasonic Distance Sensor is a sensor used for detecting the distance to an object by emitting ultrasonic sound waves, and converts the reflected sound into an electrical signal. 

## About HC-SR04 Ultrasonic Sensor Pins 
| PIN NAME                          |FUNCTION                          |
| --------------------------------- | -------------------------------- |
| **`VCC`**                         |supply voltage is nominally 5 V. |
| **`TRIG`**                        |emitting ultrasonic sound waves  |
| **`ECHO`**                        |converts the reflected sound into an electrical signal|
| **`GND `**                        | ground pin                      |


### Circuit diagram
![ultra sonic circuit](docs/assets/ultrasoniccircuit.png)
<hr/>
!!! note
    The coloured lines represent male to male jumper cables.

### Formula To Calculate 

**Formula :**  Distance = Speed * Time 

**Distance** = Speed of sound in air * (Time taken/2)

**Note:** Speed of sound in air = 344 m/s

**Note:** Here we are dividing the Time taken by 2 because sensor will give total time from the emitter to the receiver but we only need the time from emitter to object 

### Defining the HC-SR04 Ultrasonic Sensor pin and making variable 

``` c++
int distance;
long duration;
int echo_pin = 11;
int trig_pin = 12;
```
In duration variable we will store time taken by the sound wave traveling from the emitter to the receiver and In distance variable we will store distance which is calculate

### Setting pin as output

The next thing we need to do is to define the trig pin as output and echo pin as input also we will setup serial monitor using the following code.

```c++
void setup(){
    pinMode(trig_Pin, OUTPUT);  
    pinMode(echo_Pin, INPUT); 
    Serial.begin(9600);
    Serial.println("Distance measurement");
    delay(500);
}
```

### Main loop

Here we are going place the formula and print the distances in serial monitor using the following code.

``` c++
 void loop(){
    digitalWrite(trigPin, LOW);
    delay(2);
    digitalWrite(trigPin,HIGH);
    delay(2);
    digitalWrite(trigPin,LOW); 
    duration = pulseIn(echoPin, HIGH);
    distance = duration * 0.0344 / 2; 
    Serial.print("Distance: ");
    Serial.print(distance); 
    Serial.println(" cm");
    delay(100);
}                      
```

click on **`upload`** icon and the code will upload in uno2040 and open serial monitor you will see the distance from sensor in serial monitor


## Complete code
Copy the complete code from below
??? example "Complete code"
``` c++
int distance;
long duration;
int echo_pin = 11;
int trig_pin = 12;
void setup(){
  pinMode(trig_Pin, OUTPUT);  
  pinMode(echo_Pin, INPUT); 
  Serial.begin(9600);
  Serial.println("Distance measurement");
  delay(500);
}            
void loop(){
  digitalWrite(trigPin, LOW);
  delay(2);
  digitalWrite(trigPin,HIGH);
  delay(2);
  digitalWrite(trigPin,LOW); 
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.0344 / 2; 
  Serial.print("Distance: ");
  Serial.print(distance); 
  Serial.println(" cm");
  delay(100);
}  
```
## Activity
!!! question
    Try mixing and matching blinking using multiple leds and multiple blink patterns.
