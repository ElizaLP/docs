# Server Access
# Server Management for Accessing Scriptable Objects

:::info
Some functions require a **PlayerID**, so ensure you have access to this if needed. See the below methods to find which ones need this field.
:::

The server can access all methods to do with tag management, these are as listed below:
- addTag(instance: Instance, tag: string as Tag, ownerUserId: number)
- removeTag(instance: Instance, tag: Tag as string)
- removeAllTags(instance: Instance)
- getByTag(tag: Tag): Set(Instance)
- getByOwner(userId: number): Set(Instance)
- getByTagAndOwner(tag: Tag, userId: number): Set(Instance)

Unlike the client, the server is given all values that match the given criteria, allowing for more manipulation of values. The downside to this is that to access 1 value, you still need to sift through every value as if it is in an array.

The way recommended is to setup a definite assignment assertion variable (format let x!: type;), then call the required function, then loop through every item and set the definite to the required value.

:::info Why definite assignment assertion?
The reason for this variable is to satisfy the type fail-safe on TypeScript. Essentially we are saying that this variable is currently **not** defined, but before it gets to you, it **will** be defined (which in our use case here, we can almost guarantee it will be)

Read more [**on the TS Docs**](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-7.html)
:::

## Example
Taken directly from the TrainSpawner.ts file, this is how the "Hitbox" tag is accessed and used.

```ts title='TrainSpawner.ts'
let hitboxPart!: BasePart;
const hitboxSet = this.PartTagManager.getByTagAndOwner("Hitbox", userID);

for (const item of hitboxSet) {
	if(item.IsA("BasePart")) {
		hitboxPart = item;
		break;
	}
}
```

Provided the tag is correct and accessible, the variable should resolve into the BasePart requested.
Note the **casting** taking place.

The same idea should replicate to all the functions that return a **Set**.


_This is all the planned code for this section, if anything else is missing that might be required, make it known clearly._