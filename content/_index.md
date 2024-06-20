---
title: "Home"
---

<img src="/images/cobalt-manta.png" style="max-width:15%;min-width:40px;float:right;" alt="Manta ray" />

# cobalt

### ~

...is my personal, minimal website powered by [Hugo](https://gohugo.io/) and based on my
[fork](https://github.com/cicovic-andrija/hugo-xmin-fork) of [XMin](https://github.com/yihui/hugo-xmin).
It's a learning journal about programming & software systems, SCUBA diving, literature ... and a collection of
other arbitrary notes. If you happen to not be me and reading this, suggestions and bug reports are welcome
[@my-e-mail-address](mailto:cicovic.andrija@gmail.com).

Let's dive in. ⚓

### First, a quine

A _quine_ is a computer program that produces a copy of its own source code as its output:

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

### Then, everything else
