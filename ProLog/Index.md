# ProLog

## 11 March 2026

- Added some formatting and scope to the page. Current focus is Unreal 5.7 and building a customized reusable GAS template that serves as a starting point for my projects. 
- Migrated ARPG from 4.27.2 to 5.7.4 and added Custom Template to the project menu. Details need to be ironed out and template settings aren't quite configured properly. For now, your nre project must be title "ActionRPG" for the template to work correctly.

## 12 March 2026

- Updated Dovr to switch between First and Third person cams. It's kinda wonky but it's mostly pretty good. Added a flipflop to disable/enable input on ability activation. Starting a new Unity prototype.

## 13 March 2026

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
    ASC->RefershAbilityActorInfo();
}

void AGASCharacter::UnPossessed()
{
    ASC->RefershAbilityActorInfo();
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



```

