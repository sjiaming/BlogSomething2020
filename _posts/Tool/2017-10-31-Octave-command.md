---
layout: article
title: Basic Octave Commands
description: Some basic commands of Octave
imgsrc: assets/pics/tools/octave.jpg
banner: assets/pics/tools/octave_banner.jpg
date: 2017-10-31
category: Tool
tags: [Octave, Cheatsheet]
author: Song Jiaming
---
Octave is a mathematical programming language. It is a good alternative to Matlab.<br>
In this blog, I will list down some basic but useful commands of it.



### 0. Global Operations

| Description | Commands | Example/Remark |
| ---------   | :------: | ------- |
| <b>Show \>\> </b>     | PS1('\>\>')|   -     |
| <b>Help</b> | help eye | Get description for eye function|
| <b>Show path</b>  | pwd | where you currently at |
| <b>Show files</b>  | ls | list all directories in this file |
| <b>Move to a file</b>  | cd 'File Path | Go to the destinated directory |
| <b>Load data file</b>  | load xxx.dat == load('xxx.dat') | - |
| <b>Show varables</b>  | who | varaibles I have in current scope |
| <b>Show varables 2</b>  | whos | view more details |
| <b>User input</b>  | input(''); | name=input('SJM'); |
| <b>Clear</b>  | clear | - |
| <b>Save</b>  | save hello.mat v | Save v into hello.mat (binary format) |
| <b>Save 2</b>  | save hello.txt v -ascii | human readable file  |


<br>
### 1. Basic Operations

| Description | Commands | Example/Remark |
| ---------   | :------: | ------- |
|   <b>Power</b>     |    ^     |   x^2   |
|   <b>Comment</b>   |    %     |    -    |
|  <b> Equal</b>     |   ==     |   1==2  |
|<b> Not equal</b>   |   ~=     |   1~=2  |
| <b>   And</b>      |   &&     |    -    |
| <b>   Or</b>       |   \|\|   |    -    |
|  <b>  XOR</b>      |  xor(m,n)     | xor(1,0)=1, xor(1,1)=0 |
| <b>Supress output</b> |  ;    | a=3; No output will be shown |
| <b>String</b>      |  ''      | b = 'hi'|
| <b>Pi</b>          |   pi     |   pi    |
|  <b>Print</b>      |  disp(a)    |  -   |
| <b>Printf</b>      |  | disp(sprintf('2 decimals: %0.2f',a)) |
| <b>Format</b>      | format long/short | How many digits to display  |
| <b>Histogram</b>  | hist(w)  | Histogram  |
| <b>Histogram 2</b> | hist(w,n) | hist(randn(10000,1),30) (30 columns)|


<br>
### 2. Create Data

| Description | Commands | Example/Remark |
| ---------   | :------: | ------- |
| <b>Row Vector</b>  |  [ ]     | [ 1 2 3 ]|
| <b>Column vector</b>| [;]   |  [1;2;3]  |
| <b>Matrix</b>      |   [space and ;]     | A = [1 2;3 4;5 6] |
| <b>Sequence</b>    | start:step:stop | 1:0.1:2 (2 is included)|
| <b>Matrix of 1</b> | ones(m,n)   |  ones(2,3) |
| <b>Matrix of 0</b> | zeros(m,n)  | zeros(2,3) |
| <b>Random number</b> | rand(m,n) | rand(2,3)  |
| <b>Random number 2</b>| rand(m,n)| values follows Gaussian Distribution|
|<b>Identity matrix</b>| eye(n)   | eye(4) |
| <b> Magic matrix</b> | magic(n) | nxn matrix with the same row/column/diag sum|
| <b>Lower Triangular</b>  | tril(A) | make A lower triangular |
| <b>Upper Triangular</b>  | triu(A) | make A upper triangular|



<br>
### 3. Manipulate Data

| Description | Commands | Example/Remark |
| ---------   | :------: | ------- |
| <b>Size </b>  |  size(A)     | A: Matrix|
| <b>Num of rows </b>| size(A,1)   |  1st dimension of A  |
| <b>Num of columns</b>      |   size(A,2)    | 2nd dimmension of A |
| <b>Length</b>    | length(v) | length of vector v|
| <b>Get an element</b>  | A(m,n) | element at row m col n |
| <b>Get a row</b>  | A(m,:) | all element along mth row |
| <b>Get a column</b>  | A(:,n) | all element along nth column |
| <b>Get rows</b>  | A([1 3],:) | all element from 1st and 3rd row  |
| <b>Append column</b>  | A = [A,[1;2;3]] | Append col at the end of A|
| <b>Flattern </b>  |  A(:) | put A into a single verctor(column by column)|
| <b>Concatenate</b>  | [A B] | concatenate A and B |
| <b>Concatenate 2</b>  | [A;B] | put B below A  |
| <b>Get part of array</b>  | v(1:10) | first 10 element of v |



<br>
### 4. Compute Data

| Description | Commands | Example/Remark |
| ---------   | :------: | ------- |
| <b>Multiplication</b> | * | A*B |
| <b>Multiply piecewisely</b> | .* | A.*B |
| <b>Divide piecewisely</b> | ./ | 1./v |
| <b>Log</b> | log(v) | - |
| <b>Exponential</b> | exp(v) | - |
| <b>Absolute</b> | abs(v) |  |
| <b>Transpose</b> | ' | A' |     
| <b>Max of vector</b> | max(v) | v is a vector |    
| <b>Max and its index</b> | [val, ind] = max(v) | val=max(v), ind = index of val |
| <b>Max of matrix</b> | max(A) | max of each col of A  |
| <b>Filter a vector with a critera</b> | v < n | if (the entry of v) < n, return 1, else 0 |
| <b>Filter a vector 2</b> | find(v < n) | show index of entries in v which are less than n |
| <b>Filter a matrix with a critera</b> | [r,c]=find(A>=n) | r=row index, c=col index, of the entry in A that is > n  |
| <b>Sum</b> | sum(v) | sum of all entries in v  |
| <b>Sum by column</b> | sum(A,1) | each column sum up of A |
| <b>Sum by row</b> | sum(A,2) | each row sum up of A |
| <b>Product</b> | prod(v) | product of all entries in v |
| <b>Floor</b> | floor(v) | floor of all entries |
| <b>Ceiling</b> | ceil(v) | ceiling of all entries |
| <b>Max between 2 matrices</b> | max(A,B) | take max of entry of A,B |
| <b>Column-wise max</b> | max(A,[],1) | column wise maximum of A |    
| <b>Row-wise max </b> | max(A,[],2) | row wise maximum of A  |  
| <b>Max of matrix</b> | max(max(A)) | - |
| <b>Flipping </b> | flipud(A) | 1230->0321  |
| <b>Pseudo inverse</b> | pinv(A) | - |



<br>
### 5. Plot Data

#### 5.1. Plot in the same figure:
Let y1 = sin(t)，y2 = cos(t)
1. plot a graph of y1 against t: `plot(t,y1)`
2. then plot the 2nd graph with red color: 
    * `hold on`
    * `plot(t, y2, 'r')`
3. set axis scale, x in [x1,x2] and y in [y1,y2]: `axis[x1,x2. y1,y2]`
4. label axis:
    - `xlabel('time')`
    - `ylabel('value')`
5. label graphs:
6. - `legend('sin', 'cos')`
7. figure title: `title('my plot')`
8. save this figure: `print -dpng 'myPlot.png'`
9. Close this figure: `close`
10. If you want to leave the window on but close the figure: `clf`

#### 5.2. Show figures separately:
1. figure(1); plot(t, y1)
2. figure(2); plot(t, y2)

#### 5.3. Subplots
- Divede plot a m x n grid: `subplot(m,n)`
- Divede plot a m x n grid and access ith subplot: `subplot(m,n,i)`

#### 5.4. Visualise a matrix
- Visualise A: `imagesc(A)`
- Show the colour scale and set theme colour:
    + `imagesc(A), colourbar, colormap gray;`
    + use ',': separete 3 commands (but write in 1 line)
    + use ';' separate 3 commands but doesn't show their results


<br>
### 6. Loop

#### 6.1 For Loop
```
for i = 1:10,
    v(i) = 2^i;
end;
```
Or,
```
indices = 1:10
for i=indices,
    disp(i)
end;
```

#### 6.2 While Loop
```
i=1;
while i<=5,
    v(i) =100;
    i=i+1;
end;
```
Or,
```
while true,
    v(i) = 999;
    I = i+1;
    if i==6,
        break;
    end;
end;
```

<br>
### 7. If-Else Statement
```
if v(1) ==1,
   statement;
elseif v(1) ==2,
   disp();
else
  statement;
end;
```
   
<br>
### 8. Code in a file
Below, nameOfFunction is the function name, x is the parameter.<br> 
This function returns y.
1. In the Scipt,
```Matlab
function y = nameOfFunction(x)
y=x^2;
end
```
2. Then go to the directory:<br>
    Enter: `nameOfFunction(2)` => ans = 4

Note: Let `twoValues()` be a function which returns 2 values [c,d]<br>
Then `[a,b] = twoValues()` gives a=c and b=d.

<br>

----
#### References
1. [Octave/Matlab Tutorial](https://www.coursera.org/learn/machine-learning/lecture/9fHfl/basic-operations), Andrew Ng 