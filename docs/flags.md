# Flags

Literal flags are **reserved letters** that encode a meaning within the domain of information. For instance, `p` is the flag encoding decimal separator in Numbers:
```
003p46 = 3.46
```

## Replacers

Some flags are **replacers**, so they always carry the same meaning and replace all information in a label domain. They show up alone in a domain.

### Obvious

The flag `o` is a replacer for any domain in a label that is somewhat obvious, like it is described in the documentation or metadata files. It's the lazy option for not filling everything. Use with caution.

### Not-apply

The flag `x` is a replacer for any domain in an asset that somehow not apply, like an exception to the rule.

### Unknown

The flag `z` is a replacer for any domain in an asset that unknown.



