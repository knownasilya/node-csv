---
language: en
layout: page
title: "Reading data from a source"
date: 2012-10-02T15:35:24.009Z
comments: false
sharing: false
footer: false
navigation: csv
github: https://github.com/wdavidw/node-csv
---


The `csv().from` property provide functions to read to a csv input 
like a string, a file, a buffer or a readable stream. You may call
the `from` function or one of its sub function. For example, here is
to identical way to read from a file:

```javascript

csv.from('/tmp/data.csv').on('data', console.log);
csv.from.path('/tmp/data.csv').on('data', console.log);
```


<a name="from"></a>`from(mixed)`
-------------

Read from any sort of source. A convenient function to discover the source to parse. If it is a string, then if check 
if it match an existing file path and read the file content, otherwise, it
treat the string as csv data. If it is an instance of stream, it consider the
object to be an input stream. If is an array, then for each line should correspond a record.

Here's some examples on how to use this function

```javascript

csv()
.from('"1","2","3","4","5"')
.on('end', function(){ console.log('done') })

csv()
.from('./path/to/file.csv')
.on('end', function(){ console.log('done') })

csv()
.from(fs.createReadStream('./path/to/file.csv'))
.on('end', function(){ console.log('done') })

csv()
.from(['"1","2","3","4","5"',['1','2','3','4','5']])
.on('end', function(){ console.log('done') })
```



<a name="from.options"></a>`from.options([options])`
-------------------------

Update and retrieve options relative to the input source. Return 
the options as an object if no argument is provided.

*   `delimiter`   Set the field delimiter, one character only, defaults to comma.
*   `quote`       Set the field delimiter, one character only, defaults to double quotes.
*   `escape`      Set the field delimiter, one character only, defaults to double quotes.
*   `columns`     List of fields or true if autodiscovered in the first CSV line, default to null. Impact the `transform` argument and the `data` event by providing an object instead of an array, order matters, see the transform and the columns sections for more details.
*   `flags`       Used to read a file stream, default to the r charactere.
*   `encoding`    Encoding of the read stream, defaults to 'utf8', applied when a readable stream is created.
*   `trim`        If true, ignore whitespace immediately around the delimiter, defaults to false.
*   `ltrim`       If true, ignore whitespace immediately following the delimiter (i.e. left-trim all fields), defaults to false.
*   `rtrim`       If true, ignore whitespace immediately preceding the delimiter (i.e. right-trim all fields), defaults to false.


<a name="from.array"></a>`from.array(data, [options])`
------------------------------

Read from an array. Take an array as first argument and optionally 
some options as a second argument. Each element of the array  
represents a csv record. Those elements may be a string, a buffer, an
array or an object.


<a name="from.string"></a>`from.string(data, [options])`
-------------------------------

Read from a string or a buffer. Take a string as first argument and 
optionally an object of options as a second argument. The string 
must be the complete csv data, look at the streaming alternative if your 
CSV is large.


<a name="from.path"></a>`from.path(path, [options])`
----------------------------

Read from a file path. Take a file path as first argument and optionally an object 
of options as a second argument.


<a name="from.stream"></a>`from.stream(stream, [options])`
--------------------------------

Read from a stream. Take a readable stream as first argument and optionally 
an object of options as a second argument.
