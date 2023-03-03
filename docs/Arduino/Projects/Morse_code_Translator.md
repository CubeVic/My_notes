## Description

I will take a sentence from the serial com and later use the LEDs to output the same sentence using Morse code.

## The Structure

### Definition of variables

* Two variables `int` to define the LED output and the delay between the dots.
* A list of `char` that will represent the letters from A-Z.
* A list of `char` that represent the numbers from 0-9.

```C++
int ledPin = 13;
int dotDelay = 200;

char* letters[] = {
  ".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..",    // A-I
  ".---", "-.-", ".-..", "--", "-.", "---", ".--.", "--.-", ".-.",  // J-R
  "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--.."          // S-Z
};

char* numbers[] = {
  "-----", ".----", "..---", "...--", "....-", ".....", "-....", "--...", "---..", "----."};
```

### `setup()`

The setup will contain the definition of the output `pinMode()` and the baud for the serial communication.

```C++
void setup()
{
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}
```

### `loop()`

Here will be the main loop of the sketch.

1. First, I create a `char` variable that holds a character. The character will come from the input, one character at a time.
2.  I use the `Serial.available()` to check if something is waiting in the serial port.
3. It will read the serial input and save one character at a time in the variable `ch`.
4. A `if/else` conditionals that compare the input with letters (Arduino will read/interpret every letter as its value in ASCII).
5. Inside the `if/else` there is a function `flashSequence()` that will take as input one element of the list `letters[]`, the element is selected by subtracting the ASCII value of the letter taken from the serial input and a letter of the alphabet `[ch - 'a']`
6. A delay statement to make a gap between words (`delay(dotDelay * 4)`).

### The functions

There will be two functions:

* `flashSequence()`: it is going to execute the flash sequence, and check if the is more sentence or words on the serial input.
* `flashDotOrDash()`: is the function that will make the LED flash.

### The final script or sketch:

```C++
// Morse code translator

int ledPin = 13;
int dotDelay = 200;

char* letters[] = {
  ".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..",    // A-I
  ".---", "-.-", ".-..", "--", "-.", "---", ".--.", "--.-", ".-.",  // J-R
  "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--.."          // S-Z
};

char* numbers[] = {
  "-----", ".----", "..---", "...--", "....-", ".....", "-....", "--...", "---..", "----."};

void setup()
{
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop()
{
  char ch;
  if (Serial.available() > 0)
  {
    ch = Serial.read();
    if (ch >= 'a' && ch <= 'z')
    {
      flashSequence(letters[ch - 'a']);
    }
    else if (ch >= 'A' && ch <= 'Z')
    {
      flashSequence(letters[ch - 'A']);
    }
    else if (ch >= '0' && ch <= '9')
    {
      flashSequence(numbers[ch - '0']);
    }
    else if (ch == ' ')
    {
      delay(dotDelay * 4);  // gap between words
    }
  }
}

void flashSequence(char* sequence)
{
  int i = 0;
  while (sequence[i] != NULL)
  {
    flashDotOrDash(sequence[i]);
    i++;
  }
  delay(dotDelay * 3);    // gap between letters
}

void flashDotOrDash(char dotOrDash)
{
  digitalWrite(ledPin, HIGH);
  if (dotOrDash == '.')
  {
    delay(dotDelay);
  }
  else // must be a dash
  {
    delay(dotDelay * 3);
  }
  digitalWrite(ledPin, LOW);
  delay(dotDelay); // gap between flashes
}
```
