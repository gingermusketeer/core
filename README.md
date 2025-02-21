@oclif/core
===========

base library for oclif CLIs

[![Version](https://img.shields.io/npm/v/@oclif/core.svg)](https://npmjs.org/package/@oclif/core)
[![CircleCI](https://circleci.com/gh/oclif/core/tree/main.svg?style=svg)](https://circleci.com/gh/oclif/core/tree/main)
[![Downloads/week](https://img.shields.io/npm/dw/@oclif/core.svg)](https://npmjs.org/package/@oclif/core)
[![License](https://img.shields.io/npm/l/@oclif/core.svg)](https://github.com/oclif/core/blob/main/package.json)


Migrating
=====

If you're migrating from the old oclif libraries (`@oclif/config`, `@oclif/command`, `@oclif/error`, `@oclif/parser`), see the [migration guide](./MIGRATION.md).

Usage
=====

Without the generator, you can create a simple CLI like this:

**TypeScript**
```js
#!/usr/bin/env ts-node

import * as fs from 'fs'
import {Command, flags} from '@oclif/core'

class LS extends Command {
  static flags = {
    version: flags.version(),
    help: flags.help(),
    // run with --dir= or -d=
    dir: flags.string({
      char: 'd',
      default: process.cwd(),
    }),
  }

  async run() {
    const {flags} = this.parse(LS)
    let files = fs.readdirSync(flags.dir)
    for (let f of files) {
      this.log(f)
    }
  }
}

LS.run()
.catch(require('@oclif/core/handle'))
```

Then run either of these with:

```sh-session
$ ./myscript
...files in current dir...
$ ./myscript --dir foobar
...files in ./foobar...
$ ./myscript --version
myscript/0.0.0 darwin-x64 node-v9.5.0
$ ./myscript --help
USAGE
  $ @oclif/core

OPTIONS
  -d, --dir=dir  [default: /Users/jdickey/src/github.com/oclif/core]
  --help         show CLI help
  --version      show CLI version
```

See the [generator](https://github.com/oclif/oclif) for all the options you can pass to the command.
