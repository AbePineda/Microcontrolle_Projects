// segment pins
int segB = 8;
int segF = 9;
int segA = 10;
int segG = 7;
int segC = 6;
int segDP = 5;
int segD = 11;
int segE = 12;


int dig1 = 13;
int dig2 = 2;
int dig3 = 3;
int dig4 = 4;

int countDown = 0;

long int totalAmount = 0;

int var = 0;
bool timerStarter = false;

// digit variables
int ones = 0;
int tens = 0;
int hundreds = 0;
int thousands = 0;

void setup() {
    // segment pins
    pinMode(segB, OUTPUT);
    pinMode(segF, OUTPUT);
    pinMode(segA, OUTPUT);
    pinMode(segG, OUTPUT);
    pinMode(segC, OUTPUT);
    pinMode(segDP, OUTPUT);
    pinMode(segD, OUTPUT);
    pinMode(segE, OUTPUT);
    
    // digit control pins
    pinMode(dig1, OUTPUT);
    pinMode(dig2, OUTPUT);
    pinMode(dig3, OUTPUT);
    pinMode(dig4, OUTPUT);

    // analog pins
    pinMode(A0, OUTPUT);
    pinMode(A1, INPUT);
    pinMode(A2, INPUT);


    Serial.begin(9600);
}

void loop() {
    int pentMeter = analogRead(A2);
    int mappedValue = map(pentMeter, 0, 1023, 0, 1000); // Map

    int sensorValue = analogRead(A1);
    if (sensorValue >= 1023) {
        var++;
        if (var % 2 == 1) {
            timerStarter = true;
        } else {
            timerStarter = false;
        }
        delay(1000); //  button delay
    }

    if (timerStarter) {
        static unsigned long previousMillis = 0;
        static int digitIndex = 0;
        static unsigned long lastDigitChange = 0;
        const unsigned long digitChangeInterval = 5; // Time each digit is displayed in milliseconds

        unsigned long currentMillis = millis();

        totalAmount = countDown + (tens * 10) + (ones) + (hundreds * 100) + (thousands * 1000);

        if (totalAmount > 0) {
            if (currentMillis - previousMillis >= 1000) {
                previousMillis = currentMillis;
                totalAmount--;
                
                // Calculate each digit from totalAmount
                ones = totalAmount % 10;
                tens = (totalAmount / 10) % 10;
                hundreds = (totalAmount / 100) % 10;
                thousands = (totalAmount / 1000) % 10;
            }
        } else {
            beepSoundMulti();
            ones = 0;
            tens = 0;
            hundreds = 0;
            thousands = 0;
        }
        

        if (currentMillis - lastDigitChange >= digitChangeInterval) {
            lastDigitChange = currentMillis;

            // Turn off all digit controls
            digitalWrite(dig1, LOW);
            digitalWrite(dig2, LOW);
            digitalWrite(dig3, LOW);
            digitalWrite(dig4, LOW);

            // Turn off all segments
            digitalWrite(segA, HIGH);
            digitalWrite(segB, HIGH);
            digitalWrite(segC, HIGH);
            digitalWrite(segD, HIGH);
            digitalWrite(segE, HIGH);
            digitalWrite(segF, HIGH);
            digitalWrite(segG, HIGH);
            digitalWrite(segDP, HIGH);


            switch (digitIndex) {
                case 0:
                    digitalWrite(dig4, HIGH); // Units place
                    displayNumber(ones);
                    break;
                case 1:
                    digitalWrite(dig3, HIGH); // Tens place
                    displayNumber(tens);
                    break;
                case 2:
                    digitalWrite(dig2, HIGH); // Hundreds place
                    displayNumber(hundreds);
                    break;
                case 3:
                    digitalWrite(dig1, HIGH); // Thousands place
                    displayNumber(thousands);
                    break;
            }


            digitIndex = (digitIndex + 1) % 4; // Cycle through digits 0 to 3
        }

    } else {
        // Update display with the mapped value from potentiometer
        setNumberValue(mappedValue);
        displayDigits(); 
    }
}

void setNumberValue(int g) {
    if (g >= 0 && g <= 9999) {
        ones = g % 10;
        tens = (g / 10) % 10;
        hundreds = (g / 100) % 10;
        thousands = (g / 1000) % 10;
    }
}

void beepSoundMulti() {
    for(int x = 0; x < 256; x++) {
        analogWrite(A0, x);
        delay(1); 
    }
    for(int x = 255; x >= 0; x--) {
        analogWrite(A0, x);
        delay(1);
    }
}


void displayDigits() {
    // Turn off all digit controls
    digitalWrite(dig1, LOW);
    digitalWrite(dig2, LOW);
    digitalWrite(dig3, LOW);
    digitalWrite(dig4, LOW);

    // Turn off all segments
    digitalWrite(segA, HIGH);
    digitalWrite(segB, HIGH);
    digitalWrite(segC, HIGH);
    digitalWrite(segD, HIGH);
    digitalWrite(segE, HIGH);
    digitalWrite(segF, HIGH);
    digitalWrite(segG, HIGH);
    digitalWrite(segDP, HIGH);


    digitalWrite(dig1, HIGH);
    displayNumber(thousands);
    delay(5);
    digitalWrite(dig1, LOW);


    digitalWrite(dig2, HIGH);
    displayNumber(hundreds);
    delay(5);
    digitalWrite(dig2, LOW);


    digitalWrite(dig3, HIGH);
    displayNumber(tens);
    delay(5);
    digitalWrite(dig3, LOW);

    // Display ones
    digitalWrite(dig4, HIGH);
    displayNumber(ones);
    delay(5);
    digitalWrite(dig4, LOW);
}

void displayNumber(int num) {
    // Turn off all segments initially
    digitalWrite(segA, HIGH);
    digitalWrite(segB, HIGH);
    digitalWrite(segC, HIGH);
    digitalWrite(segD, HIGH);
    digitalWrite(segE, HIGH);
    digitalWrite(segF, HIGH);
    digitalWrite(segG, HIGH);
    digitalWrite(segDP, HIGH);

    switch (num) {
        case 0:
            digitalWrite(segA, LOW);
            digitalWrite(segB, LOW);
            digitalWrite(segC, LOW);
            digitalWrite(segD, LOW);
            digitalWrite(segE, LOW);
            digitalWrite(segF, LOW);
            break;
        case 1:
            digitalWrite(segB, LOW);
            digitalWrite(segC, LOW);
            break;
        case 2:
            digitalWrite(segA, LOW);
            digitalWrite(segB, LOW);
            digitalWrite(segG, LOW);
            digitalWrite(segE, LOW);
            digitalWrite(segD, LOW);
            break;
        case 3:
            digitalWrite(segA, LOW);
            digitalWrite(segB, LOW);
            digitalWrite(segG, LOW);
            digitalWrite(segC, LOW);
            digitalWrite(segD, LOW);
            break;
        case 4:
            digitalWrite(segF, LOW);
            digitalWrite(segG, LOW);
            digitalWrite(segB, LOW);
            digitalWrite(segC, LOW);
            break;
        case 5:
            digitalWrite(segA, LOW);
            digitalWrite(segF, LOW);
            digitalWrite(segG, LOW);
            digitalWrite(segC, LOW);
            digitalWrite(segD, LOW);
            break;
        case 6:
            digitalWrite(segA, LOW);
            digitalWrite(segF, LOW);
            digitalWrite(segG, LOW);
            digitalWrite(segE, LOW);
            digitalWrite(segD, LOW);
            digitalWrite(segC, LOW);
            break;
        case 7:
            digitalWrite(segA, LOW);
            digitalWrite(segB, LOW);
            digitalWrite(segC, LOW);
            break;
        case 8:
            digitalWrite(segA, LOW);
            digitalWrite(segB, LOW);
            digitalWrite(segC, LOW);
            digitalWrite(segD, LOW);
            digitalWrite(segE, LOW);
            digitalWrite(segF, LOW);
            digitalWrite(segG, LOW);
            break;
        case 9:
            digitalWrite(segA, LOW);
            digitalWrite(segB, LOW);
            digitalWrite(segC, LOW);
            digitalWrite(segD, LOW);
            digitalWrite(segF, LOW);
            digitalWrite(segG, LOW);
            break;
    }
}
