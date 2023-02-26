# Problem

Steep cannot find method definition if the parent module has the same name as the child's name.

# Reproduce

`steep check` should not report any errors, but it reports an error.

```console
$ bundle install
$ bundle exec steep check
# Type checking files:

............................................................................F.....

test.rb:4:6: [error] Type `(::Object & ::M)` does not have method `bar`
│ Diagnostic ID: Ruby::NoMethod
│
└       bar
        ~~~

Detected 1 problem from 1 file
```

# Additional information

`rbs method` looks sane.

```console
$ rbs -I . method M::M bar
::M::M#bar
  defined_in: ::M::M
  implementation: ::M::M
  accessibility: public
  types:
      () -> void

$ rbs -I . method M::M2 bar
::M::M2#bar
  defined_in: ::M::M2
  implementation: ::M::M2
  accessibility: public
  types:
      () -> void
```
