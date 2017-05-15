# ID Generator

Generates secure IDs for people. Built for [Something New](https://somethingnew.org.uk) financial open data publishing.

### Anonymous IDs

Anonymous IDs consist of the first 10 characters of a salted SHA-512 hash of the name and email address.

### Public IDs

Public IDs consist of the given name, plus the anonymous ID above.

## Usage:

Pass name, email, and a salt value to the `anon` or `public` generators, then use the result instead of the name.

```
$ bundle

$ bundle exec ./generate anon "James Smith" james@example.com ChauJe6dee6foo3sheeXag6Uu
>> 8f6b0c9338

$ bundle exec ./generate public "James Smith" james@example.com ChauJe6dee6foo3sheeXag6Uu
>> James Smith 8f6b0c9338
```

To avoid passing the salt every time, you can also put it in an a `ID_GENERATOR_SALT` environment variable:

```
$ export ID_GENERATOR_SALT=ChauJe6dee6foo3sheeXag6Uu

$ bundle exec ./generate public "James Smith" james@example.com
>> James Smith 8f6b0c9338
```
