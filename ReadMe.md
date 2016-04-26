ExtractNameVal
==============

Passing optional parameters and name/value pairs in MATLAB.
-----------------------------------------------------------

This project provides a few simple functions that you can use within your own functions
to check for optional parameters and to parse optional name/value pairs.
Here is a quick overview of how to use the functions in this project:

Examples
--------

You write a function "foobar" that takes 2 required parameters (x, y).
Suppose you also want it to take some optional parameters, such as:
<ul>
    <li>A string switch, for example 'absolute'</li>
    <li>A name-value pair such as 'factor',10.4</li>
    <li>Another name-value pair such as 'directory','C:\Data'</li>
    <li>Another name-value pair such as 'filelist',{'file1' 'file2' 'file3'}</li>
    <li>and so on...</li>
</ul>

Here is approximately what your code would look like:

```matlab
function foobar(x,y,varargin)
% A function to illustrate parameter handling with ExtractNameVal.

CaseSensitive = true;

[abspresent, varargin] = ExtractName('absolute',varargin,CaseSensitive);         % abspresent will be set to true if 'absolute' is in varargin
[factorval,  varargin] = ExtractNameVal('factor',-10,varargin,CaseSensitive);    %  -10 is the default factorval
[direcval,   varargin] = ExtractNameVal('directory','',varargin,CaseSensitive);  %  the empty string '' is the default direcval
[filelistval,varargin] = ExtractNameVal('filelist',{},varargin,CaseSensitive);   %  the empty cell array is the default filelistval

% Note that parameters are removed from varargin as they are processed,
% so you can check for unrecognized parameters at the end.
if numel(varargin)>0
   warning('Not all varargin parameters were handled!');
end

% Your function code goes here...
```

Additional features:
--------------------

<ul>
    <li>Parameter values can be of any type: numbers, strings, arrays, cells,...</li>
    <li>Parameters are checked in the order you specify within your function; it does not matter in what order they
        are specified in the call to your function.</li>
    <li>Parameter names can be case-sensitive or case-insensitive.</li>
    <li>Different parameter names can be treated as synonyms (in case you have trouble remembering what you called the parameter).</li>
    <li>Checking of parameter values can be enforced via assertions.</li>
    <li></li>
    <li></li>
</ul>

