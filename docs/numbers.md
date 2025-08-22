# Numbers

Numbers are a **core component** of Flare labels and are present in nearly every type of label.  
They must be encoded in a **text-based, consistent, and unambiguous format**, ensuring that labels are sortable, readable, and machine-actionable.  

Flare provides a structured approach to encoding **integer numbers, real numbers, signals, and magnitude multipliers**. Each type has a specific role and format within a label.

## Summary

| Number convention    | Rule / Format                       | Notes                                   |
|----------------------|--------------------------------------|-----------------------------------------|
| Integer numbers      | Zero-filled, fixed length            | Ensures alignment and lexical sorting   |
| Real numbers         | `{integer}p{decimals}`               | Uses `p` instead of `.` for decimals    |
| Signal (prefixes)    | flags `w`, `s`, `e`, `n`             | Case-insensitive; applied as prefixes  |
| Magnitude (suffixes) | flags `c`, `k`, `m`, `b`             | Case-insensitive; applied as suffixes |

## Flags

The literal flags of numbers are summarised below:

| Flag        | Domain     | Subdomain | Meaning                                     |
|-------------|------------|-----------|---------------------------------------------|
|`p`          | Number     | Fraction  | Decimal separator |
|`w`          | Number     | Sign      | flag for negative sign or West quadrant     |
|`s`          | Number     | Sign      | flag for negative sign or South quadrant     |
|`e`          | Number     | Sign      | flag for positive sign or East quadrant     |
|`n`          | Number     | Sign      | flag for positive sign or North quadrant     |
|`d`          | Number     | Magnitude | Tens multiplier (x10)     |
|`c`          | Number     | Magnitude | Hundreds multiplier (x100)     |
|`k`          | Number     | Magnitude | Thousands multiplier (x1,000)     |
|`m`          | Number     | Magnitude | Millions multiplier (x1,000,000)     |
|`b`          | Datetime   | Timerange | Billions multiplier (x1,000,000,000)    |

---

## Integers

Integer numbers are the most basic form of numerical encoding in Flare.  
They are used to represent counts, indices, or sequential identifiers.  
To ensure proper alignment and **consistent sorting**, integers are typically represented in a **zero-filled format** with a pre-set length for each label chunk.  
This avoids issues where, for example, `2` would otherwise appear after `20` in a lexical sort.

- **Format:** zero-filled integers of fixed length.  
- **Purpose:** alignment, sorting, and clarity.

Examples
| Encoded           | Decoded                        |
|----------------|-------|
| `00002`        | 2     |
| `00020`        | 20    |
| `01223`        | 1223  |

---

## Fractions

Real numbers extend the integer format by allowing **decimal fractions**.  
Because certain characters, like the period (`.`), are prohibited in labels, Flare uses the **letter `p` as a decimal separator**.  
This allows precise numerical values to be encoded without violating the text-only principle.

- **Format:** `[integer]p[decimals]`  
- **Purpose:** represent fractional values in a fully text-compatible way.

Examples
| Encoded           | Decoded                        |
|----------------|-------|
| `002p3`        | 2.3   |
| `023p4`        | 23.4  |
| `125p0`        | 125.0 |

---

## Sign

By default, Flare assumes the sign of a number is **positive**. But in some contexts, numbers need to convey **direction, polarity, or orientation**, such as in georeferencing or coordinate systems. For this, Flare uses **signal flags**, which are letters placed at the **beginning of a number**, to indicate whether it is positive or negative.  

| Prefix | Sign      | Quadrant |
|--------|-----------| -------- |
| `w`    | negative  | West     |
| `s`    | negative  | South    |
| `e`    | positive  | East     |
| `n`    | positive  | North    |

- Sign flags are **case-insensitive** and are always **prefixes to the numeric value**.

Examples
| Encoded        | Decoded                        |
|----------------|---------|
| `S002p3`       | -2.3    |
| `N023p4`       | +23.4   |
| `w125p0`       | -125.0  |

---

## Magnitude

By default, Flare assumes the multiplier of a number is 1. Sometimes, it is necessary to indicate that a number should be interpreted with a **scale or multiplier**, such as hundreds or thousands.  
Flare uses **magnitude multiplier flags** as **suffixes** to numbers, separate from signals, to encode this information.

| Suffix | Multiplier        |
|------|-----------------|
| `d`  | tens (×10)  |
| `c`  | hundreds (×100)  |
| `k`  | thousands (×1,000) |
| `m`  | millions (×1,000,000) |
| `b`  | billions (×1,000,000,000) | 

- Multipliers are **optional** and **case-insensitive**, allowing consistent scaling in numeric encoding.

Examples
| Encoded           | Decoded                        |
|----------------|--------------|
| `02p3k`        | 2,300.0     |
| `23p44c`       | 2,344.0     |
| `W05P0M`       | -5,000,000.0 |

