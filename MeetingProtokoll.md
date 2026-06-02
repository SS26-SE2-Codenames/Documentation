# Projekt Meeting Protokoll

## 23.03.2026
- Codenames gespielt, um die Spielmechanik zu analysieren.
- Spielablauf dokumentiert.
- Allgemeines Brainstorming für Tickets.
- Tickets erstellt.
  - Ticketeinteilung soll im nächsten Meeting erfolgen.

## 25.03.2026
- Verteilung der Rollen und Tasks/ Tickets an die Teammitglieder.
- Neue Tickets erstellt.

## 27.03.2026
- Kurze Besprechung eines potentiellen Spielmodus von Emre.
- Einigung auf den Google Java Style Guide für das Backend.

## 06.04.2026 - Stand Up Meeting
- Technische Themen:
  - Besprechung der implementierten Systemarchitektur und des Design.
  - Kurze Vorstellung des Codes durch alle Teammitglieder.
  - Client Server Kommunikation:
    - Join/ Leave soll über REST API erfolgen.
    - Spiel Kommunikation: Text-WebSockets.
- Neue Aufgabenverteilung:
  - Alexander: Weiterführung Frontend (UI, Screen, Buttons, Navigation)
  - Selina: Weiterführung Frontend (UI, Screen, Buttons, Navigation)
  - Natasa: Android-Netzwerkverbindung (Frontend-Integration)
  - Sofia: Fertigstellen des Turn-Systems, Implementierung des Game-Loops
  - Emre: Fertigstellen der Spielvorbereitung
  - Christopher: Backend Chat Funktionalität für Spieler ("synchronized" für Methoden einführen, standard getter -> Lombok getter)
  - Anna: Implementierung der Frontend Lobby
- Pläne für die kommende Sprints:
  - Sprint 2: Fertigstellen des Spiels, eventuell Implementierung kleinerer Features.
  - Sprint 3: Polishing, Bug-Fixing, eventuell Integration von Audio/ Musik.

## 14.04.2026 - Stand Up Meeting
- Technische Themen:
  - Besprechung der implementierten branches: UI, Lobby(Frontend, Backend), Refactoring vom Server auf STOMP, Gamelogic(clue management, turn system, roles)
  - Kurze Vorstellung des Codes durch alle Teammitglieder.
  - Neue tickets bezüglich UI und neue Features für Sprint 2 und 3.
- Neue Aufgabenverteilung:
  - Alexander: Weiterführung Frontend (UI, Screen, Buttons, Navigation)
  - Selina: Weiterführung Frontend (UI, Screen, Buttons, Navigation)
  - Natasa: Fertigstellen STOMP Implementierung, Android Client
  - Anna: Fertigstellen Lobby Frontend
  - Sofia: Fertigstellen des Turn-Systems, Implementierung des Game-Loops
  - Emre: Implementierung der Rollen (#39) oder Implementierung des Game-Loops (Eventuell Mocking des Turn-Systems)
  - Christopher: Chat tests + Integration mit Server
  
## 22.04.2026 - Stand Up Meeting & Sprint Planung
- Technische Themen & Code-Qualität:
  - Einhaltung des Google Java Style im Backend.
  - Implementierung von ktlint im Frontend für automatisierte Code-Formatierung. (Command um das zu automatisieren im README.md)
  - Klärung des Merge-Prozesses in den `development` Branch. Deadline: 22.04.
  - Kommunikation soll in der Zukunft besser werden, besonders wenn Komponenten voneinander abhängen. Kommunikation muss im Sprint 2 verstärkt werden, um Integrationen der Komponenten zu erleichtern.
  - Tickets müssen genauer und konkreter werden. 
  - Einführung neuer Epics für Sprint 2.
- Neue Aufgabenverteilung & Organisation:
  - Anna übernimmt die Button-Implementierung für die Live Demo am 23.04. Button soll zeigen, dass  Kommunikation zwischen Server und Client möglich ist. 
- Aufteilung der Präsentation 23.04
  - Natasa: Sprint Überblick + Kanbanboard, Tickets, Fortschritt, etc.
  - Alexander: UI Demo + Journey Map
  - Anna: SonarQube
  - Anna-Christopher: Priorisierung von Tickets/ Tasks + Aktuellen Zustand vom Spiel (Unfertiges transparent machen) + Next Steps  für Sprint 2
  - Selina: Arbeitsverteilung, GitHub Statistics
- Sprint 2 Planung:
  - Alte Tickets aus Sprint 1 nachholen.
  - Neue Epics: Erweiterung des Frontends, Fertigstellung des Backends, Integration Frontend + Backend.
  - Fokus auf das Frontend bzw. die Integrations.
 
## 28.04.2026 - Finalisierung der Sprint Planung
- Fixe Tickets definiert.
- Besprechung über upcoming Tasks bis
  - Anna: Remaining Issues aus Sprint 1 beheben
  - Christopher Natasa: Refactoring Codebase aus Sprint 1 für sauberen Start ins 2. Sprint
  - Alexander Selina: Start mit Sprint 2 Tickets
  - Emre Sophia: Offene PRs erledigen 

## 11.05.2026 - Stand Up Meeting 
- Besprechung der fertigen Tickets
- Restlichen Aufgaben eingeteilt:
  - Alexander: Weiterführung Frontend (UI, Screen, Buttons, Navigation)
  - Selina: Weiterführung Frontend (UI Chat)
  - Natasa: Netzwerkendpoints festlegen
  - Sofia: Fertigstellung des Turn-Systems bis 12.05.2026 18:00
  - Emre: Game-Loop
  - Christopher: Clue Integration im Frontend
  - Anna: Card flipping Integration im Frontend

## 16.05.2026 - Stand Up Meeting 
- Besprechung der fertigen Tickets
- Besprechen der noch zu erledigenden Tickets
  - Game Loop kann elegant gelöst werden in dem man Gamephase im GameStateDTO einfügt, Frontend muss den GameState auslesen und winner, currentTeam, gamePhase auslesen und UI updaten
  - Lobby und Netzwerk relevanten Issues sind fast komplett erledigt
  - Chat im Frontend braucht ein Fix.
- Restlichen Aufgaben eingeteilt:
  - Alexander: Game Zustand im Frontend fertig stellen + Game over screen (simpel halten)
  - Selina: Chat UI im Frontend fertigstellen
  - Natasa: Endpoints, GameRecovery
  - Sofia: Turn system wurde nicht erstellt, Spielprotokoll Feature weiter machen 
  - Emre: Schummelfunktion überlegen, konkrete Tickets erstellen
  - Christopher: GameStateDTO für Frontend erweitern, evtl. Clue Integration im Frontend
  - Anna: Lobby und Game Mechanics im Frontend

## 19.05.2026 - Stand Up Meeting 
- Besprechung der fertigen Tickets
- Besprechen der noch zu erledigenden Tickets
- Tickets und EPICS für Sprint 3 festgelegt.
  - Refactoring/ Maintenance tasks, Netzwerk, DB, Schummelfunktion, etc..

## 22.05.2026 - Meeting 
- Besprechung was das Ziel für die Nächste Woche ist
- Einteilung von den ersten Tasks: refactoring frontend backend, docker
- T-Shirt sizes für die Tickets

## 02.06.2026 - Stand Up Meeting 
- Besprechung der fertigen Tickets
- Besprechen der noch zu erledigenden Tickets
- DB Schema hergezeigt und diskutiert
- Einteilung der offenen Tickets
  - Fokus auf Backend anstatt UI
- Sprint 3 Requirements genauer analysiert
  - Potentielle Fragen überlegt für Product Owner
  - Ziel: Diese Woche eine Liste an implemented features von allen Mitgliedern kompilieren + Fragen konkretisieren und als Email senden




