# Number Guessing Game

[Return](https://seanafoster.github.io/index)

The bulk of this application was done in PHP, and was fully deployed as a web application. The user was first presented with a login/register screen with password validation, using SHA256 hashing with a salt for security. Passwords were verified server-side, using a connection secured with an SSL certificate. 

```
if ($result->num_rows > 0) {
    $row = $result->fetch_assoc();

    $db_username = $row["Username"];
    $db_passwordHash = $row["PasswordHash"];
    $db_salt = $row["Salt"];
}

$conn->close();

$passwordHash = hash("sha256", $userPassword) . $db_salt;
```
<br>

After logging in or registering a new account, and user would be presented with a screen to make a guess between 1 and 100. Based on their input, the application would determine if their guess was too high, too low, or correct.

>![Guessing game snapshot](/docs/assets/guessing-game-1.png)

<br>

When a user made a correct guess, they would be taken to a win screen. Scores were calculated by how many guesses it took to get to the correct number.

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
```

[Return](https://seanafoster.github.io/index)

[Link to repo](https://github.com/seanafoster/number-guessing-game)