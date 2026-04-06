# Spielmechanik und Regeln 
*Stand: 23.03.2026*

## Teamstruktur und Rollen
Spiel besteht aus 2 Teams, jedes Team hat:
- Spymasters: Kennen alle Farben und Wörter der Karten.
- Operatives: Sehen das gleiche Spielfeld wie Spymaster, alle noch unaufgedeckten Karten zeigen jedoch eine weiße Farbe.

## Spielablauf
1. Hinweisgabe: Spymaster kommuniziert über ein spezielles UI ein einzelnes Wort, das nicht auf dem Spielfeld steht, sowie eine Zahl. Diese Zahl gibt an, wie viele Karten auf dem Board mit dem Hinweis in Verbindung stehen.
2. Raten: Die Operatives sind dran und diskutieren untereinander, welche Karten sie auswählen möchten. Sie können auf die Karten tippen, um sie zu markieren. Wenn sie die Karte ein zweites Mal anklicken, dann wird die Karte aufgedeckt.
3. Zuglimit: Die Operatives dürfen {Zahl vom Spymaster + 1} aufdecken.
4. Zugende: Der Zug endet sofort, wenn:
  - Maximale Anzahl an Versuchen erreicht
  - Weiße Karte aufgedeckt
  - Gegnerische Karte aufgedeckt
  - Schwarze Karte aufgedeckt (Gegner Team gewinnt automatisch)
6. Manueller Wechsel: Wenn ein Team mit dem Raten fertig ist und keine Karte mehr aufdecken wollen, können sie ihren Zug manuell beenden.

## Sieg- und Niederlagebedingungen
- Sieg: Ein Team gewinnt, sobald alle Karten der eigenen Teamfarbe aufgedeckt werden.
- Niederlage: Das Team, welches die schwarze Karte aufdeckt hat automatisch verloren.

## Technische Anforderungen & UI-Features
- Rollenwahl: Ein Menüsystem ermöglicht Rollenauswahl am Beginn des Spiels.
- Zugriffskontrolle: Nur das Team, das aktuell am Zug ist, haben die Berechtigung Karten auszuwählen.
- Counter: Es soll mitgezählt werden, wie viele Karten der jeweiligen Teams noch im Spiel sind.
