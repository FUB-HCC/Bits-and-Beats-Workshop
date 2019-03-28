# Von Bits und Beats

## Setup
Bevor wir richtig anfangen, lasst uns prüfen, ob unser Raspberry Pi funktioniert, und eine Umgebung für unser späteres Projekt aufsetzen. Um dies zu tun, befolge einefach folgende Schritte:
  1. Schalte den Raspberry Pi ein, indem du ihn mit Strom versorgst
  2. Erstelle einen Ordner "Theremin" auf dem Desktop
  3. Erstelle eine Datei `theremin.py`, indem du in dem Ordner einen Rechtsklick machst und "Neue Datei" auswählst

## Let's make some noise!
`Achtung! Bitte ändert niemals etwas an der Verkabelung, wenn der Raspberry Pi läuft. Es besteht die Gefahr, dass die Elektronik dabei durchbrennt!!!!`

Nachdem wir uns diesen dezenten Aufruf zu Herzen genommen haben, wenden wir uns zuerst einer Möglichkeit zu mit dem Mikrocontroller einen Ton zu erzeugen. Hierfür werden wir einen handelsüblichen Piezobuzzer mit einem Piezoelement verwenden, so wie er auch in beinahe allen PCs verbaut ist.
Wikipedia sagt folgendes:
> Ein Piezoelement ist ein Bauteil, das den Piezoeffekt ausnutzt, um entweder durch Anlegen einer elektrischen Spannung eine mechanische Bewegung auszuführen (Piezoaktor, verwendet den sogenannten inversen Piezoeffekt), oder bei Einwirkung einer mechanischen Kraft eine elektrische Spannung zu produzieren. 

![Piezo Animation](https://upload.wikimedia.org/wikipedia/commons/c/c4/SchemaPiezo.gif)

Das bedeutet also, dass ein Piezoelement je nach angelegter Spannung seine Form ändert. Dies mag jetzt noch nicht besonders klingen (oder vielleicht schon, falls ihr das noch nicht kennt), aber wirklich praktisch wird dieses Bauteil erst wenn wir überlegen, was Schall eigentlich ist.
Schall ist letztendlich nichts anderes als eine Welle, die sich in der Luft als verdichtete und ausgedehnte Teile manifestiert. Das bedeutet also, dass wir Schall (und somit einen Ton) erzeugen können, wenn wir diese Welle erzeugen.

![Schallwellen](https://upload.wikimedia.org/wikipedia/commons/8/82/Spherical_pressure_waves.gif)

Im einfachsten Falle erzeugt ein Körper durch Verdrängung genau dies. _Wenn wir doch nur ein Bauelement kennen würden, welches sich elektronisch steuern lässt und seine Form ändern kann ..._ Und genau hier kommt unser Piezo ins Spiel.

Bevor wir das Bauteil benutzen können, müssen wir es jedoch an eine steuerbare Stromquelle anschließen.
`Schaltet den Raspi bitte erstmal aus, bevor ihr die Schaltung nachbaut!`
Nun könnt ihr die Schaltung wie angegeben nachbauen.

![Buzzer](https://raw.githubusercontent.com/wittenator/girlsday19/master/pics/buzzer.png)

Nun wir es Zeit für das Programmieren:

Macht einen Doppelklick auf die zuvor erstellte Datei namens `theremin.py` und es sollte sich ein Editor öffnen, indem ich nun schreiben könnt.

Zuerst importieren wir die Funktionen, die wir benötigen werden.
```
import RPio.GPIO as GPIO
import time
```
Jetzt sagen wir dem Microcontroller wie er seine Pins verwenden soll. Dazu sagen wir, dass Pin 13 (dort wohin das rote Kabel vom Buzzer führt) ein Ausgang ist und dort Strom hingegeben werden kann.
```
GPIO.setmode(GPIO.BOARD)
PIN_BUZZ = 13
GPIO.setup(PIN_BUZZ, GPIO.OUT)
```

Nun können wir auch schon anfangen und eine Funktion schreiben, die unserer Buzzer ertönen lässt. Dazu sagen wir explizit, dass bei Aufruf der Funktion zuerst Strom auf den Pin gegeben werden soll, dann `sec` Sekunden lang gewartet wird und anschließend der Strom wieder abgestellt wird und noch `wait` Sekunden lang gewartet wird. Somit hören wir einen Ton `sec` Sekunden lang. (Achtet darauf, dass die Einrückung wichtig ist!)
```
def peep(sec, wait):
    GPIO.output(PIN_BUZZ, GPIO.HIGH)
    time.sleep(sec)
    GPIO.output(PIN_BUZZ, GPIO.LOW)
    time.sleep(wait)
```

Das Ganze können wir jetzt testen, indem wir die Funktion ausführen und den Startknopf oben in der Leiste des Editors drücken. Falls ihr nichts hört, ruft einfach einen der Workshopleiter dazu!
Der ganze Code sieht jetzt so aus:
```
import RPio.GPIO as GPIO
import time

GPIO.setmode(GPIO.BOARD)
PIN_BUZZ = 13
GPIO.setup(PIN_BUZZ, GPIO.OUT)

def peep(sec, wait):
    GPIO.output(PIN_BUZZ, GPIO.HIGH)
    time.sleep(sec)
    GPIO.output(PIN_BUZZ, GPIO.LOW)
    time.sleep(wait)

peep(0.5, 0.5)
```

Jetzt ist eure Kreativität gefragt! Ihr könnt `peep()` nun mit verschiedenen Parametern aufrufen und mal gucken, wie sich der Ton verändert.



## Herr Fischer, Herr Fischer, wie tief ist das Wasser?

Wie es der Name vermuten lässt, detektieren Ultraschallsensor den Abstand mithilfe von Ultraschallwellen. Der Sensorkopf gibt eine Ultraschallwelle aus, die vom Zielobjekt zurückreflektiert wird. Ultraschallsensor detektieren den Abstand zum Zielobjekt, indem Sie die Zeit zwischen Senden und Empfangen der Ultraschallwelle messen.

![Buzzer](https://www.keyence.de/Images/sensorbasics_ultrasonic_info_img_01_1547954.jpg)

Der Abstand kann anhand der folgenden Formel berechnet werden:

> L = 1/2 × T × C

wobei L der Abstand, T die Zeit zwischen Senden und Empfangen und C die Schallgeschwindigkeit ist (Der Wert wird mit 1/2 multipliziert, weil T die Zeit für den Hinund den Rückweg der Welle ist).

Bevor wir das neue Bauteil benutzen können, müssen wir es jedoch an eine steuerbare Stromquelle anschließen.
`Schaltet den Raspi bitte erstmal aus, bevor ihr die Schaltung nachbaut! Und ruft einen der Workshopleiter hinzu, bevor ihr das System anschaltet!`
Nun könnt ihr die Schaltung wie angegeben nachbauen.

![Buzzer](https://raw.githubusercontent.com/wittenator/girlsday19/master/pics/theremin.png)

Jetzt erweitern wir unseren zuvor erstellten Code:
Wie zuvor schon müssen wir dem Raspi erstmal sagen wie wir die Pins benutzen wollen. Hierbei ist ein Pin zum Ansteuern des Moduls gedacht (PIN_TRIGGER) und ein Pin um das Ergebnis zurückzubekommen.
```
PIN_TRIGGER = 7
PIN_ECHO = 11

GPIO.setup(PIN_TRIGGER, GPIO.OUT)
GPIO.setup(PIN_ECHO, GPIO.IN)
```

Nun schreiben wir wieder eine Funktion, die uns diesmal den Abstand zu einem Hindernis zurückgibt!
```
def distance():
    time.sleep(0.01)
    GPIO.output(PIN_TRIGGER, GPIO.HIGH)
    time.sleep(0.00001)
    GPIO.output(PIN_TRIGGER, GPIO.LOW)
    
    while GPIO.input(PIN_ECHO)==0:
        pulse_start_time = time.time()
    while GPIO.input(PIN_ECHO)==1:
        pulse_end_time = time.time()
    
    pulse_duration = pulse_end_time - pulse_start_time
    distance = round(pulse_duration * 17150, 2)
    print("Distance:",distance,"cm")
    return distance
```
Diese Funktion sieht erstmal sehr kompliziert aus, aber wenn man sie zerteilt, ist sie eigentlich ganz einfach.
  1. Zuerst muss dem Sensor mitgeteilt werden, dass er eine Messung starten soll. Hierzu setzen wir den Triggerpin für 10 Millisekunden unter Strom. 
  2. Jetzt warten wir auf den Beginn der Messung, indem wir gucken, wann auf dem Echopin eine Antwort ankommt. Diese Zeit speichern wir.
  3. Jetzt warten wir bis das Signal zuende ist und speichern wieder die Zeit.
  4. Die Differenz beider Zeiten ist also die Länge des Signals und praktischerweise ist die Länge dieses Signals genau proportional zur Entfernung zum nächsten Objekt.
  5. Das können wir jetzt mit unserer zuvor entwickelten Formel umrechnen - et voilá, wir haben die Entfernung zum nächsten Objekt erhalten.

Wemn ihr die Funktion jetzt in einer Schleife ausführt, könnt ihr sehen wie der Sensor wiederholt Messungen macht und diese im Terminal ausgibt.
```
while true:
    distance()
```

Der vollständige Code ist jetzt also:
```
import RPio.GPIO as GPIO
import time

GPIO.setmode(GPIO.BOARD)
PIN_BUZZ = 13
PIN_TRIGGER = 7
PIN_ECHO = 11

GPIO.setup(PIN_TRIGGER, GPIO.OUT)
GPIO.setup(PIN_ECHO, GPIO.IN)
GPIO.setup(PIN_BUZZ, GPIO.OUT)

def peep(sec, wait):
    GPIO.output(PIN_BUZZ, GPIO.HIGH)
    time.sleep(sec)
    GPIO.output(PIN_BUZZ, GPIO.LOW)
    time.sleep(wait)
    
def distance():
    time.sleep(0.01)
    GPIO.output(PIN_TRIGGER, GPIO.HIGH)
    time.sleep(0.00001)
    GPIO.output(PIN_TRIGGER, GPIO.LOW)
    
    while GPIO.input(PIN_ECHO)==0:
        pulse_start_time = time.time()
    while GPIO.input(PIN_ECHO)==1:
        pulse_end_time = time.time()
    
    pulse_duration = pulse_end_time - pulse_start_time
    distance = round(pulse_duration * 17150, 2)
    print("Distance:",distance,"cm")
    return distance

while true:
    distance()
```

Von nun an habt ihr die Möglichkeit diese beiden Komponenten beliebig zu kombinieren und zu Beispiel den Output der `distance` Funktion als Input für die `peep` Funktion zu nutzen und dadurch den Pieper zu steuern oder den Buzzer einen komplexeren Beat spielen zu lassen. Werdet kreativ^^

