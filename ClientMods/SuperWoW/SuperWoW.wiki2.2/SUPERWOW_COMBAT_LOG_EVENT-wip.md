# SUPERWOW_COMBAT_LOG_EVENT WIP

## Common Params
| 1st Param | 2nd Param | 3rd Param | 4th Param | 5th Param | 6th Param | 7th Param | 8th Param |
| --------  | -------- | -------- | -------- | -------- | -------- |-------- | -------- |
| timestamp | event    | sourceGUID    | sourceName  | sourceFlags | destGUID | destName  | destFlags |


## Prefix Params
Prefix | 1st Parameter (9th) | 2nd Paramater (10th) | 3rd Parameter (11th)
-- | -- | -- | --
SWING
SPELL | spellId | spellName | spellSchool
SPELL_PERIODIC | spellId | spellName | spellSchool
ENVIRONMENTAL | environmentalType

## Suffix Params
Suffix | 1st Param | 2nd Param | 3rd Param | 4th Param  | 5th Param | 6th Param | 7th Param | 8th Param | 9th Param
-- | -- | -- | -- | -- | -- | -- | -- | -- | --
_DAMAGE | amount | school | resisted | blocked | absorbed | critical | glancing | crushing | isOffHand
_MISSED | missType | isOffHand | 
_HEAL | amount | critical
_ENERGIZE | amount | powerType
_DRAIN | amount | powerType
_LEECH | amount | powerType | extraAmount
_DISPEL 
_EXTRA_ATTACKS | amount
_AURA_APPLIED | auraType
_AURA_REMOVED | auraType
_AURA_APPLIED_DOSE | auraType | amount
_AURA_REMOVED_DOSE | auraType | amount
_CAST_START | castTime
_CAST_SUCCESS
_CAST_FAILED
_INSTAKILL

### Special Events:
DAMAGE_SPLIT: Params of SPELL prefix + _DAMAGE suffix.

DAMAGE_SHIELD: Params of no prefix + _DAMAGE suffix.

UNIT_DIED

PARTY_KILL