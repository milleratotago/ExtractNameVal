ExtractNameVal
==============

Tools for passing optional parameters and name/value pairs in MATLAB.
---------------------------------------------------------------------

This project provides a few simple functions that you can use
to parse optional parameters and name/value pairs within your own functions.
Here is a quick overview:

Features:
---------

<ul>
    <li>Parameter values can be of any type: numbers, strings, arrays, cells,...</li>
    <li>Your function controls the order in which parameters are checked;
        the order in which the parameters are specified in the call to your function
        does not matter.
    <li>You specify whether each parameter name is case-sensitive or case-insensitive.</li>
    <li>You specify a default value for each optional parameter, and the parameter
        is automatically set to its default value if it is not specified in the function call.</li>
    <li>You may specify multiple acceptable names for a single parameter (in case there are several names
        that make sense and you want to accept any of them).</li>
    <li>You can check parameter values to make sure they meet your criteria (via assertions).</li> ; 
</ul>

Example
-------

You write a function "foobar" that takes 2 required parameters (x, y).
Suppose you also want it to take some optional parameters, such as:
<ul>
    <li>A string switch, for example 'absolute'</li>
    <li>A name-value pair such as 'factor',10.4</li>
    <li>Another name-value pair such as 'directory','C:\Data'</li>
    <li>Another name-value pair such as 'filelist',{'file1' 'file2' 'file3'}</li>
    <li>A name-value pair specifying a 'posfactor' that must be greater than 0.</li>
    <li>and so on...</li>
</ul>

Here is approximately what your code would look like:

```matlab
function foobar(x,y,varargin)
% A function to illustrate parameter handling with ExtractNameVal.

CaseSensitive = true;

[abspresent, varargin] = ExtractName('absolute',varargin,CaseSensitive);
% abspresent will be set to true if foobar is called with the optional parameter:  'absolute';
% otherwise, abspresent will be set to false.

[factorval,  varargin] = ExtractNameVal('factor',-10,varargin,CaseSensitive);
% factorval will be set to X if foobar is called with the optional parameter pair:  'factor',X
% otherwise, factorval will be set to the specified default factorval of -10

[direcval,   varargin] = ExtractNameVal('directory','',varargin,CaseSensitive);
% direcval will be set to X if foobar is called with the optional parameter pair:  'directory',X
% otherwise, direcval will be set to the specified default direcval of '' (an empty string)

[filelistval,varargin] = ExtractNameVal('filelist',{},varargin,CaseSensitive);
% filelistval will be set to X if foobar is called with the optional parameter pair:  'filelist',X
% otherwise, filelistval will be set to the specified default filelistval of {} (an empty cell array)

[posfactorval,  varargin] = ExtractNameVal('posfactor',1,varargin,CaseSensitive,'x>0');
% posfactorval will be set to X if foobar is called with the optional parameter pair:  'posfactor',X
% otherwise, posfactorval will be set to the specified default posfactorval of 1.
% The final value of posfactor will be checked to make sure it is greater than zero.



% Note that parameters are removed from varargin as they are processed,
% so you can check for unrecognized parameters at the end.
if numel(varargin)>0
   warning('Not all varargin parameters were handled!');
end

% Your function code goes here...

end
```

