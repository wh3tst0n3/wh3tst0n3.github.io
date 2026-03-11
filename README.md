# wh3tst0n3.github.io

## Notes on Unreal Engine 5.7 and C++

## GameplayTags

- Can be added in code via macros

``` cpp

// In the header file
#pragma once

#include "NativeGameplayTags.h"

UE_DECLARE_GAMEPLAY_TAG_EXTERN(TAG_Character_Movement_Walk);
UE_DECLARE_GAMEPLAY_TAG_EXTERN(TAG_Equipment_Type_Weapon);

// In the source file

// Define and expose the gameplay tag "Character.Movement.Walk"
UE_DEFINE_GAMEPLAY_TAG(TAG_Character_Movement_Walk, "Character.Movement.Walk");

// Define and expose the gameplay tag "Equipment.Type.Weapon"
UE_DEFINE_GAMEPLAY_TAG(TAG_Equipment_Type_Weapon, "Equipment.Type.Weapo");

```

## Using GAmeplay Tags in C++

``` cpp
#include "GameplayTagContainer.h"
#include "MyActor.generated.h"

UCLASS()
class AMyActor : public AActor, public IGameplayTagAssetInterface
{
    GENERATED_BODY()

public:
    // Expose a container to Blueprints and the Editor
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Gameplay Tags")
    FGameplayTagContainer GameplayTags;

    // Implement the interface function to standardize tag access
    virtual void GetOwnedGameplayTags(FGameplayTagContainer& TagContainer) const override
    {
        TagContainer.Append(GameplayTags);
    }
};

// Check if the actor has a specific tag or any of its children
if (GameplayTags.HasTag(TAG_Status_Stunned))
{
    // Handle stunned logic
}

// Check for an exact tag match, ignoring hierarchy
if (GameplayTags.HasTagExact(TAG_Weapon_Type_Rifle))
{
    // Handle specific rifle logic
}
```
## Custom Debug Logs


- Can be added in code via macros
``` cpp

// In the header file
DECLARE_LOG_CATEGORY_EXTERN(MyLogName, Log, All);

// In the source file
DEFINE_LOG_CATEGORY(MyLogName);

```

You can then use your custom log category when 

## Data Driven Gameplay Elements

## CSV

Good for large files with simple data types, like maps of primitives.

## JSON

Cumbersome for simple data, but much better suited to things like complex object serialization and nested data structures.

## Important notes

Data Tables are *slower* than Data Assets and Curve Tables

Data Assets can e thought of as a single row entry in a complex data table.

