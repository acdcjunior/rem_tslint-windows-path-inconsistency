# tslint-quoted-unquoted-path-inconsistency

Quoting paths or not has some weird effects when using `tslint` as script.

# Reproducing...

NPM install before anything:
```bash
# install deps
npm install
```

## Unquoted path (`npm run unquoted`)

- @windows 10
	- All good: three linting errors!
	
	```bash
	$ npm run unquoted

	> tslint-windows-path-inconsistency@1.0.0 unquoted D:\github\tslint-windows-path-inconsistency
	> tslint src/**/*.ts

	src/FirstLevel.ts[1, 12]: " should be '
	src/second/SecondLevel.ts[1, 12]: " should be '
	src/second/third/ThirdLevel.ts[1, 12]: " should be '

	npm ERR! Windows_NT 10.0.14393
	...
	```

- @centos 7
	- **Only one error when three are expected!**
	
	```bash
	[box@box tslint-windows-path-inconsistency]$ npm run unquoted

	> tslint-windows-path-inconsistency@1.0.0 unquoted /box/github/tslint-windows-path-inconsistency
	> tslint src/**/*.ts

	src/second/SecondLevel.ts[1, 12]: " should be '

	npm ERR! Linux 3.10.0-229.el7.x86_64
	...
	```

## Quoted path  (`npm run quoted`)

- @windows 10
	- **Bad: no error whatsoever!**
	
	```bash
	$ npm run quoted

	> tslint-windows-path-inconsistency@1.0.0 quoted D:\github\tslint-windows-path-inconsistency
	> tslint 'src/**/*.ts'

	$
	```

- @centos 7
	- All good!
	
	```bash
	[box@box tslint-windows-path-inconsistency]$ npm run quoted

	> tslint-windows-path-inconsistency@1.0.0 quoted /box/github/tslint-windows-path-inconsistency
	> tslint 'src/**/*.ts'

	src/FirstLevel.ts[1, 12]: " should be '
	src/second/SecondLevel.ts[1, 12]: " should be '
	src/second/third/ThirdLevel.ts[1, 12]: " should be '

	npm ERR! Linux 3.10.0-229.el7.x86_64
	...
```
