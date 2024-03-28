---
title: "Home"
---

# cobalt

### _inspired by the deep, endless expanse of the sea_

...is my minimal+personal website, powered by [Hugo](https://gohugo.io/) and based on my fork of
[XMin](https://github.com/yihui/hugo-xmin). It contains an exploration journal about software systems, SCUBA diving and
literature. There are also cooking recipes sprinkled around... and other arbitrary notes.

Let's dive in [:)]

### First, a quine:

A _quine_ is a computer program that takes no input and produces a copy of its own source code as its only output:

```
/* assumed ASCII code table */
#include <stdio.h>
const char *program = "/* assumed ASCII code table */%c#include <stdio.h>%cconst char *program = %c%s%c;%cint main(void)%c{%cprintf(program, 10, 10, 34, program, 34, 10, 10, 10, 10, 10, 10);%creturn 0;%c}%c";
int main(void)
{
printf(program, 10, 10, 34, program, 34, 10, 10, 10, 10, 10, 10);
return 0;
}
```

### Then, everything else:
