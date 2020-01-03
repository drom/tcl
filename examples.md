| TCL | JS |
|-|-|
| `# comment` | `// comment` |
| `set x 2`  | `let x = () => 2;`    |
| `set op *` | `let op = () => '*';` |
| `set sum [expr {$x + 3}];` | `let sum = () => expr(x() + 3);` |
| `puts "hello $sum"` | `puts("hello " + sum());` |

