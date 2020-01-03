```tcl
# comment
set x 2
set op *;
set sum [expr $x$op$x]
puts "hello $sum"
```

```js
// comment
let x = 2;
let op = '*';
let sum = expr(x() + op() + x());
puts("hello " + sum);
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
let age = 10;

if (age < 20) {
  puts('Age is less than 20')
} else {
  puts('Age is greater than 20')
}
```

----

```tcl
set a {1 2 3}
if {1 in $a} {
  puts "ok"
} else {
  puts "fail"
}```

```js
let a = '1 2 3';

if(_in(1, a)) {
  puts('ok');
} else {
  puts('fail');
}
```
