:construction: TCL to JavaScript Transpiler :construction:

How Ugly it would look like?

## Other projects

* https://github.com/cyanogilvie/Tcl.js - Javascript implementation of the Tcl language
* https://github.com/rubikscraft/tcl-js - A native Javascript TCL interpreter
* https://github.com/nukedzn/node-tcl - Node.JS Tcl binding. NAN, 2017
* https://github.com/bovine/nodetcl - Node.JS extension to allow Tcl code to be invoked from JavaScript, 2012

## Transpiler vs Interpreter

An interpreter (or a bytecode VM) written in JS makes significantly more sense than a static transpiler. Tcl’s core architecture—where control structures are ordinary commands and execution relies heavily on runtime evaluation—makes static compilation into JavaScript virtually impossible without generating code that essentially mimics an embedded interpreter anyway.

**Key Tcl Semantics That Sabotage Transpilation**

* **Stack Manipulation (`upvar` / `uplevel`):** Tcl procedures can directly read and mutate variables in arbitrary parent call stack frames. Standard JavaScript lexical scoping does not allow function calls to inspect or modify parent variables without explicit runtime context objects.
* **No Syntax Keywords:** Commands like `if`, `for`, `while`, and `proc` are standard runtime functions accepting strings, not parser keywords. A Tcl script can redefine or alias `if` at runtime, which breaks static AST-to-JS mappings.
* **Everything is a String:** Code blocks, lists, and numbers are treated as strings until evaluated. Because Tcl scripts frequently construct and execute code dynamically (`eval`, `subst`), a transpiler would still have to bundle a complete JS-side parser and evaluator runtime.

| Metric | Tcl-to-JS Transpiler | Tcl Interpreter / VM |
| --- | --- | --- |
| **Implementation Complexity** | Extremely High (requires heavy JS codegen wrappers) | Moderate (clean tree-walk or instruction loop) |
| **Tcl Feature Parity** | Low (breaks on `uplevel`, custom `if`, dynamic redefs) | High (full control over environment & call stack) |
| **Performance** | Marginally faster math, slow dynamic lookups | Predictable; can optimize via value dual-housing |
| **Debugging** | Hard (mapping dynamic Tcl source to generated JS) | Easy (direct access to Tcl stack traces and AST) |

**Recommended Architecture**

Build an **AST tree-walk interpreter** or a simple **bytecode VM** utilizing these patterns:

1. **Explicit Stack Frames:** Model call stacks as objects (`{ vars: Map, caller: Frame }`). This makes `upvar` and `uplevel` simple dictionary lookups up the chain.
2. **String Dual-Porting ("Shimmering"):** Represent values as objects holding both a string representation and a cached internal representation (like a JS array or number) to avoid repeated string re-parsing.
3. **Selective JIT for `expr`:** Use JS's `new Function()` solely to compile static expressions within `expr` commands into native JS math, as arithmetic is the main bottleneck in Tcl interpreters.
