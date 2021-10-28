# Shared endpoints
These endpoints will be shared between all games supported by the client. Therefore, **the payloads of these endpoints have to be implemented regardless of the games.**

## **GET `/player`**
Get player's data and currently owned tips. Since it's a GET request, the player's display name in the database may be outdated.
* Request format: `/player/<playerID>`
* Responses:
    * HTTP 200 OK - [PlayerWithTips](https://github.com/AllBurst/burstSpecs/tree/main/English/shared#playerwithtips)
    * HTTP 404 Not Found - The specified player hasn't joined the server yet.
    * HTTP 500 Internal Server Error - An unknown error happened.

## **POST `/player`**
Get player to join the server, that is, enable player to start or join Poker games.
* Request format:
```json
{
    "player_id": "1234567890",
    "avatar_url": "https://awesome-website.com/abc.png",
    "name": "John Doe"
}
```
* Responses:
    * HTTP 201 Created - [PlayerWithTips](https://github.com/AllBurst/burstSpecs/tree/main/English/shared#playerwithtips)
    * HTTP 400 Bad Request - A player with the same player ID has already joined the server.

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