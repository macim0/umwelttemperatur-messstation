# Umweltmessstation

## Schritt 1: Messwerte aufnehmen
Wir sollten als erstes den Sensor testen. Dafür wollen wir nach dem Drücken der A und B Taste (A+B), 10 Messwerte anzeigen. 
Als erstes benötigen wir aus dem Bereich ``||Input: Eingabe||`` den Block ``||Input: Wenn Knopf A gedrückt||``. Nun ändern wir noch den Knopf A auf A+B.
Anschließend wollen die Messwere Anzeigen. Da es immer wieder die gleiche Aufgabe ist, können wir eine ``||Loops: Schleife||`` nutzen z.B. ``||Loops: 4-mal wiederholen||``.
In dieser Schleif rufen wir immer wieder die Temperatur ab (``||Input: Temperatur (C)||``) und zeigen diese an (``||basic: Zeige Zahl||``), außerdem machen wir nach jedem Durchgang eine Pause von 1 Sekunde (``||basic: pausiere (ms) 100||``).


```blocks
input.onButtonPressed(Button.AB, function () {
    for (let index = 0; index < 10; index++) {
        basic.showNumber(input.temperature())
        basic.pause(1000)
    }
})
```

## Schritt 2: Messwerte speichern
Nun sollten wir die Werte speichern. Hierfür legen wir eine ``||Variables: Variable||`` vor der Schleife an z.B. ``||Variables: Messwerte||``. 
In diese Variable kommt ein ``||Array: leeres Array||``, diese findest du unter ``||advanced: Fortgeschritten||`` und dann unter ``||Array: Arrays||``.
In der Schleife ersetzen wir ``||basic: zeige Zahl|`` durch ``||Array: list füge Wert am Ende hinzu||``. 
In den freien Teil kommt unser ``||Input: Temperatur (°C)||`` und die ``||Variables: Variable||`` ``||Variables: list||`` erstzen wir durch ``||Variables: Messwerte||``.

```blocks
let Messwerte: number[] = []
input.onButtonPressed(Button.AB, function () {
    Messwerte = []
    for (let index = 0; index < 10; index++) {
        Messwerte.push(input.temperature())
        basic.pause(100)
    }
})
```

## Schritt 3: Alarm
Um einen dauerhaften Alarm zu erzeugen benötigen wir wieder eine ``||Variables: Variable||``. 
Diese könnten wir z.B. ``||Variables: Alarm_an||`` nennen und erstellen Sie direkt nach dem Aufnehmen der Messwerte. 
Wir geben der ``||Variables: Variable||`` den Wert ``||Logic: wahr||`` (diesen Block finden wir im Bereich ``||Logic: Logik||``).
Nun nutzen wir die ``||Loops: Schleife||`` ``||Loops: während wahr||`` und erstzen das Feld mit dem ``||Logic: wahr||`` durch unsere ``||Variables: Variable||`` ``||Variables: Alarm_an||``, somit wird alles, was jetzt folgt, solange ausgeführt bis, der Alarm deaktiviert wird.
In der ``||Loops: Schleife||`` kann man jetzt z.B. die RGB-LED blinken lassen oder einen Text auf dem Display ausgeben. Wir wollen aber Töne abspielen. 
Hierfür suchen wir uns 2 Noten aus dem Bereich ``||Music: Musik||`` aus und fügen es einfach in die ``||Loops: Schleife||`` ein.


```blocks
let Alarm_an = false
let Messwerte: number[] = []
input.onButtonPressed(Button.AB, function () {
    Messwerte = []
    for (let index = 0; index < 10; index++) {
        Messwerte.push(input.temperature())
        basic.pause(100)
    }
    Alarm_an = true
    while (Alarm_an) {
        music.playTone(262, music.beat(BeatFraction.Whole))
        music.playTone(349, music.beat(BeatFraction.Whole))
    }
})
```

## Schritt 4: Messwerte Anzeigen
Als nächstes Wollen wir durch das Drücken von Knopf A, alle Messwerte ausgeben. 
Hierfür benötigen wir aus der ``||Input: Eingabe||`` den Block ``||Input: Wenn Knopf A gedrückt||``. 
Als erstes sollten wir den Alarm deaktivieren indem wir den Werte der ``||Variables: Variable||`` ``||Variables: Alarm_an||`` auf ``||Logic: falsch||`` setzen.
Nun müssen wir alle Werte aus unserer Liste ``||Variables: Messwerte||`` abrufen. Für diese Aufgabe gibt es eine spezielle ``||Loops: Schleife||``, die ``||Loops: für Element Wert von list||``.
Wenn wir die Variable ``||Variables: list||`` zu ``||Variables: Messwerte||`` ändern, dann werden die Werte nacheinander abgerufen. 
In der ``||Loops: Schleife||`` zeigen wir den Inhalt (``||basic: zeige Zahl||``) der ``||Variables: Variable||`` ``||Variables: Wert||`` und anschließend ein Zeichen (``||basic: zeige Symbol||``) an, damit man die einzelnen Zahlen voneinander unterscheiden kann.


```blocks
let Alarm_an = false
let Messwerte: number[] = []
input.onButtonPressed(Button.AB, function () {
    Messwerte = []
    for (let index = 0; index < 10; index++) {
        Messwerte.push(input.temperature())
        basic.pause(100)
    }
    Alarm_an = true
    while (Alarm_an) {
        music.playTone(262, music.beat(BeatFraction.Whole))
        music.playTone(349, music.beat(BeatFraction.Whole))
    }
})
input.onButtonPressed(Button.A, function () {
    Alarm_an = false
    for (let Wert of Messwerte) {
        basic.showNumber(Wert)
        basic.showIcon(IconNames.SmallDiamond)
    }
})
```

## Schritt 5: Mittelwert anzeigen
Als letztes wollen wir noch den Mittelwert oder Durchschnitt berechnen. Hierfür müssen wir als erstes eine die Taste B ansteuern. 
Dies tun wir, indem wir aus dem Bereich ``||Input: Eingabe||`` den Block ``||Input: Wenn Knopf B gedrückt||``. 
Auch hier sollten wir den Alarm deaktivieren, indem wir die ``||Variables: Variable||`` ``||Variables: Alarm_an||`` auf ``||Logic: falsch||`` setzen.
Nun benötigen wir 2 neue ``||Variables: Variablen||``. In der einen rechnen wir alle Messwerte zusammen und die andere speichert wie viele Messwerte wir haben. 
Die ``||Variables: Variable||`` ``||Variables: Summe_aller_Messwerte||`` setzen wir auf 0 und um die ``||Variables: Variable||`` ``||Variables: Anzahl_Messwerte||`` zu speichern nutzen wir aus den Bereich ``||Array: Arrays||`` (unter ``||advanced: Fortgeschritten||``) den Block ``||Array: Array-Länge||``.
Jetzt nutzen wir wieder die ``||Loops: Schleife||`` ``||Loops: für alle Elemente von list||`` und ändern den Inhalt von ``||Variables: Summe_aller_Messwerte||`` **um** Wert.
Nach der ``||Loops: Schleife||`` zeigen wir die Zahl an (``||basic: zeige Zahl||``), die rauskommt, wenn man ``||Variables: Summe_aller_Messwerte||`` durch ``||Variables: Anzahl_Messwerte||`` teilt.
Die Rechenoperation ist im Bereich ``||math: Mathematik||`` zu finden (``||math: :||``).

```blocks
let Alarm_an = false
let Messwerte: number[] = []
let Summe_aller_Messwerte = 0
let Anzahl_Messwerte = 0
input.onButtonPressed(Button.A, function () {
    Alarm_an = false
    for (let Wert of Messwerte) {
        basic.showNumber(Wert)
        basic.showIcon(IconNames.SmallDiamond)
    }
})
input.onButtonPressed(Button.AB, function () {
    Messwerte = []
    for (let index = 0; index < 10; index++) {
        Messwerte.push(input.temperature())
        basic.pause(100)
    }
    Alarm_an = true
    while (Alarm_an) {
        music.playTone(262, music.beat(BeatFraction.Whole))
        music.playTone(349, music.beat(BeatFraction.Whole))
    }
})
input.onButtonPressed(Button.B, function () {
    Alarm_an = false
    Summe_aller_Messwerte = 0
    Anzahl_Messwerte = Messwerte.length
    for (let Wert of Messwerte) {
        Summe_aller_Messwerte += Wert
    }
    basic.showNumber(Summe_aller_Messwerte / Anzahl_Messwerte)
})
```