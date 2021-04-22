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