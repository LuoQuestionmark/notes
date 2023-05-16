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
