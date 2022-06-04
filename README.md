# TFT_counter
Find tft's best compos, their counters and different stats
## Dataset

The data is pulled every X days and pushed to an s3 bucket (parquet files)

### Raw
The raw datasets are as follows:

#### challenger_raw
Contains information about TFT's challenger players

| Column       | Type   | Data type                                                                      |
|--------------|--------|--------------------------------------------------------------------------------|
| summonerId   | String | Encrypted Summoner Id                                                          |
| summonerName | String | Summoner name                                                                  |
| leaguePoints | Int    | # of league points                                                             |
| rank         | String | rank code (should be "I" for all cases since we only pull challenger data)     |
| wins         | Int    | # of wins (1st position)                                                       |
| loses        | Int    | # of loses (position != 1st)                                                   |
| veteran      | Bool   | Wether the summoner has been in the challenger rank for more than X weeks      |
| inactive     | Bool   | Wether the summoner has not played a ranked match in the last X days           |
| freshblood   | Bool   | Wether it's the first consecutive week this summoner is in the challenger rank |
| hotStreak    | Bool   | Wether the player has won X % of the last ranked games                         |

#### challenger_matches
Contains matches data 
| Column        | Type         | Data type                                                                 |
|---------------|--------------|---------------------------------------------------------------------------|
| matchId       | String       | unique ID of the match                                                    |
| puuid         | String       | participant id                                                            |
| lastRound     | Int          | # of the last round the payer survived                                    |
| level         | Int          | Level of the player by the end of the mach                                |
| placement     | Int          | Rank of said user in the match                                            |
| time_alive    | float        | number of seconds until the player was eliminated                         |
| active_traits | List[Trait]  | List of the active traits for the player at the time of its death         |
| units         | List[Unit]   | List of units present in the board of the player by the time of its death |
| augments      | List[String] | List of the augments the player had by the time of its death              |

The trait object is defined as:
| Column        | Type         | Data type                                                                 |
|---------------|--------------|---------------------------------------------------------------------------|
| name          | String       | Name of the active trait                                                  |
| tier          | Int          | Tier of the active trait                                                  |
The Unit object is defined as:
| Column        | Type         | Data type                                                                 |
|---------------|--------------|---------------------------------------------------------------------------|
| name          | String       | Name of the unit                                                          |
| tier          | Int          | Tier of the unit                                                          |
| items         | list[Int]    | List of the id's of the unit's items                                      |
