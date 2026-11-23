# Calculate Custom Score

This method is used to define the formula on how the individual scores and weights will come together. This method will run 3 times per Job and System combination.

## Context

`PsJobScoreInfo ScoreInfo`

Gets a PsJobScoreInfo object for the job and system combination. This object holds properties that give information on the Job, System, and Product that is currently being scored.

`int ScoreType`

Gets an integer value that is used to differentiate which run of the 3 that is currently being run.
