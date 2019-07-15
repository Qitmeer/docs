---
title: base58
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

### base58-encode

encode a base16 string to a base58 string

#### Example

```bash
~ qx base58-encode 1234567890abcdef
```

```bash
# base58 string
43c9JGZmRvE
```

---

### base58-decode

decode a base58 string to a base16 string

#### Example 1

```bash
~ qx base58-decode RmCYoUMqKZopUkai2YhUFHR9UeqjeyjTAgW
```

```bash
# base16 string
0df144d959afb6db4ad730a6e2c0daf46ceeb98c53a059cd6527
```