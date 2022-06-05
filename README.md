```javascript
const re = new RegExp('^' + require('legal-versioning-regexp') + '$')
const assert = require('assert')

const valid = [
  '1.2.3',
  '10.20.30',
  '100.200.300',
  '1.2.3-4',
  '1.2.3-45'
]

for (const version of valid) assert(re.test(version))

const invalid = [
  '001.2.3', // leading zeroes in edition
  '01.2.3', // leading zero in edition
  '1.02.3', // leading zero in update
  '1.2.03', // leading zero in correction
  '1.0.0-0', // draft zero
  '1.0.0-01' // leading zero in draft
]

for (const version of invalid) assert(!re.test(version))
```

The following capture groups are part of the versioned public API of this package.

```javascript
const { groups } = re.exec('1.2.3-4')
assert(groups.edition === '1')
assert(groups.update === '2')
assert(groups.correction === '3')
assert(groups.draft === '4')
```
