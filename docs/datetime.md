# Date and time

Date and time (**datetime**) is a fundamental **domain** in Flare, since nearly all other domains of asset labeling require temporal reference.
To cover different use cases, Flare provides two main **subdomains** of temporal encoding:

- **Timestamps** -- instant records of the timeline.
- **Timeranges** -- arbitrary time interval of the timeline.

> See also the Flare system for [Numbers](https://github.com/ipo-exe/flare/blob/main/docs/numbers.md).

## Timestamps

A timestamp represent a precise record of a date and/or time.
Timestamps are usually part of a **timeseries**, where each entry is valid until the next timestamp occurs.
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

The **time** is separated from **date** by the flag `t`.  
The **zone** is separated from **time** by the flag `z`.

### Date
The date component is encoded as the following subcomponents:

```
{year}{month}{day} = YYYYMMDD
```
Where: 
- year (`YYYY`) = 4 digits integer number;
- month (`MM`) = 2 digits integer number;
- day (`DD`)= 2 digits integer number.

### Time

The time componment is encoded as the following subcomponents:
```
{hour}{minute}{second} = hhmmss
```
Where:
- hour (`hh`) = 2 digits integer number;
- minute (`mm`) = 2 digits integer number;
- second (`ss`)= 2 digits integer number or (optional) real number with 2 digits for the integer part.
hours and minutes are always 2 digits integers. Seconds have at least 2 digits but may optionally include decimals.

### Zone

The zone component is a timezone offset from [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time). It has a [signal prefix](https://github.com/ipo-exe/flare/blob/main/docs/numbers.md#signal) (`w/e` or `s/n`) and an offset in `{hour}{minute}`.
```
{signal}{hour}{minute} = shhmmss
```

### Human-readable mode

**Human-readable mode** allows insertion of hyphens (`-`) between timestamp components 
and in the subcomponents of **date** to improve readability:
```
YYYY-MM-DD-thhmmss-zshhmm
```

### Examples

| Encoded                    | Decoded (ISO 8601)             |
|----------------------------|--------------------------------|
| `20140302t124804p143zw0300`| 2014-03-02 12:48:04.143 -03:00 |
| `20140302t124804`          | 2014-03-02 12:48:04 (no zone)  |
| `2014-03-02-T124804`       | 2014-03-02 12:48:04 (no zone)  |
| `20140302`                 | 2014-03-02 (daily)             |
| `2014-03`                  | 2014-03 (monthly)              |
| `2014`                     | 2014 (yearly)                  |


## Timeranges

**Timeranges** represent any arbitrary interval between a start and end point in the timeline. These are used when the temporal span must be explicitly delimited.

### Structure

The timerange is simply a concatenation of two timestamps denoting the interval. The flag for separator is the `u` letter, denoting the "union":
```
{timestamp_start}u{timestamp_stop}
```

Where:
- `timestamp_start` is the starting time of the interval (inclusive lower limit);
- `timestamp_stop` is the stopping time of the interval (exclusive upper limit).

> Note: by exclusive upper limit Flare means that at that moment the timerange is no longer valid.
> Hence, in a timerange of `2020u2030` the year 2030 is not included.

### Examples

| Encoded                                           | Decoded                                   |
|---------------------------------------------------|-------------------------------------------|
| `20140302t124804u20140302t134804`                 | 2014-03-02 12:48:04 → 2014-03-02 13:48:04 |
| `20140302u20140305`                               | 2014-03-02 → 2014-03-05 (daily interval)  |
| `2014-03u2014-04`                                 | 2014-03 → 2014-04 (monthly interval)      |
| `2014U2015`                                       | 2014 → 2015 (yearly interval)             |
| `20140302t124804p143zw0300u20140302t134804zw0300` | 2014-03-02 12:48:04.143 -03:00 → 2014-03-02 13:48:04 -03:00 |

## Flags

The literal flags of datetime are summarised below:

| Flag        | Domain     | Subdomain | Meaning                                     |
|-------------|------------|-----------|---------------------------------------------|
|`t`          | Datetime   | Timestamp | Separator of date and time |
|`z`          | Datetime   | Timestamp | Separator of time and zone |
|`u`          | Datetime   | Timerange | Separator of timestamps    |



