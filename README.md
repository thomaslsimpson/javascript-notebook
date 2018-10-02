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

### Execute in Promise in series with done Promise
```
function execute_in_series(list, callback_with_promise){
    return new Promise((resolve, reject) => {
        list.reduce( (p,c, index, source_list) => {
            return p.then(() => {
                var cb_result=  callback_with_promise(c).then( () => { 
                    if(index >= (source_list.length -1)){
                        resolve();
                    }   
                }); 
                return cb_result;
            }); 
        }, Promise.resolve());
    }); 
}

execute_in_series([1,1.2,1.4,1.6], (t) => {
    return new Promise((resolve, reject) => {
        console.log(`>>>>> --- Test begin: ${t}`);
        setTimeout(() => {
           console.log(`<<<<< ---   Test complete: ${t}`);
           resolve();
        }, Math.floor(t * 1000));
    });
}).then( () => {
    console.log("All Done.");
});

```



