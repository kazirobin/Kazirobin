# Date/Time Types

PostgreSQL supports a full set of SQL date and time types, as shown in table below. Dates are counted according to the Gregorian calendar. Here, all the types have resolution of **1 microsecond / 14 digits** except **date** type, whose resolution is **day**.

| **Name** | **Storage Size** | **Description** | **Low Value** | **High Value** |
| --- | --- | --- | --- | --- |
| timestamp [(p)] [without time zone ] | 8 bytes | both date and time (no time zone) | 4713 BC | 294276 AD |
| TIMESTAMPTZ | 8 bytes | both date and time, with time zone | 4713 BC | 294276 AD |
| date | 4 bytes | date (no time of day) | 4713 BC | 5874897 AD |
| time [ (p)] [ without time zone ] | 8 bytes | time of day (no date) | 00:00:00 | 24:00:00 |
| time [ (p)] with time zone | 12 bytes | times of day only, with time zone | 00:00:00+1459 | 24:00:00-1459 |
| interval [fields ] [(p) ] | 12 bytes | time interval | -178000000 years | 178000000 years |