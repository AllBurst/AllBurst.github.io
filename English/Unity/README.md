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