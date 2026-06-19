# Network Protocol Documentation  
  
## Overview  
  
The backend uses two communication mechanisms:  
  
1. HTTP/REST for lobby management, health checks, and initial lobby/game actions.  
2. WebSocket + STOMP for real-time lobby, chat, gameplay, and cheat communication.  
  
All payloads are serialized as JSON.  
  
---  
  
## WebSocket Configuration  
  
Connection endpoint:  
  
- `/ws-fallback`  
  
Application prefix:  
  
- `/app`  
  
Broker prefixes:  
  
- `/topic`  
- `/queue`  
  
Client-specific queue prefix:  
  
- `/user/queue`  
  
Clients send messages to:  
  
- `/app/...`  
  
Clients subscribe to:  
  
- `/topic/...`  
- `/user/queue/...`  
  
Note: The backend currently registers `/ws-fallback` as the STOMP endpoint. `/ws` is not registered in the current cheat-validation backend branch.  
  
---  
  
## REST Endpoints  
  
### Create Lobby  
  
Request:  
  
- `GET /lobby/create?username={username}`  
  
Response:  
  
```json  
{  
  "message": "Successfully created Lobby.",  "lobbyCode": "ABCD",  "playerList": [    {      "username": "Alice",      "team": null,      "role": null,      "isHost": true    }  ],  "isStarted": false}  
```  
  
Purpose:  
  
- Creates a lobby and returns the new lobby state.  
  
### Join Lobby  
  
Request:  
  
- `GET /lobby/{lobbyCode}/join?username={username}`  
  
Response:  
  
```json  
{  
  "message": "Joined Lobby successfully.",  "lobbyCode": "ABCD",  "playerList": [],  "isStarted": false}  
```  
  
Purpose:  
  
- Adds a player to a lobby and returns the updated lobby state.  
  
### Leave Lobby  
  
Request:  
  
- `GET /lobby/{lobbyCode}/leave?username={username}`  
  
Response:  
  
```json  
{  
  "message": "Left lobby successfully.",  "lobbyCode": "ABCD",  "playerList": [],  "isStarted": false}  
```  
  
Purpose:  
  
- Removes a player from a lobby and returns the updated lobby state.  
  
### Get Lobby Information  
  
Request:  
  
- `GET /lobby/{lobbyCode}`  
  
Response:  
  
```json  
{  
  "message": "Lobby info retrieved successfully.",  "lobbyCode": "ABCD",  "playerList": [],  "isStarted": false}  
```  
  
Purpose:  
  
- Retrieves the current lobby state.  
  
### Select Team / Role  
  
Request:  
  
- `POST /lobby/{lobbyCode}/select-position`  
  
Payload:  
  
```json  
{  
  "username": "Alice",  "team": "RED",  "role": "SPYMASTER",  "isHost": true}  
```  
  
Response:  
  
```json  
{  
  "message": "Position selected successfully.",  "lobbyCode": "ABCD",  "playerList": [],  "isStarted": false}  
```  
  
Purpose:  
  
- Assigns team and role and returns the updated lobby state.  
  
### Start Game  
  
Request:  
  
- `GET /lobby/{lobbyCode}/start-game?username={username}`  
  
Response:  
  
```json  
{  
  "message": "Game is starting now.",  "lobbyCode": "ABCD",  "playerList": [],  "isStarted": true}  
```  
  
Purpose:  
  
- Marks the lobby as started. This is the final REST action before the game state is requested over WebSocket.  
  
### Health Endpoint  
  
Request:  
  
- `GET /health`  
  
Response:  
  
```json  
{  
  "status": "UP"}  
```  
  
Purpose:  
  
- Verifies backend availability.  
  
---  
  
## WebSocket Messages  
  
### Join Lobby / Reconnect  
  
Client to server destination:  
  
- `/app/join`  
  
Payload:  
  
```json  
{  
  "name": "Alice",  "code": "ABCD"}  
```  
  
Broadcasts:  
  
- `/topic/lobby/{code}` with updated player usernames.  
- `/topic/game/{code}` with current game state.  
  
Error destination on failed join:  
  
- `/topic/errors/{sessionId}`  
  
Purpose:  
  
- Registers the WebSocket session with username and lobby code, then broadcasts lobby/game updates.  
  
### Start Game State Broadcast  
  
Client to server destination:  
  
- `/app/start-game`  
  
Payload:  
  
```json  
{  
  "lobbyCode": "ABCD"}  
```  
  
Broadcast:  
  
- `/topic/game/{lobbyCode}`  
  
Purpose:  
  
- Sends the current game state to subscribed players.  
  
### Reveal Card  
  
Client to server destination:  
  
- `/app/reveal-card`  
  
Payload:  
  
```json  
{  
  "lobbyCode": "ABCD",  "position": 3,  "currentTurn": "RED"}  
```  
  
Broadcast:  
  
- `/topic/game/{lobbyCode}`  
  
Purpose:  
  
- Reveals a card, persists a snapshot, and broadcasts the updated game state.  
  
### Submit Clue  
  
Client to server destination:  
  
- `/app/submit-clue`  
  
Payload:  
  
```json  
{  
  "lobbyCode": "ABCD",  "word": "ANIMAL",  "guessAmount": 2,  "currentTurn": "BLUE"}  
```  
  
Broadcast:  
  
- `/topic/game/{lobbyCode}`  
  
Purpose:  
  
- Submits a clue, persists a snapshot, and broadcasts the updated game state.  
  
### Pass Turn  
  
Client to server destination:  
  
- `/app/pass-turn`  
  
Payload:  
  
```json  
{  
  "lobbyCode": "ABCD",  "currentTurn": "RED"}  
```  
  
Broadcast:  
  
- `/topic/game/{lobbyCode}`  
  
Purpose:  
  
- Ends the turn early, persists a snapshot, and broadcasts the updated game state.  
  
### Use Cheat  
  
Client to server destination:  
  
- `/app/cheat`  
  
Payload:  
  
```json  
{  
  "lobbyCode": "ABCD",  "username": "Alice",  "positions": [0, 1]}  
```  
  
Private response destination:  
  
- `/user/queue/system`  
  
Private response payload:  
  
```json  
{  
  "senderUsername": "System",  "content": "Cheat result message",  "type": "SYSTEM"}  
```  
  
Purpose:  
  
- Checks selected card positions for the requesting player/team and returns the result only to that user.  
- The backend persists a snapshot after a valid cheat result.  
- Invalid cheat requests do not broadcast a response.  
  
---  
  
## Game State Broadcast Payload  
  
Broadcast destination:  
  
- `/topic/game/{lobbyCode}`  
  
Payload:  
  
```json  
{  
  "winner": null,  "currentTurn": "RED",  "currentPhase": "SPYMASTER",  "currentClue": {    "word": "ANIMAL",    "guessAmount": 2  },  "remainingGuesses": 2,  "cardList": [    {      "word": "CAT",      "color": "RED",      "isGuessed": false    }  ],  "redTeamCheatUsed": false,  "blueTeamCheatUsed": false}  
```  
  
Field notes:  
  
- `winner` is `RED`, `BLUE`, or `null`.  
- `currentTurn` is `RED` or `BLUE`.  
- `currentPhase` is `SPYMASTER` or `OPERATIVE`.  
- `currentClue` is `null` when no clue is active.  
- `cardList` contains the board cards.  
- `redTeamCheatUsed` and `blueTeamCheatUsed` indicate whether each team has already used its cheat.  
  
---  
  
## Chat Communication  
  
All chat messages use this payload:  
  
```json  
{  
  "senderUsername": "Alice",  "content": "Hello team!",  "type": "CHAT"}  
```  
  
The backend verifies and overwrites the message type for user-sent chat messages as `CHAT`.  
  
### Lobby Chat  
  
Client to server destination:  
  
- `/app/chat/{lobbyId}`  
  
Broadcast:  
  
- `/topic/chat/{lobbyId}`  
  
Purpose:  
  
- Sends messages visible to all players in the lobby.  
  
### Team Chat  
  
Client to server destination:  
  
- `/app/chat/{lobbyId}/{team}`  
  
Broadcast:  
  
- `/topic/chat/{lobbyId}/{team}`  
  
Purpose:  
  
- Sends messages restricted to one team.  
- The sender must belong to the destination team.  
  
### Operative Chat  
  
Client to server destination:  
  
- `/app/chat/{lobbyId}/{team}/operative`  
  
Broadcast:  
  
- `/topic/chat/{lobbyId}/{team}/operative`  
  
Purpose:  
  
- Sends messages restricted to operatives of one team.  
- The sender must belong to the destination team and have role `OPERATIVE`.  
  
---  
  
## Serialization  
  
All communication uses JSON serialization.  
  
Enums are serialized as uppercase names:  
  
- `Team`: `RED`, `BLUE`  
- `Role`: `SPYMASTER`, `OPERATIVE`  
- `ChatMessageType`: `CHAT`, `SYSTEM`  
  
Example:  
  
```json  
{  
  "team": "RED",  "role": "OPERATIVE"}  
```  
  
---  
  
## Session Handling  
  
WebSocket sessions are associated with:  
  
- username  
- lobby code  
  
Team and role are validated via lobby state during message processing.  
  
Invalid sessions or unauthorized chat/game actions are rejected or ignored depending on the endpoint.
