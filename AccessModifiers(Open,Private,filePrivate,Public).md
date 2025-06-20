## Open Vs Public:

* Public does not allow a class to be inherited in another module/target whereas Open does.
* Public method does not allow to be overridden in subclass in another module/target whereas Open does.
Apart from above both are same.

## Private Vs Fileprivate:
* (Within single file) Private does not allow to access (func and properties) in subclass whereas FilePrivate does.
* (Outside File) Private and FilePrivate both can't be accessible.

Private
Private access only in class and its extension(When extension is in the same .swift file).

File Private
File-private access only in class and its extension & subClass(When extension or subClass is in the same .swift file).


| Access Level  | Scope Description                                                            |
| ------------- | ---------------------------------------------------------------------------- |
| `open`        | Most permissive – accessible **and overridable** outside the module          |
| `public`      | Accessible **but not overridable** outside the module                        |
| `internal`    | Default – accessible anywhere **within the same module**                     |
| `fileprivate` | Accessible **only within the same source file**                              |
| `private`     | Accessible **only within the enclosing scope** (like class/struct/extension) |

✅ "Overridable" means:
You can override a method or property in a subclass (i.e., provide your own implementation that replaces the parent’s version).
