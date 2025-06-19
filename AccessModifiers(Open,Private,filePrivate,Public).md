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
