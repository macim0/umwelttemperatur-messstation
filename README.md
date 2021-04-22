# Umweltmessstation

## Schritt 1: Messwerte aufnehmen
Wir sollten als erstes den Sensor testen. Dafür wollen wir nach dem Drücken der A und B Taste (A+B), 10 Messwerte anzeigen. 
Als erstes benötigen wir aus dem Bereich ``||Input: Eingabe||`` den Block ``||Input: Wenn Knopf A gedrückt||``. Nun ändern wir noch den Knopf A auf A+B.
Anschließend wollen die Messwere Anzeigen. Da es immer wieder die gleiche Aufgabe ist, können wir eine ``||Loops: Schleife||`` nutzen z.B. ``||Loops: 4-mal wiederholen||``.
In dieser Schleif rufen wir immer wieder die Temperatur ab (``||Input: Temperatur (°C)||``) und zeigen diese an (``||basic: Zeige Zahl||``), außerdem machen wir nach jedem Durchgang eine Pause von 1 Sekunde (``||basic: pausiere (ms) 100|``).


```blocks
input.onButtonPressed(Button.AB, function () {
    for (let index = 0; index < 10; index++) {
        basic.showNumber(input.temperature())
        basic.pause(1000)
    }
})
```



## Blockvorschau

Dieses Bild zeigt den Blockcode vom letzten Commit im Master an.
Die Aktualisierung dieses Bildes kann einige Minuten dauern.

![Eine gerenderte Ansicht der Blöcke](https://github.com/macim0/umwelttemperatur-messstation/raw/master/.github/makecode/blocks.png)

#### Metadaten (verwendet für Suche, Rendering)

* for PXT/calliopemini
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
