# Firestore Typescript Converter

By default, Firestore documents are untyped. This can be annoying when developing larger applications with lots of models.

This repository makes use of Firestore's converter feature to make the process easier for you without breaking the ideology behind it.

## Installation
```
yarn install firestore-typescript-converter
```

```
npm install firestore-typescript-converter
```

## Usage
First, create a converter for your model:

```typescript
type User = {
    firstName: string
    lastName: string
}

const UserConverter = firestoreConverter<User>()
```

That's it! Now you can use the converter wherever you use Firestore. For example:

```typescript
query(
    collection(getFirestore(), "profiles"),
    where("firstName", "==", "Bob")
).withConverter(ProfileConverter)
```

When calling `data()` on any of the documents resulting from this query, you will get a nice typed `User` object.

### Including IDs
It might be useful to include the `id` field in the "data" of the document, to allow you to reference a single object rather than a separate `id` and `data()`. This package makes it easy!

The `firestoreConverter` function takes a single optional argument, `includeID`. If true, the ID will be included in the data (returning `WithID<T>` instead of just `T`)

```typescript
const UserConverter = firestoreConverter<User>(true)
```

## License
MIT license
