## 1. Flyway Migrations — How to Update the DB

### Current state

Flyway is enabled via `application.yaml`:

```yaml
spring:
  flyway:
    enabled: true
```

Migration scripts live in:

```
src/main/resources/db/migration/
```

We use Spring Boot's auto-configuration — Flyway runs automatically on application startup. No manual intervention needed.

### Adding a new migration

**Create a new SQL file** in `src/main/resources/db/migration/` with this naming pattern:

   ```
   V<version>__<description>.sql
   ```

   - `<version>`: Incrementing integer. 
   - Double underscore `__` between version and description.
   - `<description>`: Descriptive snake_case name, e.g. `add_chat_history_table`.

   **Example:**
   ```
   V4__add_chat_history_table.sql
   ```
**Start the app.** Flyway will detect the new migration script and apply it automatically. The `flyway_schema_history` table in the database tracks which migrations have already run.

### Important rules

- **Never modify** a migration that has already been applied. Flyway checksums each migration and will refuse to run if the checksum changes.
- If you need to fix a past migration, create a **new** migration that corrects it.
- Version numbers increase sequentially.
- If, for whatever reason a script HAS to be changed and the contents of the DB can be erased, run `docker compose down -v`. This clears the volumes, allowing the DB to accept modified scripts.

## 2. Cascading System — Snapshot & Restore

### Overview

- The app persists game state as snapshots so that games survive server restarts.
- When a lobby row is deleted, PostgreSQL automatically deletes all child rows in `player`, `game_state`, and `card`.

### Trigger points — when snapshots are saved

Snapshots are saved at key game events. The `PersistenceService.saveSnapShot(lobbyCode)` method is called:

- After a player joins or leaves a lobby
- After a clue is given
- After a card is revealed (guess)
- When the turn passes
- After a cheat is used

This ensures the database always reflects the latest game state. The database deletes the previous snapshot and stores a new one. We do not call persistence when a lobby is created as certain attributes for the DB do not exist yet. This also saves on additional DB read and writes as there is no need to save a lobby that has not started yet. 


### What happens if the server crashes mid-game?

1. In-memory state is lost.
2. On restart, `RestorationService.restoreOnContainerStart()` reads the saved snapshot from the DB.
3. The game resumes from that snapshot — at worst, the very last action might be lost (between the action and the save call), but the game itself is never fully lost.

### Key design decisions

- Lobby is the aggregate root and everything is linked to it. If the lobby entry is deleted, the deletion cascades to the other tables, deleting the respective entries
- Snapshots are full replacements not partial updates.
- ORM We use Object-Relational Mapping
