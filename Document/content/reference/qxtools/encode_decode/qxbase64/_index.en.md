---
title: base64
weight: 3
#pre: "<b>1. </b>"
# chapter: true
---

### base64-encode

Convert a base16 string to a base64 string.

```bash
~ qx base64-encode --help

Usage: qx base64-encode [hexstring]
```

#### Example 1

```bash
~ qx base64-encode 1234567890abcdef

# base64 string
EjRWeJCrze8=
```

---

### base64-decode

Convert a base64 string to a base16 string.

```bash
~ qx base64-decode --help

Usage: qx base64-decode [hexstring]
```

#### Example 2

```bash
~ qx base64-decode EjRWeJCrze8=

# base16 string
1234567890abcdef
```