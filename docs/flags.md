# Flags

Literal flags are **reserved characters** that encode a meaning within the domain of information. For instance, `p` is the flag encoding decimal separator in Numbers:
```
'003p46' = 3.46
```
## Separators

### Domain

As mentioned in principles, the domain separator is the underscore `_` character. It splits the domains in a label.

### Subdomain

As mentioned in principles, the subdomain separator is the hyphen `-` character. It splits the subdomains in a label domain.

## Replacers

Some flags are **replacers**, so they always carry the same meaning and replace all information in a label domain. They show up alone in a domain.

### Obvious

The flag `o` is a replacer for any domain in a label that is somewhat obvious, like it is described in the documentation or metadata files. It's the lazy option for not filling everything. Use with caution.

### Not-apply

The flag `x` is a replacer for any domain in an asset that somehow not apply, like an exception to the rule.

### Unknown

The flag `z` is a replacer for any domain in an asset that unknown.

## Catalog

See below the full catalog of flags in Flare.

| Flag        | Domain     | Subdomain | Meaning                                     |
|-------------|------------|-----------|---------------------------------------------|
|`_`          | x          | x         | Domain separator |
|`-`          | All        | x         | Subdomain separator |
|`o`          | All        | x         | Replacer for obvious information |
|`x`          | All        | x         | Replacer for not-apply |
|`z`          | All        | x         | Replacer for unknown information    |
|`p`          | Number     | Fraction  | Decimal separator |
|`w`          | Number     | Sign      | flag for negative sign or West quadrant     |
|`s`          | Number     | Sign      | flag for negative sign or South quadrant     |
|`e`          | Number     | Sign      | flag for positive sign or East quadrant     |
|`n`          | Number     | Sign      | flag for positive sign or North quadrant     |
|`d`          | Number     | Magnitude | Tens multiplier (x10)     |
|`c`          | Number     | Magnitude | Hundreds multiplier (x100)     |
|`k`          | Number     | Magnitude | Thousands multiplier (x1,000)     |
|`m`          | Number     | Magnitude | Millions multiplier (x1,000,000)     |
|`b`          | Number     | Magnitude | Billions multiplier (x1,000,000,000)    |
|`t`          | Timestamp  | Time  | Prefix for time notation |
|`z`          | Timestamp  | Zone  | Prefix for zone notation |
|`u`          | Timerange  | Stop  | Separator of timestamps    |

