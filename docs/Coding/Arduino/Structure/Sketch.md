
The arduino code has two basic "Functions", these functions are a requirement to the sketch to run, other functions can be define and use inside this basic loops, these basic function are:

* `Setup` function.
* `Loop` function.

## `setup()` function

The `setup()` function is called when a sketch starts. Use it to initialize variables, pin modes, start using libraries, etc. The `setup()` function will only run once, after each powerup or reset of the Arduino board.

```C++
void setup(){
  
}
```

one of the statement that are going to be in this function, or that are commonly found, is the function to communicate with the serial port, `Serial.begin(9600);` this is standard and basically is feeding 960 characters per second over the serial

```C++
int buttonPin = 3;

void setup() {
  Serial.begin(9600);
  pinMode(buttonPin, INPUT);
}

void loop() {
  // ...
}
```

## `loop()` function

After creating a `setup()` function, which initializes and sets the initial values, the `loop()` function does precisely what its name suggests, and loops consecutively, allowing your program to change and respond. Use it to actively control the Arduino board.

```C++
int buttonPin = 3;

// setup initializes serial and the button pin
void setup() {
  Serial.begin(9600);
  pinMode(buttonPin, INPUT);
}

// loop checks the button pin each time,
// and will send serial if it is pressed
void loop() {
  if (digitalRead(buttonPin) == HIGH) {
    Serial.write('H');
  }
  else {
    Serial.write('L');
  }

  delay(1000);
}
```



