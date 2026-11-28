### Endpoint for fetching the user's portfolio
A user wants to fetch the state of his/hers holdings

GET request

1. Through the redis Pub/Sub we should fetch the curent value of his positions and calculate the amount of each one.
2. We should probably display all company prices as well + dividends

TODO: write out the format of the response

---
### Endpoint for fetching the dividends 
(probably paged 100-200 items per page)
The user wants to see an aggregation of all of its dividends and history of them; when we scrolls down we should automatically load the next page/cursor


---
### Endpoint for aggregation of the user's dividends

In order to displ