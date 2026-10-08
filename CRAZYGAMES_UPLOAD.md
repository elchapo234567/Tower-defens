# CrazyGames-Veröffentlichung

## Fertiger Upload

Die Datei `release/mega-tower-defense-crazygames.zip` ist das fertige HTML5-Spielpaket. `index.html` liegt direkt im Stamm des ZIP-Archivs. Das Spiel lädt das offizielle CrazyGames HTML5 SDK v3 und verwendet ausschließlich dessen Rewarded-Ad-Schnittstelle.

## Im CrazyGames-Portal

1. Auf [developer.crazygames.com](https://developer.crazygames.com/) anmelden und ein neues Spiel anlegen.
2. Als Plattform beziehungsweise Engine **HTML5** auswählen.
3. `release/mega-tower-defense-crazygames.zip` als Spiel-Build hochladen.
4. Titel, Beschreibung, Steuerung, Kategorien sowie die im Portal verlangten Cover- und Vorschaubilder ergänzen.
5. Den privaten Preview-/Sandbox-Link öffnen und diese Abläufe prüfen:
   - **GET GEMS**: eine vollständig beendete Werbung vergibt genau 5 Gems.
   - Abgebrochene oder fehlgeschlagene Werbung vergibt nichts.
   - **Shop → Gratis-Turm**: jede beendete Werbung erhöht den Zähler genau einmal; bei 5/5 kann ein noch gesperrter Turm gewählt werden.
   - Mission starten, pausieren, verlieren und gewinnen.
   - Seite neu laden und prüfen, ob Fortschritt erhalten bleibt.
6. Nach dem Preview-Test den Build im Portal zur Prüfung einreichen.

Rewarded Ads funktionieren absichtlich nur innerhalb der CrazyGames-Umgebung. Auf GitHub Pages oder beim direkten lokalen Öffnen bleibt die Werbeschaltfläche deaktiviert. Für Tests echter Anzeigen immer die CrazyGames-Vorschau verwenden.

## Angaben für die Spielseite

**Steuerung**

- Linksklick: Menüs, Türme platzieren und Upgrades kaufen
- Rechtsklick oder Escape: Platzierung abbrechen
- Tasten 1–5: Turm aus dem Arsenal wählen
- Leertaste: Spieltempo wechseln

**Fortschritt**

Gems, Missionen, Türme, Slots und der Gratis-Turm-Werbezähler werden im Browser gespeichert. Ein neuer Spieler beginnt mit 0 Gems, 0 abgeschlossenen Missionen, 0/5 Gratis-Turm-Werbungen und den fünf Starttürmen.

## Technische Werberegeln

- Eine Anzeige startet nur nach einem bewussten Klick des Spielers.
- Eine Belohnung wird nur im `adFinished`-Callback vergeben.
- `adError` und abgebrochene Anzeigen vergeben keine Belohnung und verbrauchen keinen Fortschritt.
- Während eine Anzeige läuft, sind weitere Eingaben gesperrt.
- Das Spiel meldet Laden, Spielstart und Spielende über das CrazyGames SDK.

Offizielle Referenz: [CrazyGames HTML5 SDK – Advertisement](https://docs.crazygames.com/sdk/html5/advertisement/)
