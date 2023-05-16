# Programmation réseau dans les jeux vidéo 2

## Components

```txt
AGameMode
	Règles de jeu
	Server only # client return null
	e.g. N players
```

```txt
AGameState
	Données de la game
	Autorité serveur
	Repliqué client
	e.g. team score
```

```txt
APlayerState
	Données d'un player
	Autorité serveur
	Repliqué clients
	e.g. K/D
```

```txt
APlayerController
	Contrôle un player
	Autorité serveur
	Repliqué sur le owning client
	e.g. Life
```

```txt
APawn / ACharacter
	Représentation Player
	Autorité serveur
	Repliqué aux clients
	e.g. Mesh
```

```
AHud
```

## Structure

- Dedicate server
- Listen server 服务器为客户之一

### RPC Remote Procedure Call 回调

- Server
  - `Owning Client -> Server`
  - Server / Drop
- Client
  - `Server -> Owning Client`
  - Owning Client / Server
- Multicast
  - `Server -> All Clients`
  - Server + Clients

#### Reliability

- Reliable
- Unreliable

#### Validation

if the parameters are correct. anti-cheat. etc.

### Replication

Varaibles classes herite d'`Actor`

Type Variable : `NetSerializable`

```c++
UPROPERTY(Replicated) // 服务器修改自动扩散
```

```c++
GetLifetimeReplicatedProps // 应当被重载（？）
bReplicates = true;
```

```c++
OnRepNotify() {} // 修改后自动执行
UPROPERTY(ReplicatedUsing = FUNCTION) // Don't execute on server
```

### Ownership

Server own TOUT, sauf :

- `Pawn`
- `PlayerController`

```txt
Actor
	Collider
Component
Line Sweep
Interface
Customisation BP
```

----

## Plugin

Add `C++` plugin. Plngin should be put in a `git`, then there is a plugin insert it into Unreal.

`InteractFramework`

File named `*.Build.cs` can add dependencies:

```csharp
PublicDependcyModuleNames.AddRange(
	new String[] {
		"Core",
		"AIModule",
		// dependcies
	}
);
```

```c++
class SomeClass: public OtherClass
{
	void SomeClass::StartupModule() {}
	void SomeClass::ShutdownModule() {}
	// 不要乱动……
}
```

```c++
UINTERFACE()
class UIFInterface: public UInterface {
	GENERATED_BODY()
}; // no touche pas

class INTERACTFRAMEWORK_API IIFInteractable : public AActor : public Interactable
{
    GENERATED_BODY()
    public:
    virtual void Interact(AActor* Interactor) = 0;
    
    UPROPERTY(EditAnywhere, Blueprintxxx)
    class Trigger* XXX;
}

AIFInteractibleActor::AIFInteractibleActor() {
    PrimaryActorTick.bCanEverTick = false;
    
    Trigger = CreateDefaultSubobject<USphereComponent>(TEXT("Trigger"));
    RootComponent = Trigger;
    Trigger->SetCollisionProfileName(TEXT("Trigger"));
    Trigger->SetGenerateOverlapEvents(true);
}

void AIFInteractiableActor::BeginPlay() {
    Super::BeginPlay();
    Trigger->OnComponenetOverlap.AddDynamic(this, ...)
}

void AIFInteractiableActor::HandleOverlapEvent(...) {
    if (OtherActor == nullptr) return;
    auto* xxx = Cast<UIFInteractiableActor>(Src::OtherActor->SetComponent...);
}
```

```c++
UFUNCTION(Blueprintxxx) // create an event in blueprint
BP_Interact(Interactor);
```

```c++
void UIFInteractorComponent::Interact()
{
	if (!GetOwner()->HasAuthority()) {
		Server_Interact();
		return;
	}
	XXX();
}
```

