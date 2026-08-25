# Third-party notices

This repository vendors one third-party skill, unmodified, alongside its own MIT-licensed content.

## unslop

- **Source:** [`cursor/plugins`](https://github.com/cursor/plugins), inside the `pstack` plugin
- **Upstream file:** https://github.com/cursor/plugins/blob/main/pstack/skills/unslop/SKILL.md
- **Author:** Lauren Tan (`pstack` plugin author, per the `cursor/plugins` plugin table)
- **License:** MIT. The `cursor/plugins` repository's README states its overall license as MIT
- **Vendored at:** [`skills/unslop/SKILL.md`](./skills/unslop/SKILL.md), copied verbatim
- **Included under:** MIT License (see full text below)

**Diligence note.** Each plugin folder in `cursor/plugins` (e.g. `pstack/`) may carry its own `LICENSE` file, and none could be checked when this notice was written. The repository-wide README states "License: MIT" with no listed exceptions; that statement is the basis for vendoring this file here. If real legal stakes ride on this, check `github.com/cursor/plugins/tree/main/pstack` yourself for a plugin-specific `LICENSE` that narrows or overrides the repo-wide grant.

If you'd rather not vendor a copy at all, you can depend on it at runtime instead, without copying anything into this repo:

```bash
npx skills add https://github.com/cursor/plugins --skill unslop
```

---

### MIT License

```
MIT License

Copyright (c) Cursor / Lauren Tan (pstack plugin, cursor/plugins repository)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
