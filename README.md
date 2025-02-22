# `<lang>`
> My language that I have yet to make a proper name for.

`<lang>` is a low-level, purely-functional, strictly-typed with a focus on developer control.
It is not meant to be an introductory language, but hopes to have as low of a learning curve
as possible for a low-level functional language.

## Implementation

The following text is idealistic and is bound to change as the language is implemented. As of writing this,
the grammer for `<lang>` is still being decided and development has yet to start.

## `"Welcome Back, World!"`

As we do with all introductions to new programming languages, let's start with `"Hello, World!"` (with type inference):

```rust
// hello-world.lang

^entry = hello-world;

let std = import std;

let hello-world =
| "Hello, World!"
| std.io.print
;
```

As can be seen above, `<lang>` takes inspiration from a multitude of languages. Each `.lang` file declares
it's own _module_ that serves as a namespace for it's members. The members of a module are made up of constants,
more familiarly variables -- though `<lang>` has no mutable-state, that can be anything from an unsigned-integer
to a partially-applied function.

Our `"Hello, World!"` module starts with an `^entry` assignment to declare the entrypoint of this module. 
`^`-symbol prefixed constants are _reserved module variables_ (_reserves_) that are _undefined at declaration_ 
-- and therefore unusable until assignment. If `<lang>` is designated to run this module as the `root` module 
of a program, it looks to the value of `^entry` an procedes with execution from there. All `^`s are implicitly 
assigned after module evaluation if they were not specified in the module. Besides `^entry` -- which is required
for `root` modules, all other reserves do not need to be assigned in both `root` and `library` modules and have 
inferred defaults. The module above can be rewritten without the module system as:

```rust
// hello-world-without-modules.lang

let ^entry: ||;
// other ^_ declarations.

^entry = hello-world;

let std = import std;

let hello-world =
| "Hello, World!"
| std.io.print
;

// assignment of other ^_ declarations
```

The module system is an example of a _compilation layer_ (_CL_), which are functions that take in lexed tokens and return 
a transformation of them. CLs are extremely powerful and several are enabled by default:

- `type-inference` - Allows types to be elided and inferred by this complitation layer.
- `imports` - Allows programs to be split across files.
- `modules` - As mentioned above.

The modularization of the compiler is to allow for the base compiler to be kept as small as possible, for the simple fact
that the `<lang>` compiler is not installed globally on a system. Rather, the `<lang>` cli is used to bootstrap projects
which include a stable, bootstrapping compiler, as well as the source code.
