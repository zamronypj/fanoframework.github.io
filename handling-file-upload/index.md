---
title: Handling File Upload
description: Tutorial on how to work with file upload in Fano Framework
---

<h1 class="major">Handling file upload</h1>

If you have form like following snippet

```
<form action="/submit" method="post" enctype="multipart/form-data">
    <input type="file" name="myFile">
    <button type="submit">Submit</button>
</form>
```

To retrieve file uploaded by client, you need to call `getUploadedFile()` method from `IRequest` interface. It returns data of type `IUploadedFileArray` which array of `IUploadedFile` instance. Please read [Working with request](/working-with-request) for information how to work with request object.


```
var myFile : IUploadedFileArray;
...
myFile := request.getUploadedFile('myFile');
```

Client can send one or more file with same name, for example:

```
<form action="/submit" method="post" enctype="multipart/form-data">
    <input type="file" name="myFile">
    <input type="file" name="myFile">
    <button type="submit">Submit</button>
</form>
```

If client upload one or more files, `length(myFile)` will indicates how many
files actually uploaded.

## Move uploaded file

Initially, uploaded file will be stored in system temporary directory. You need to
call `moveTo()` methods to move into permanent location.

```
if (length(myFile) > 0) then
begin
    myFile[0].moveTo(targetUploadPath);
end;
```
`targetUploadPath` is full filename (including its target directory). You must make sure that `targetUploadPath` is writeable. Exception `EInOutError` is raised when
uploaded file can not be written to target path.

If you do not call `moveTo()`, at the end of request handling, temporary uploaded file will be deleted.

## Get uploaded file size

Size of uploaded file in octet (or bytes) can be queried with `size()` method.

```
var fSize : int64;
...
fSize := myFile[0].size();
```

## Get file MIME type

MIME type of uploaded file can be queried with `getClientMediaType()` method.
For example, if upload JPEG image, you may get `image/jpeg`.

```
var mime : string;
...
mime := myFile[0].getClientMediaType();
```

If client does not send any MIME type (aka Content Type) then it is assumed
`application/octet-stream`.

## Get original file name

To get original file name of uploaded file use `getClientFilename()` method.

```
var filename : string;
...
filename := myFile[0].getClientFilename();
```

If client does not send filename then it returns empty string.

## File Upload Validation

Fano Framework validation feature provides several built-in validation rules you can use to [validate against file upload](/security/form-validation/built-in-validation-rules#uploaded-file), such as, to verify that field is indeed a file upload, to verify that file upload match certain MIME type or more advanced use, such as, antivirus scan validation or file format validation.

## Example demo

For example application that demonstrates how to handle file upload with Fano Framework, see
[Fano Upload](https://github.com/fanoframework/fano-upload).
While [Fano Scgi Upload example](https://github.com/fanoframework/fano-scgi-upload) shows how to validate file being uploaded using various validation rules.

## Explore more

- [Working with response](/working-with-response)
- [Working with request](/working-with-request)
- [Form Validation](/security/form-validation)
