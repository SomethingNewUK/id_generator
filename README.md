# ID Generator

Generates secure IDs for people. Built for [Something New](https://somethingnew.org.uk) financial open data publishing.

## Why?

As the treasurer of an political party, I want to [publish all our finances as open data](https://somethingnew.org.uk/about/finances/). In this data, it's useful to be able to see who is making donations, how often, and of what size.

We ask if we can make donor names public, but no everyone wishes to do so, as is their right. Therefore for users of open data to be able to track donations over time, we need a stable identifier for individuals which is not relatable to their personal data.

We wish to avoid simply minting a random ID for each user, because in order to reuse those IDs, we will have to keep them in a database, which if leaked would allow donation details to be linked to real people.

Therefore we wish to generate IDs from the personal data using a fixed algorithm which does not rely on a data store, and which cannot be reversed to obtain the input data even if the algorithm and any keys used are known.

## ID format

### Anonymous IDs

Anonymous IDs consist of the first 10 characters of a salted SHA-512 hash of the name and email address.

We combine the data as "{name} <{email}> {salt}", generate a SHA-512 hex digest, and use the first 10 characters as the ID.

The salt is stored in a secure password database, but even if the salt is leaked the hashes could not be reverse engineered to obtain input data, though if possible input data was known it would be possible to verify if a person was a donor.

### Public IDs

Public IDs consist of the given name, plus the anonymous ID above. These are used where donors have given permission for their name to be published.

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
