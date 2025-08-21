# Flare — Numbers

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

---

## 1. Integer numbers

Integer numbers are the most basic form of numerical encoding in Flare.  
They are used to represent counts, indices, or sequential identifiers.  
To ensure proper alignment and **consistent sorting**, integers are typically represented in a **zero-filled format** with a pre-set length for each label chunk.  
This avoids issues where, for example, `2` would otherwise appear after `20` in a lexical sort.

- **Format:** zero-filled integers of fixed length.  
- **Purpose:** alignment, sorting, and clarity.

---

## 2. Real numbers

Real numbers extend the integer format by allowing **decimal fractions**.  
Because certain characters, like the period (`.`), are prohibited in labels, Flare uses the **letter `p` as a decimal separator**.  
This allows precise numerical values to be encoded without violating the text-only principle.

- **Format:** `[integer]p[decimals]`  
- **Purpose:** represent fractional values in a fully text-compatible way.

---

## 3. Signal prefix

In some contexts, numbers need to convey **direction, polarity, or orientation**, such as in georeferencing or coordinate systems.  
Flare uses **signal flags**, which are letters placed at the **beginning of a number**, to indicate whether it is positive or negative.  

| Prefix | Signal    | Quadrant |
|--------|-----------| -------- |
| `w`    | negative  | West     |
| `s`    | negative  | South    |
| `e`    | positive  | East     |
| `n`    | positive  | North    |

- Signal flags are **case-insensitive** and are always **prefixes to the numeric value**.

---

## 4. Magnitude suffix

Sometimes, it is necessary to indicate that a number should be interpreted with a **scale or multiplier**, such as hundreds or thousands.  
Flare uses **magnitude multiplier flags** as **suffixes** to numbers, separate from signals, to encode this information.

| Suffix | Multiplier        |
|------|-----------------|
| `c`  | hundreds (×100)  |
| `k`  | thousands (×1,000) |
| `m`  | millions (×1,000,000) |
| `b`  | billions (×1,000,000,000) | 

- Multipliers are **optional** and **case-insensitive**, allowing consistent scaling in numeric encoding.

---

By combining **integer numbers, real numbers, signals, and magnitude multipliers**, Flare can encode **precise, scaled, and directional numerical information** in a text-based label format that is fully consistent with its principles.


