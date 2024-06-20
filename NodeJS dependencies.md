## Specifying version ranges

| Notation              | Semantic                                        |
| --------------------- | ----------------------------------------------- |
| `version`             | match `version` exactly                         |
| `>version`            | greater than `version`                          |
| `>=version`           | not lower than `version`                        |
| `<version`            | lower than `version`                            |
| `<=version`           | not greater than `version`                      |
| `~version`            | approximately equivalent to `version`           |
| `^version`            | compatible with `version`                       |
| `1.2.x`               | 1.2.0, 1.2.1, etc., but not 1.3.0               |
| `http://...`          | url as dependency                               |
| `*`                   | matches any version                             |
| `""`                  | same as `*`                                     |
| `version1 - version2` | same as `>=version1 <=version2`                 |
| `range1 \|\| range2`  | passes if either range1 or range2 are satisfied |
