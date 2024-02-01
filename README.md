//5_player_quiz_buzzer_system_arduino
#define button1 2   // Button 1
#define button2 3   // Button 2
#define button3 4   // Button 3
#define button4 5   // Button 4
#define button5 6   // Button 5
#define resetButton 7 // Reset button
#define buzzerPin 8 // Buzzer
#define LED1 9   // LED 1
#define LED2 10  // LED 2
#define LED3 11  // LED 3
#define LED4 12  // LED 4
#define LED5 13  // LED 5
#define uint8 unsigned char

uint8 buzzerFlag = 0; // Indicates if the buzzer has been pressed
uint8 buzzerPressedButton = 0; // Holds the value of the button that pressed the buzzer

void setup()
{
  pinMode(buzzerPin, OUTPUT);
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
  pinMode(LED3, OUTPUT);
  pinMode(LED4, OUTPUT);
  pinMode(LED5, OUTPUT);

  pinMode(button1, INPUT_PULLUP);
  pinMode(button2, INPUT_PULLUP);
  pinMode(button3, INPUT_PULLUP);
  pinMode(button4, INPUT_PULLUP);
  pinMode(button5, INPUT_PULLUP);
  pinMode(resetButton, INPUT_PULLUP);

  digitalWrite(LED1, LOW);
  digitalWrite(LED2, LOW);
  digitalWrite(LED3, LOW);
  digitalWrite(LED4, LOW);
  digitalWrite(LED5, LOW);
}

void loop()
{
  uint8 b1State = digitalRead(button1);
  uint8 b2State = digitalRead(button2);
  uint8 b3State = digitalRead(button3);
  uint8 b4State = digitalRead(button4);
  uint8 b5State = digitalRead(button5);
  uint8 resetState = digitalRead(resetButton);

  if (resetState == 0)
  {
    // Reset the system
    resetSystem();
  }

  if (buzzerFlag == 0)
  {
    if (b1State == 0 || b2State == 0 || b3State == 0 || b4State == 0 || b5State == 0)
    {
      buzzerFlag = 1;
      if (b1State == 0)
      {
        buzzerPressedButton = 1;
        digitalWrite(LED1, HIGH);
      }
      else if (b2State == 0)
      {
        buzzerPressedButton = 2;
        digitalWrite(LED2, HIGH);
      }
      else if (b3State == 0)
      {
        buzzerPressedButton = 3;
        digitalWrite(LED3, HIGH);
      }
      else if (b4State == 0)
      {
        buzzerPressedButton = 4;
        digitalWrite(LED4, HIGH);
      }
      else if (b5State == 0)
      {
        buzzerPressedButton = 5;
        digitalWrite(LED5, HIGH);
      }
      soundBuzzer();
    }
  }
}

void soundBuzzer()
{
  for (int i = 0; i < 100; i++)
  {
    digitalWrite(buzzerPin, HIGH);
    delay(2);
    digitalWrite(buzzerPin, LOW);
    delay(2);
  }
}

void resetSystem()
{
  digitalWrite(LED1, LOW);
  digitalWrite(LED2, LOW);
  digitalWrite(LED3, LOW);
  digitalWrite(LED4, LOW);
  digitalWrite(LED5, LOW);

  buzzerFlag = 0;
  buzzerPressedButton = 0;
}
