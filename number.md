# Number Guessing Game

[Return](https://seanafoster.github.io/index)

The bulk of this application was done in PHP, and was fully deployed as a web application.

>![Guessing game snapshot](/docs/assets/guessing-game-1.png)

>![Guessing game win screen snapshot](/docs/assets/guessing-game-2.png)

The win screen pulled the top 10 scores from a database, and pointed out if the user made the list.

```
if ($result->num_rows > 0) {
    $scoreId = 1;

    while ($row = $result->fetch_assoc()) {
    echo $scoreId . ":   Player - " . $row["Username"] . " | Score - " . $row["Score"];
    if ($row["Id"] == $_SESSION["gameId"]) {
        echo "  <-- That's you!";
    }
    echo "<br>";
    $scoreId = $scoreId + 1;
    }
} else {
    echo "Got no results.";
}
