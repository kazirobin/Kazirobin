# Monetary Types

The money type stores a currency amount with a fixed fractional precision. Values of the numeric, int, and bigint data types can be cast to money. Using Floating point numbers is not recommended to handle money due to the potential for rounding errors.

| **Name** | **Storage Size** | **Description** | **Range** |
| --- | --- | --- | --- |
| money | 8 bytes | currency amount | -92233720368547758.08 to +92233720368547758.07 |