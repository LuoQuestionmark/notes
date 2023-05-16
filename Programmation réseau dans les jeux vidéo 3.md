# Programmation réseau dans les jeux vidéo 3

## Travel in game

```c++
UWorld::ServerTravel
APlayerController::ClientTravel
```

ServerTravel:

- Seamless
- Non-seamless

## `GameMode`

n'utilise pas `GameModeBase`, utilise `GameMode`.

```h++
protected:
    UPROPERTY(EditAnywhere, Category = ...)
    int NumberOfPlayer = 4;
    
    UPROPERTY(EditAnywhere, Category = ...)
    FString LevelToLoad;

public:
    APLobbyGameMode() {
        bUseSeamlessTravel = !GIsEditor;
        // var start with G is global magic
        // Seamless doesn't work with the editor
    }    
```

```c++
void APLobbyGameMode::OnPostLogin(AController* NewPlayer) {
    Super::OnPostLogin(NewPlayer);
    
    if (GameSate->PlayerArray.Num() >= NumberOfPlayer) {
        GetWorld()->ServerTravel(LevelToLoad.Append("?listen"));
    }
}

```

In game mode blueprint, start the level path (`LevelToLoad`) by the `Game` repo.

## Timer

Timer is a `GameState`, but it is not controlled by player, thus we need a `PlayerController`.

```c++
class APBasePlayerController {
protected:
    UFUNCTION(Server, Reliable)
    void ServerRequestTime(APlayerController* Requester, float RequestTime);

    UFUNCTION(Client, Reliable, WithValidation)
    void ClientRequestTime(float RequestTime, float ServerTime);
}

void APBasePlayerController::ServerRequestTime_Implementation(...) {
    return (...).getWorldTime(...);
}

bool APBasePlayerController::ServerRequestTime_Validate(...) {
}

void APBasePlayerController::ClientReportTime(float RequestTime, float ServerTimeResponse) {
    float RTT = GetWorld()->GetTimeSeconds() - RequestTime;
    // the default function is slow
}

void APBasePlayerController::ReceivedPlayer() {
    Super::ReceivedPlayer();

    if (IsLocalController()) {
        ServerRequestTime(this, GetWorld()->getTimeSeconds());

        GetWorld()->GetTimerManager().SetTimer(UpdateServerHandle, ...);
        // need to add a timer (UE), too
    }
}
```

```c++
void APBaseGameState::APBaseGameState()
{
    PrimaryActorTick.bCanEverTick = false;
}

double APBaseGameState::GetSererWorldTimeSeconds() const {
    if (HasAuthority()) {
        return GetWorld()->GetTimeSeconds();
    }

    else {
        auto *MyPC = Cast<PBasePlayerController>(GetGameInstance()->Get(...))
    }

    if (MyPC == nullptr) {
        return Super::GetServerWorldTimeSeconds();
    }

    return MyPC->ServerTime;
}
```

### steps

- At $t=0$, player ask the time from the server, calculate RTT, latency ; therefore the correct time on server.
- (default `Request/Response` impl is bad, reimplement customized `PlayerController`)
- `Request/Response` dans `PlayerController`
- ReceivedPlayer: 1st request, setup timer
- Tick: client update the server time (pseudo)

### public Server time

override `GetServerTimeSeconds` dans le game state

si on est serveur, `World::GetTimeInSec`

si on est client, `PlayerController` custom `ServerTime`
