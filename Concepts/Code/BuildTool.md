# Build Tool
BuildTool is a extenable class game uses to define build tools the player can use. Only one build tool can be active at the time. Each tool has references to Player and its controller and camera, PlayerActionBuild.
Has helper method that make reading from game state easier
```cs
public void _Init(GameData _gameData)
```
Initalizes variables, creates buildPreviews list. Registers events.

```cs
public void _Free()
```
Free all used variables

```cs
public void _Open()
```
This method is called after this tool is enabled.

```cs
public void _Close()
```
This method is called after this tool is disabled.

```cs
public void _GameTick(long time)
```
Main game tick for tool.  Makes raycast to find where the player is looking. Calls `_OnTick(long time)` method

```cs
public virtual bool DetermineActive()
```
This is the method that determines which build tool should be active

```cs
protected virtual void _OnInit() // Init the tool

protected virtual void _OnFree() // Free used variables

protected virtual void _OnRegEvent() // Register to event calls

protected virtual void _OnUnregEvent() // Clear registered events

protected virtual void _OnOpen() // Called when player enables the tool

protected virtual void _OnClose() // Called when tool is disabled

protected virtual void _OnTick(long time) // Called every tick if the tool is enabled

public virtual void UpdatePreviewModels(BuildModel model)

public virtual void UpdatePreviewModelConditions(BuildModel model)

public virtual void EscLogic()

public virtual void NotifyBuilt(int preObjId, int postObjId) // Called when an entity is built

public virtual void NotifyDismantled(int objId) // Called when an entity is dismantled
```
These methods are supposed to be overriden by extending class to create new behavior.

```cs
public virtual void SetFactoryReferences()
```
Ensures that `factory` points to current factory.

```cs
public virtual void UpdateCollidersForCursor()
```
Updates collider for player cursor

```cs
public virtual void UpdateGizmos(BuildModel model)
```
In this method tool ensures that all gizmos are setup properly. Also supposed to be overriden

```cs
public void GetOverlappedObjectsNonAlloc(Vector3 pos, float objSize = 0f, float areaSize = 10f, bool ignoreAltitude = false)
```
Using Near Collider Logic finds all objects in an area.

```cs
public void GetOverlappedVeinsNonAlloc(Vector3 pos, float objSize = 0f, float areaSize = 10f)
```
Using Near Collider Logic finds all veins in an area.

```cs
public ItemProto GetItemProto(int objId)
```
Get ItemProto for this entity

```cs
public PrefabDesc GetPrefabDesc(int objId)
```
Get PrefabDesc for this entity

```cs
public int GetBeltInputCount(int _objId)
```
Gets amount of belts that are inputing to this belt

```cs
public int GetBeltConnCount(int _objId)
```
Gets amount of belts that are connected to this belt

```
public Pose GetBeltInputBeltPose(int _objId, out bool hasInput)
```
Tries to get Pose of a belt that inputs to this belt. If successful `hasInput` is set to `true`

```cs
public Pose GetBeltOutputBeltPose(int _objId, out bool hasOutput)
```
Tries to get Pose of a belt that this belt outputs to. If successful `hasOutput` is set to `true`

```cs
public Pose[] GetLocalPorts(int objId)
```
Gets all port (direct belt connection) Poses for this entity

```cs
public Pose[] GetLocalSlots(int objId)
```
Gets all slot (sorter connections) Poses for this entity

```cs
public Pose GetObjectPose(int objId)
```
Get pose of this entity

```cs
public Pose GetObjectPose2(int objId)
```
Get second pose of this entity. Used by Inserters


public void GetInserterT1T2(int objId, out bool t1, out bool t2)
{
	t1 = false;
	t2 = false;
	if (!this.ObjectIsInserter(objId))
	{
		return;
	}
	if (objId == 0)
	{
		return;
	}
	if (objId <= 0)
	{
		bool flag;
		int num;
		int num2;
		this.factory.ReadObjectConn(objId, 0, out flag, out num, out num2);
		int num3;
		this.factory.ReadObjectConn(objId, 1, out flag, out num3, out num2);
		if (num3 != 0 && !this.ObjectIsBelt(num3))
		{
			t1 = true;
		}
		if (num != 0 && !this.ObjectIsBelt(num))
		{
			t2 = true;
		}
		return;
	}
	int inserterId = this.factory.entityPool[objId].inserterId;
	if (inserterId == 0)
	{
		return;
	}
	t1 = this.factory.factorySystem.inserterPool[inserterId].t1 != 0;
	t2 = this.factory.factorySystem.inserterPool[inserterId].t2 != 0;
}

```cs
public int GetObjectProtoId(int objId)
```
Get entity ItemProto id.


```cs
public bool ObjectIsBelt(int objId)
```
Is this entity a belt

```cs
public bool ObjectIsSplitter(int objId)
```
Is this entity a splitter

```cs
public bool ObjectIsPowerNode(int objId)
```
Is this entity a power node

```cs
public bool ObjectIsInserter(int objId)
```
Is this entity a sorter