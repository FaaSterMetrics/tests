## WIP timing of printing on various platforms

This tests how long various combinations of "numbers of lines printed" with "characters per line" take.  
It takes 20 samples for each test and selects the one with the least execution time.

```js
const { PerformanceObserver, performance } = require('perf_hooks');


exports.handler = async (event) => {

    var print_num = 10000;
    
    var tested = [];

    for (var rep_char = 10; rep_char <= 10000; rep_char *= 10) {
        for (var rep_print = 10; rep_print <= 10000; rep_print *= 10) {
            tested.push( {"rep_char": rep_char, "rep_print": rep_print, "time": 10000000});
        }
    }
    

    for (var a = 0; a < 20; a++) {
        var ind = 0;

        for (var rep_char = 10; rep_char <= 10000; rep_char *= 10) {
            for (var rep_print = 10; rep_print <= 10000; rep_print *= 10) {
                var time = performance.now();
                for(var i = 0; i < rep_print; i++) {
                    var str = print_num++ + " " + "a".repeat(rep_char);
                    console.log(str);
                }
                time = performance.now() - time;
                if(time < tested[ind]["time"]) {
                    tested[ind] = {"rep_char": rep_char, "rep_print": rep_print, "time": time};
                }
                ind++;
            }
        }
    }

    // TODO implement
    const response = {
        statusCode: 200,
        body: JSON.stringify(tested),
    };
    return response;
};
```

## results:

AWS: 
```json
[
   {
      "rep_char":10,
      "rep_print":10,
      "time":0.05174200050532818
   },
   {
      "rep_char":10,
      "rep_print":100,
      "time":0.46276899985969067
   },
   {
      "rep_char":10,
      "rep_print":1000,
      "time":6.033760999329388
   },
   {
      "rep_char":10,
      "rep_print":10000,
      "time":217.97031100001186
   },
   {
      "rep_char":100,
      "rep_print":10,
      "time":0.05154599994421005
   },
   {
      "rep_char":100,
      "rep_print":100,
      "time":0.48639100044965744
   },
   {
      "rep_char":100,
      "rep_print":1000,
      "time":17.61947900056839
   },
   {
      "rep_char":100,
      "rep_print":10000,
      "time":236.61721100006253
   },
   {
      "rep_char":1000,
      "rep_print":10,
      "time":0.061091999523341656
   },
   {
      "rep_char":1000,
      "rep_print":100,
      "time":0.6947210002690554
   },
   {
      "rep_char":1000,
      "rep_print":1000,
      "time":23.366251000203192
   },
   {
      "rep_char":1000,
      "rep_print":10000,
      "time":338.66876700054854
   },
   {
      "rep_char":10000,
      "rep_print":10,
      "time":0.2007519993931055
   },
   {
      "rep_char":10000,
      "rep_print":100,
      "time":3.368088999763131
   },
   {
      "rep_char":10000,
      "rep_print":1000,
      "time":79.42832899931818
   },
   {
      "rep_char":10000,
      "rep_print":10000,
      "time":1022.2539029996842
   }
]
```
