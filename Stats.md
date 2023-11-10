Stats are global integers stored in the GameData (`gd`) context.  They are used for cooldowns, statistics and other global purposes.

| STAT | TYPE | DESCRIPTION | NOTES |
| :--- | :--- | :--- | :--- |
| `ALL_ORGASMS`|||
| `ANAL_ORGASMS`|||
| `ANAL_PARTNERS`|||
| `ANAL_SHAGS`|||
| `BEATINGS_GIVEN`|||
| `BEST_JOB_PERFORMANCE`|||
| `COMPELLED_HYPNOSIS_SESSION`|||
| `CUNNILINGUS_ORGASMS`|||
| `FACIALS`|||
| `HANDJOB_PLEASURE`|||
| `LANDLORD_WATCH_PC_WITH_GF_FOR_RENT_COOLDOWN`|||
| `MONEY_EARNED`|||
| `MONEY_SPENT_CLOTHES`|||
| `OFFICE_BOSS_ASKING_OUT_COOLDOWN`|||
| `OFFICE_PARTY_COOLDOWN`|||
| `ORAL_PLEASURE`|||
| `RENT_MODIFIER`|||
| `RENT_PERIOD`|||
| `RISKY_INSEMINATIONS`|||
| `SALES_SLACKER_FRIENDSHIP_MEETS`|||
| `SEX_ORGASMS`|||
| `SEX_PARTNERS`|Total number of sexual partners||
| `SHAGS`|Vaginal intercourse counter||
| `SHOPPING_TRIPS`|||
| `TEMPORARILY_BLOCK_IMPREGNATION`|||
| `TIMES_MUGGED`|||
| `TITJOB_PLEASURE`|||
| `WEEKS_SINCE_ANAL`|||
| `WEEKS_SINCE_INSEMINATION`|||
| `WEEKS_SINCE_ORGASM`|||
| `WEEKS_SINCE_SEX`|||
| `WEEKS_UNTIL_RENT_PAYMENT`|Weeks until the next rental payment is due||
| `WORK_TROUBLE_COUNTDOWN`|||

## Methods

| Method | Type |  Change | Parameters | Returns |
| :------- | :--- | :----- | :---- | :---- |
| [addStat](Context-Objects#addstatstring-stat-void) | Modify	| Increments the Stat by 1. | String `<stat>` | Void |
| [addStat](Context-Objects#addstatstring-stat-int-amount-void)	| Modify	| Increments the Stat by the specified *amount*. | String `<stat>`, Integer *amount* | Void |
| [getStat](Context-Objects#getstatstring-stat-int)	| Condition |	Gets the value for the supplied Stat. |	String `<stat>` |	Integer |
| [setStat](Context-Objects#setstatstring-stat-int-amount-void)	| Modify | Sets the Stat to specified *amount*. | String `<stat>`, Integer *amount* | Void |

