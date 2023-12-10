## Arousal

| Method | Type | Scope | Mechanic/Item | Change | Parameters | Returns |
| :------- | :--- | :---- | :------------ | :----- | :---- | :---- |
| [addArousalTiny](Context-Objects#addarousaltiny-void) | Modify | PC/NPC | Arousal | Very small Increase (1) | None  | Void |
| [addArousalSmall](Context-Objects#addarousalsmall-void) | Modify | PC/NPC | Arousal | Small increase (2) | None  | Void |
| [addArousalMedium](Context-Objects#addarousalmedium-void) | Modify | PC/NPC | Arousal | Moderate increase (4) | None  | Void |
| [addArousalLarge](Context-Objects#addarousallarge-void) | Modify | PC/NPC | Arousal | Large increase (6) | None  | Void |
| [addArousalHuge](Context-Objects#addarousalhuge-void) | Modify | PC/NPC | Arousal | Very large increase (10) | None  | Void |
| [isArousalComfort](Context-Objects#isarousalcomfort-boolean) | Condition | PC/NPC | Arousal | Is arousal at or above the "comfort" threshold? | None  | Boolean |
| [isArousalEnjoy](Context-Objects#isarousalenjoy-boolean) | Condition | PC/NPC | Arousal | Is arousal at or above the "enjoy" threshold? | None  | Boolean |
| [isArousalClose](Context-Objects#isarousalclose-boolean) | Condition | PC/NPC | Arousal | Is arousal at or above the "close" threshold? | None  | Boolean |
| [isArousalOrgasm](Context-Objects#isarousalorgasm-boolean) | Condition | PC/NPC | Arousal | Is arousal at or above the "orgasm" threshold? | None  | Boolean |
| [reduceArousalTiny](Context-Objects#reducearousaltiny-void) | Modify | PC/NPC | Arousal | Very small decrease (1) | None  | Void |
| [reduceArousalSmall](Context-Objects#reducearousalsmall-void) | Modify | PC/NPC | Arousal | Small decrease (2) | None  | Void |
| [reduceArousalMedium](Context-Objects#reducearousalmedium-void) | Modify | PC/NPC | Arousal | Moderate decrease (4) | None  | Void |
| [reduceArousalLarge](Context-Objects#reducearousallarge-void) | Modify | PC/NPC | Arousal | Large decrease (6) | None  | Void |
| [reduceArousalHuge](Context-Objects#reducearousalhuge-void) | Modify | PC/NPC | Arousal | Very large decrease (10) | None  | Void |
| [setArousalDiscomfort](Context-Objects#setarousaldiscomfort-void) | Modify | PC/NPC | Arousal | Sets arousal level to lowest "discomfort" level | None  | Void |
| [setArousalComfort](Context-Objects#setarousalcomfort-void) | Modify | PC/NPC | Arousal | Sets arousal level to the "comfort" threshold | None  | Void |
| [setArousalEnjoy](Context-Objects#setarousalenjoy-void) | Modify | PC/NPC | Arousal | Sets arousal level to the "enjoy" threshold | None  | Void |
| [setArousalClose](Context-Objects#setarousalclose-void) | Modify |  PC/NPC | Arousal | Sets arousal level to the "close" threshold | None  | Void |
| [setArousalOrgasm](Context-Objects#setarousalorgasm-void) | Modify | PC/NPC | Arousal | Sets arousal level to the "orgasm" threshold | None  | Void |

## Alcohol

| Method | Type | Scope | Mechanic/Item | Change | Parameters | Returns |
| :------- | :--- | :---- | :------------ | :----- | :---- | :---- |
| [addAlcoholSmall](Context-Objects#addalcoholsmall-void) | Modify | PC/NPC | Alcohol | Small increase | None  | Void |
| [addAlcoholMedium](Context-Objects#addalcoholmedium-void) | Modify | PC/NPC | Alcohol | Moderate increase | None  | Void |
| [addAlcoholLarge](Context-Objects#addalcohollarge-void) | Modify | PC/NPC | Alcohol | Significant increase | None  | Void |
| [clearAlcohol](Context-Objects#clearalcohol-void) | Modify | PC/NPC | Alcohol | Sets alcohol level to zero | None  | Void |
| [reduceAlcoholSmall](Context-Objects#reducealcoholsmall-void) | Modify | PC/NPC | Alcohol | Small decrease | None  | Void |
| [reduceAlcoholMedium](Context-Objects#reducealcoholmedium-void) | Modify | PC/NPC | Alcohol | Moderate decrease | None  | Void |
| [reduceAlcoholLarge](Context-Objects#reducealcohollarge-void) | Modify | PC/NPC | Alcohol | Significant decrease | None  | Void |


## GameData

| Method | Type | Scope | Mechanic/Item | Change | Parameters | Returns |
| :------- | :--- | :---- | :------------ | :----- | :---- | :---- |
| [addJobPerformanceModifier](Context-Objects#addjobperformancemodifierint-amount-void) | Modify | GameData | Employment | Adds a numeric modifier for the next time job performance is calculated.  | Integer amount | Void |
| [addStat](Context-Objects#addstatstring-stat-void) | Modify	| GameData | Stats | Increments the stat by 1 | String `<stat>` | Void |


