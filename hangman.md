# Hangman Game

This project was built in the .NET framework, using Razor pages.

![Guessing game snapshot](/docs/assets/hangman-1.png)

![Guessing game win screen snapshot](/docs/assets/hangman-2.png)

We created a websocket in order to validate the user's guess server-side, and stored a dictionary of playable words in a JSON file.

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