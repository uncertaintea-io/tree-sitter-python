# tree-sitter-python

[![CI][ci]](https://github.com/tree-sitter/tree-sitter-python/actions/workflows/ci.yml)
[![discord][discord]](https://discord.gg/w7nTvsVJhm)
[![matrix][matrix]](https://matrix.to/#/#tree-sitter-chat:matrix.org)
[![crates][crates]](https://crates.io/crates/tree-sitter-python)
[![npm][npm]](https://www.npmjs.com/package/tree-sitter-python)
[![pypi][pypi]](https://pypi.org/project/tree-sitter-python/)

Python grammar for [tree-sitter][].

This fork adds a contextual `given` operator for conditional probability:

```python
y = 2*x given x >= 5 and not x > 9
```

`given` binds less tightly than arithmetic, comparisons, `not`, `and`, and
`or`, but more tightly than conditional expressions and lambdas. The example
groups as `(2*x) given ((x >= 5) and (not (x > 9)))`. Conditions accept general
expressions; validating and evaluating them is the runtime's responsibility.
The parser produces a `given_operator` node with `left`, `operator`, and `right`
fields.

Repeated conditioning requires parentheses: `(x given p) given q` or
`x given (p given q)`. To condition a whole conditional expression, write
`(x if flag else z) given p`. Existing identifiers named `given` remain valid.
This syntax extension does not add execution support to standard Python.

To regenerate the parser, install Node.js/npm and run `npm ci` followed by
`npx tree-sitter generate`. Run `npx tree-sitter test` to compile and test the
parser; this also requires a C compiler. Generated parser sources are committed
so binding consumers do not need to regenerate them.

[tree-sitter]: https://github.com/tree-sitter/tree-sitter

## References

- [Python 2 Grammar](https://docs.python.org/2/reference/grammar.html)
- [Python 3 Grammar](https://docs.python.org/3/reference/grammar.html)

[ci]: https://img.shields.io/github/actions/workflow/status/tree-sitter/tree-sitter-python/ci.yml?logo=github&label=CI
[discord]: https://img.shields.io/discord/1063097320771698699?logo=discord&label=discord
[matrix]: https://img.shields.io/matrix/tree-sitter-chat%3Amatrix.org?logo=matrix&label=matrix
[npm]: https://img.shields.io/npm/v/tree-sitter-python?logo=npm
[crates]: https://img.shields.io/crates/v/tree-sitter-python?logo=rust
[pypi]: https://img.shields.io/pypi/v/tree-sitter-python?logo=pypi&logoColor=ffd242
