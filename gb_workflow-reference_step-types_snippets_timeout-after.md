# Timeout

Specifies a span of time after which a Step will **Timeout** and exit execution.

For example, if `Hours` = 1, `Minutes` = 5, `Seconds` = 8, then a Step will timeout (exit with a Timeout result) if it does not complete successfully after (1 \* 3600) + (5 \* 60) + 8 = 3908 Seconds.

## Timeout After

### Hours

Specifies an (integer) number of hours.

### Minutes

Specifies an (integer) number of minutes.

### Seconds

Specifies an (integer) number of seconds.
