# ID Generator

Generates secure IDs for people. Built for [Something New](https://somethingnew.org.uk) financial open data publishing.

### Anonymous IDs

Anonymous IDs consist of the first 10 characters of a salted SHA-512 hash of the name and email address.

### Public IDs

Public IDs consist of the given name, plus the anonymous ID above.

## Usage:

```
$ bundle

$ bundle exec ./generate anon "James Smith" james@floppy.org.uk ChauJe6dee6foo3sheeXag6Uu
>> d17397628f

$ bundle exec ./generate public "James Smith" james@floppy.org.uk ChauJe6dee6foo3sheeXag6Uu
>> James Smith d17397628f
```

To avoid passing the salt every time, you can also put it in an a `ID_GENERATOR_SALT` environment variable:

```
$ export ID_GENERATOR_SALT=ChauJe6dee6foo3sheeXag6Uu

$ bundle exec ./generate public "James Smith" james@floppy.org.uk
>> James Smith d17397628f
```
