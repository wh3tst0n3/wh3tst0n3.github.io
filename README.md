# wh3tst0n3.github.io

## [UnrealPages](UnrealPages/Index.md)

- Notes on Unreal Engine 5.7 and C++
- Focus areas include:
  - Best practices for C++ and Blueprint
  - Gameplay Ability System (GAS)
  - Data-Driven Gameplay

So it turns out there's a little bug with Unreal GAS that messes with (the validity of) the player controller. Best practice is to add

```cpp

// Character.h

virtual void PossessedBy(AController* NewController) override;
virtual void UnPossessed();

// Character.cpp

void AGASCharacter::PossessedBy(AController* NewController) override
{
    Super::PossessedBy(NewController);
    // other logic here
    ASC->RefreshAbilityActorInfo();
}

void AGASCharacter::UnPossessed()
{
    ASC->RefreshAbilityActorInfo();
}


```

And quite possibly

``` cpp

// AssetManager.cpp

#include "AbilitySystemGlobals.h"

void UMyAssetManager::StartInitialLoading()
{
    Super::StartInitialLoading();

    UAbilitySystemGlobals::Get().InitGlobalData();
}

