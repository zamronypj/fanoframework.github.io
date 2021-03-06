---
title: Working with Models
description: Tutorial on how to work with models in Fano Framework
---

<h1 class="major">Working with Models</h1>

## Read-only model

Model is a object that encapsulate data. In Fano framework, model that can only be used to read data is encapsulate in `IModelReader` interface and model that write data implements `IModelWriter` interface.

`IModelReader` has two methods that implementor class must provide:

```
(*!----------------------------------------------
 * read data from storage
 *-----------------------------------------------
 * @param params parameter for search/filtering
 * @return model data
s         *-----------------------------------------------*)
function read(const params : IModelParams = nil) : IModelResultSet;

(*!----------------------------------------------
 * return data instance after read() is execute
 *-----------------------------------------------
 * @return model data
 *-----------------------------------------------*)
function data() : IModelResultSet;
```
Fano Framework does not have built-in implementation of both interface as they
may be specific to application need.

## Write-only model

In Fano framework, model that can only be used to write data implements `IModelWriter` interface.

`IModelWriter` has two methods that implementor class must provide:

```
(*!----------------------------------------------
 * write data to storage
 *-----------------------------------------------
 * @param params parameters related to data being stored
 * @param data data being stored
 * @return current instance
 *-----------------------------------------------*)
function write(const params : IModelParams; const data : IModelParams) : IModelWriter;
```
Fano Framework does not have built-in implementation of both interface as they
may be specific to application need.

## Read write model

To make class, can read and write data, you need to implements both interface.

```
type
    TExampleModel = class(TInterfacedObject, IModelReader, IModelWriter)
    public
        //implements all interface methods here
    end;
```

## Model result set

After model read data from storage, it returns instance of `IModelResultSet` interface instance. Data can be accessed through this interface which has several methods:

- `count()` returns number of data currently in result set.
- `eof()` returns if current cursor pointer is at the end of result set.
- `next()` advances current cursor pointer to next data.
- `readString()` read data as string.

## Display model data in View

See [Working with Views](/working-with-views) to understand how model can be used inside `IView` instance.

## Explore more

- [Working with Controllers](/working-with-controllers)
- [Working with Views](/working-with-views)
