# Shared endpoints
These endpoints will be shared between all games supported by the client. Therefore, **the payloads of these endpoints have to be implemented regardless of the games.**

## **POST `/oauth/login`**
Used to get player's data and currently owned tips.
* Request format: `/oauth/login?state=<stateID>`
* Responses:
    * HTTP 200 Ok - [PlayerWithTips](https://github.com/AllBurst/burstSpecs/tree/main/English/shared#playerwithtips)
    * HTTP 400 Bad Request - Missing state in the query string.
    * HTTP 400 Bad Request - The specified state doesn't exist.
    * HTTP 404 Not Found - The specified player hasn't joined the server yet.
    * HTTP 500 Internal Server Error - An unknown error happened.

## **GET `/player/<playerID>/daily`**
Get player's daily rewards. Player's display name is **NOT** updated.
* Request format: `/player/<playerID>/daily`
* Responses:
    * HTTP 200 OK - [RewardResponse](https://github.com/AllBurst/burstSpecs/tree/main/English/shared#rewardresponse) with player's current tip data and whether the collection is successful (`Success` or `Failed`).
    * HTTP 404 Not Found - Player doesn't exist in the database, i.e. player hasn't joined the server yet.
    * HTTP 500 Internal Server Error - As its name implies. Detail messages can be found in the logs.

## **GET `/player/<playerID>/weekly`**
Get player's weekly rewards. Player's display name is **NOT** updated.
* Request format: `/player/<playerID>/weekly`
* Responses:
    * HTTP 200 OK - [RewardResponse](https://github.com/AllBurst/burstSpecs/tree/main/English/shared#rewardresponse) with player's current tip data and whether the collection is successful (`Success` or `Failed`).
    * HTTP 404 Not Found - Player doesn't exist in the database, i.e. player hasn't joined the server yet.
    * HTTP 500 Internal Server Error - As its name implies. Detail messages can be found in the logs.

## **POST `/black_jack/join`**
Request to be enrolled to the waiting list, or try to start a game immediately by pinging other players (Discord only).
* Request format:
```json
{
    "client_type": "Unity",
    "player_ids": [1234567890, 987654321]
}
```
* Responses:
    * HTTP 200 OK - **(Discord only)** Players are authenticated and the bot is responsible for collecting reactions from players.
    ```json
    {
        "type": "Start",
        "player_ids": [1234567890, 987654321]
    }
    ```
    * HTTP 200 OK - Player has been successfully enrolled to the waiting list, waiting other players to join. **The client (both Discord and Unity) is responsible for opening a WebSocket connection to listen for new games available.**
    ```json
    {
        "type": "Waiting",
        "socket_identifier": "781f7ad7-0d5e-4053-a4f8-6778aa73ca30",
        "player_ids": [1234567890]
    }
    ```
    * HTTP 201 Created - There are enough players in the waiting list, so a game is successfully created.
    ```json
    {
        "type": "Matched",
        "game_id": "781f7ad7-0d5e-4053-a4f8-6778aa73ca30",
        "player_ids": [1234567890, 987654321]
    }
    ```
    * HTTP 400 Bad Request - At least one of the players mentioned is already in the waiting list.
    * HTTP 404 Not Found - At least one of the players mentioned hasn't joined the server yet.
    * HTTP 500 Internal Server Error - As its name implies. Detail messages can be found in the logs.