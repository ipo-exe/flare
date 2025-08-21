# Date and time

Date and time are fundamental dimensions in Flare, since nearly all domains of file and asset labeling require temporal reference.
To cover different use cases, Flare provides two main categories of temporal encoding:

- **Timestamps** 
- **Timeranges** represent explicit intervals between a start and end point. These are used when the temporal span must be explicitly delimited.

## Timestamps

A timestamp represent a precise record of a date and/or time.
Timestamps are usually part of a **time series**, where each entry is valid until the next timestamp occurs.
In this sense, the Flare system is mostly based on the [ISO 8601 standard](https://en.wikipedia.org/wiki/ISO_8601).
The table below show all variants of timestamps.

| Variant          | Alias  | Signature                     | Length (chars) | Pattern    | 
|-----------------|---------|-------------------------------|----------------|------------|
| Full            | `ts`    | `YYYYMMDDthhmmsszshhmm`       | ≥ 21           | `*t*z*`    |
| Full human      | `tsh`   | `YYYY-MM-DD-thhmmss-zshhmm`   | ≥ 25           | `*-*-t*-z*`| 
| Un-zoned        | `tsu`   | `YYYYMMDDthhmmss`             | ≥ 15           | `*t*`      | 
| Un-zoned human  | `tsuh`  | `YYYY-MM-DD-thhmmss`          | ≥ 18           | `*-*-*-t*` |
| Daily           | `tsd`   | `YYYYMMDD`                    | 8              | `*`        |
| Daily human     | `tsdh`  | `YYYY-MM-DD`                  | 10             | `*-*-*`    | 
| Monthly         | `tsm`   | `YYYYMM`                      | 6              | `*`        |
| Monthly human   | `tsmh`  | `YYYY-MM`                     | 7              | `*-*`      |
| Yearly          | `tsy`   | `YYYY`                        | 4              | `*`        | 


### Structure

The structure of a **full timestamp** is composed of three main components:

```
{date}t{time}z{zone}
```

### Flags

The **time** is separated from **date** by the lowercase flag `t`.  
The **zone** is separated from **time** by the lowercase flag `z`.

### Date subcomponents
The date component is encoded as the following subcomponents:

```
{year}{month}{day} = YYYYMMDD
```
Where: 
- year (`YYYY`) = 4 digits integer number;
- month (`MM`) = 2 digits integer number;
- day (`DD`)= 2 digits integer number.

>> [!tip] See the Flare system for Numbers.

### Time subcomponents

The time componment is encoded as the following subcomponents:
```
{hour}{minute}{second} = hhmmss
```
Where:
- hour (`hh`) = 2 digits integer number;
- minute (`mm`) = 2 digits integer number;
- second (`ss`)= 2 digits integer number or (optional) real number with 2 digits for the integer part.
hours and minutes are always 2 digits integers. Seconds have at least 2 digits but may optionally include decimals.

### Zone subcomponents

The zone component is a timezone offset from [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time), followed by a signal (`w/e` or `s/n`) and an offset in `{hour}{minute}`.
```
{signal}{hour}{minute} = shhmmss
```

### Human-readable mode

**Human-readable mode** allows insertion of hyphens (`-`) between timestant components 
and in the subcomponents of **date** to improve readability:
```
YYYY-MM-DD-thhmmss-zshhmm
```

 ``

### Examples of timestamps

| Flare encoding | Value
`20140302T124804P143ZW0300` | 2014-03-02 12:48:04.143 -03:00 |
