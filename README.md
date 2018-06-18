# javascript-notebook
Notebook of Javascript Things to Remember


### Pad with Zeros:
```
function(number, pad) { 
  var result= String(number);
  while(result.length < (pad || 2)) result= "0" + result; 
  return result;
}
```

