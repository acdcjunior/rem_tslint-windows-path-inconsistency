# tslint-windows-path-bug

Run

```bash
# install deps
npm install

# no quotes works (lint error is shown)
npm run works

# with quotes doesn't work on windows: no lint error is shown
npm run doesntwork
```