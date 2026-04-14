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
  
