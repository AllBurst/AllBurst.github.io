# Shared endpoints
These endpoints will be shared between all games supported by the client. Therefore, **the payloads of these endpoints have to be implemented regardless of the games.**

## **GET `/player`**
Get player's data and currently owned tips. Since it's a GET request, the player's display name in the database may be outdated.
* Request format: `/player/<playerID>`
* Responses:
    * HTTP 200 OK - [PlayerWithTips](https://github.com/AllBurst/burstSpecs/tree/main/English/shared#playerwithtips)
    * HTTP 404 Not Found - The specified player hasn't joined the server yet.
    * HTTP 500 Internal Server Error - An unknown error happened.

## **GET `/player/<playerID>/daily`**
Get player's daily rewards. Player's display name is **NOT** updated.
* Request format: `/player/<playerID>/daily`
* Responses:
    * HTTP 200 OK - [Tip](https://github.com/AllBurst/burstSpecs/tree/main/English/shared#tip) with updated tips.
    * HTTP 204 No Content - The daily reward has been granted in the last 24 hours.

## **GET `/player/<playerID>/weekly`**
Get player's weekly rewards. Player's display name is **NOT** updated.
* Request format: `/player/<playerID>/weekly`
* Responses:
    * HTTP 200 OK - [Tip](https://github.com/AllBurst/burstSpecs/tree/main/English/shared#tip) with updated tips.
    * HTTP 204 No Content - The daily reward has been granted in the last 24 hours.