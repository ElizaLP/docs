# Client Access
# Client Management for Accessing Scriptable Objects

:::warning WARNING: UNSAFE CODE
This area contains code which could be an entrypoint for exploiters. Please ensure this is fully checked before released - bop
:::

As the management system for accessing Scriptable Objects is fully done on the server, you need to use the RemoteFunction registered as below:

```ts
    tag.getByTagAndOwner: remote<Server, [tag: string, owner: number]>...
```

**The only method accessible by the client is getByTagAndOwner. This will be expanded if necessary.**

Compared to the server, the client is only able to access the first item returned from the server instead of all, reducing risk of access to exploit (the client theoretically should only need 1 item from the server anyways at a time)

This makes writing into this easier, as all you need to do is simply call the remote function, and **cast** to your specific object type.

:::info
All items returned are **Instances**, and will therefore need to be cast. Failure to do so can cause an error.
:::

## Example
Taken directly from the TrainController.ts file, this is how the "DriverSeat" tag is accessed and used.

```ts title='TrainController.ts'
let seat: VehicleSeat = await Network.tag.getByTagAndOwner("DriverSeat", Players.LocalPlayer.UserId) as VehicleSeat;
```

Provided the tag is correct and accessible, the variable should resolve into the VehicleSeat requested.
Note the **casting** taking place.


_This is all the planned code for this section, if anything else is missing that might be required, make it known clearly._