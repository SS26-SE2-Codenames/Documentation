# Network Protocol Documentation

## Overview

The backend uses two communication mechanisms:

1. HTTP/REST for lobby management and state retrieval
2. WebSocket + STOMP for real-time lobby, chat, and gameplay communication

All payloads are serialized as JSON.

---

## WebSocket Configuration

Connection endpoint:

* /ws (SockJS enabled)

Fallback endpoint:

* /ws-fallback

Application prefix:

* /app

Broker prefixes:

* /topic, /queue

Clients send messages to:

* /app/...

Clients subscribe to:

* /topic/...

---

## REST Endpoints

### Create Lobby

Request:

* GET /lobby/create?username={username}

Response:

* `{ "message": "...", "lobbyCode": "...", "playerList": [...], "isStarted": true }`

Purpose:

* Creates a lobby and returns the new lobby state.

### Join Lobby

Request:

* GET /lobby/{lobbyCode}/join?username={username}

Response:

* `{ "message": "...", "lobbyCode": "...", "playerList": [...], "isStarted": true }`

Purpose:

* Adds a player to a lobby and returns updated lobby state.

### Leave Lobby

Request:

* GET /lobby/{lobbyCode}/leave?username={username}

Response:

* `{ "message": "...", "lobbyCode": "...", "playerList": [...], "isStarted": true }`

Purpose:

* Removes a player from a lobby and returns updated lobby state.

### Get Lobby Information

Request:

* GET /lobby/{lobbyCode}

Response:

* `{ "message": "...", "lobbyCode": "...", "playerList": [...], "isStarted": true }`

Purpose:

* Retrieves current lobby state.

### Select Team / Role

Request:

* POST /lobby/{lobbyCode}/select-position

Payload:

* `{ "username": "...", "team": "RED", "role": "SPYMASTER", "isHost": true }`

Response:

* `{ "message": "...", "lobbyCode": "...", "playerList": [...], "isStarted": true }`

Purpose:

* Assigns team and role and returns updated lobby state.

### Health Endpoint (pending merge from feature/health-endpoint)

Request:

* GET /health

Response:

* `{ "status": "UP" }`

Purpose:

* Verifies backend availability.

---

## WebSocket Messages

### Join Lobby

Client to server destination:

* /app/join

Payload:

* `{ "name": "...", "code": "ABCD" }`

Broadcast:

* /topic/lobby/{code}

Error destination on failed join:

* /topic/errors/{sessionId}

Purpose:

* Registers session and broadcasts updated player usernames.

### Start Game

Client to server destination:

* /app/start-game

Broadcast:

* /topic/game/{lobbyCode}

Purpose:

* Sends first game state.

### Reveal Card

Client to server destination:

* /app/reveal-card

Payload (minimum):

* `{ "lobbyCode": "ABCD", "position": 3, "currentTurn": "RED" }`

Broadcast:

* /topic/game/{lobbyCode}

Purpose:

* Reveals a card and broadcasts updated game state.

### Submit Clue

Client to server destination:

* /app/submit-clue

Payload (minimum):

* `{ "lobbyCode": "ABCD", "currentClue": {"word" = "ANIMAL", "guessAmount":2}, "currentTurn": "BLUE" }`

Broadcast:

* /topic/game/{lobbyCode}

Purpose:

* Submits clue and broadcasts updated game state.

### Pass Turn

Client to server destination:

* /app/pass-turn

Payload (minimum):

* `{ "lobbyCode": "ABCD", "currentTurn": "RED" }`

Broadcast:

* /topic/game/{lobbyCode}

Purpose:

* Ends the turn early and broadcasts updated game state.

---

## Chat Communication

### Lobby Chat

Destination:

* /app/chat/{lobbyId}

Broadcast:

* /topic/chat/{lobbyId}

Purpose:

* Messages visible to all players.

### Team Chat

Destination:

* /app/chat/{lobbyId}/{team}

Broadcast:

* /topic/chat/{lobbyId}/{team}

Purpose:

* Messages restricted to one team.

### Operative Chat

Destination:

* /app/chat/{lobbyId}/{team}/operative

Broadcast:

* /topic/chat/{lobbyId}/{team}/operative

Purpose:

* Messages restricted to operatives.

---

## Serialization

All communication uses JSON serialization.

Example:

* `{ "team": "RED", "role": "OPERATIVE" }`

---

## Session Handling

WebSocket sessions are associated with:

- username
- lobby code

Team and role are validated via lobby state during message processing.

Invalid sessions or unauthorized chat/game actions are rejected.
