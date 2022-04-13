# Speed Game

[Return](https://seanafoster.github.io/index)

This web application was made using .NET with Razor pages. We also used SignalR to facilitate asynchronous play in multiple browsers.

>![Speed game snapshot](/docs/assets/speed-1.png)

>![Speed game in progress snapshot](/docs/assets/speed-2.png)

Utilizing a custom hub, we were able to keep both players' screen in sync.

```
public async Task SendTable(Table table)
{
    Table newTable = AddPlayers(table);
    await Clients.All.SendAsync("ReceiveUpdatedTable", newTable);
}

protected override async Task OnInitializedAsync()
{
    hubConnection = new HubConnectionBuilder()
        .WithUrl(NavigationManager.ToAbsoluteUri("/speedhub"))
        .Build();

    hubConnection.On<Table>("ReceiveUpdatedTable", (table) =>
    {
        Table = table;
        checkForWin();
        PullCards();
        StateHasChanged();
    });

    await hubConnection.StartAsync();
}