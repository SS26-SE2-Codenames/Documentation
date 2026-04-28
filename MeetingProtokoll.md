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

