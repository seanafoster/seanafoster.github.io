# Hangman Game

This project was built in the .NET framework, using Razor pages. A user was required to login or register a new account before they could play. Passwords were hashed, salted and stored in a database, and all verification took place server-side. Once authenticated, a user could enter the hangman game and attempt to guess the word.

>![Hangman game snapshot](/docs/assets/hangman-1.png)

>![Hangman game snapshot 2](/docs/assets/hangman-2.png)

We created a websocket in order to validate the user's guess and update the UI. One particular accomplishment of mine for this group project was the creation of the playable word dictionary. Our dictionary of 50 words was stored as a JSON file, which was parsed on initialization.

```
public void LoadJson()
{
    using (StreamReader r = new("dictionary.json"))
    {
        string json = r.ReadToEnd();
        Dictionary<int, string> words = JsonConvert.DeserializeObject<Dictionary<int, string>>(json);

        _words = words;
    }
}
```

[Return](https://seanafoster.github.io/index)

[Link to repo](https://github.com/seanafoster/Hangman)