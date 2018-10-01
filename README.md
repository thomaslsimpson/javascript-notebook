# javascript-notebook
Notebook of Javascript Things to Remember


### Left Pad with Zeros:
```
function(number, pad) { 
  var result= String(number);
  while(result.length < (pad || 2)) result= "0" + result; 
  return result;
}
```

### Execute asynchronous items in series
```
function waitabit(time){
    console.log(`Creating Promise for ${time}`);
    return new Promise((resolve, reject) => {
        console.log(`Start executing wait for ${time}`);
        setTimeout(() => {
            console.log(`done waiting for ${time} :: calling resolve()`);
            resolve(time);
        }, time);
    }); 
}

var wait_list= [2000,4000,1000,3000];

function execute_in_series(list, callback_with_promise){
    list.reduce( (p,c) => {
        return p.then(() => {
            return callback_with_promise(c);
        }); 
    }, Promise.resolve());
}

execute_in_series(wait_list, waitabit);
```

