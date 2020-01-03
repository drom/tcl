```tcl
# comment
set x 2
set op *;
set sum [expr $x$op$x]
puts "hello $sum"
```

```js
let {puts, expr} = require('tcl');
let x, op, sum;

// comment
x = 2;
op = '*';
sum = expr(x + op + x);
puts('hello ', sum);
```

----

```tcl
set age 10

if {$age < 20} {
  puts "Age is less than 20"
} else {
  puts "Age is greater than 20"
}
```

```js
let {puts} = require('tcl');
let age;

age = 10;

if (age < 20) {
  puts('Age is less than 20');
} else {
  puts('Age is greater than 20');
}
```

----

```tcl
set a {1 2 3}
if {1 in $a} {
  puts "ok"
} else {
  puts "fail"
}
```

```js
let {puts, inOp} = require('tcl');
let a;

a = '1 2 3';

if (inOp(1, a)) {
  puts('ok');
} else {
  puts('fail');
}
```
