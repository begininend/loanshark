# Introduction #

Here are a couple of examples on how you might use LoanShark.


# Details #

The interface of a LoanShark object pool is:

```
function borrowObject():*;

function returnObject(object:*):void;

function get size():int;

function get unused():int;

function get used():int;

function get ObjectClass():Class;

function clean():void;

function flush(force:Boolean = false, disposeUnusedObjects:Boolean = false):void;

function dispose():void;

function addEventListener(type:String, listener:Function, useCapture:Boolean = false, priority:int = 0, useWeakReference:Boolean = false):void;

function removeEventListener(type:String, listener:Function, useCapture:Boolean = false):void;
```

You could use LoanShark to create a pool of Bitmaps, which all wrap the same BitmapData, by default:

```
// Given any BitmapData
var bitmapData:BitmapData;

// Create a pool a Bitmap objects, with your bitmapData as the default init object
var pool:LoanShark = new LoanShark(Bitmap, false, 0, 0, bitmapData);

// You can get as many object from the pool as necessary
var bitmap:Bitmap = pool.borrowObject();
addChild(bitmap);

// When done with objects, recycle them back into the pool
pool.returnObject(removeChild(bitmap));
```