# Asset Manager

## Description

The Asset Manager class grew out of a need to dynamically manage large collections of types, such as weapons or items in an RPG.

There is only one Asset Manager instance ever, this includes in the editor.

## Key Points

- The Asset Manager is a Global Singleton UObject
- Not specific to Game Mode or Map
- Communicates with [Asset Registry](AssetRegistry.md)
- Maintains global asset state (loaded, unloaded, etc)
- Integrates disparate Unreal systems like cooking and async loading
- Query every loadable item
- Hide complexity of Blueprint classes
- Mitigate long loading times caused by statically loading all game data at startup
- Suports soft references for async loading
- Handle loading states
- Handle packaging and cooking rules

## Asset Manager Compnents

### Primary Asset ***Type***

- One per item class

### Primary Asset ***ID***

- One ID per item asset

### Primary Asset ***Rules***

- Cooking and chunking management

### Primary Asset ***Settings***

- Game-specific settings for how to utilize primary assets

### Secondary Assets

- The assets that a Primary Asset type is comprised of

## Primary Asset ***Type***

- Uses a unique subclass of `UPrimaryDataAsset`
- Primary Assets are Top_Level assets, essentially meaning the thing the game talks about - MapType, WeaponType, PotionType

### To declare a new Primary Data Asset

``` cpp

#pragma once

#include "CoreMinimal.h
#include "MyPrimaryDataAsset.generated.h"


```
