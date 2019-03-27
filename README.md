# Von Bits und Beats

## Setup
Bevor wir richtig anfangen, lasst uns prüfen, ob unser Raspberry Pi funktioniert, und eine Umgebung für unser späteres Projekt aufsetzen. Um dies zu tun, befolge einefach folgende Schritte:
  1. Schalte den Raspberry Pi ein, indem du ihn mit Strom versorgst
  2. erstelle einen Ordner "Theremin" auf dem Desktop
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

Im einfachsten Falle erzeugt ein Körper durch Verdrängung genau dies. _Wenn wir doch nur ein Bauelement kennen würden, welches sich elektronisch steuern lässt und seine Form ändern kann ..._


## Herr Fischer, Herr Fischer, wie tief ist das Wasser?


