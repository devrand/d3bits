## Collections

### each(array)
```js
[1, 2, 3].forEach(function(num) { alert(num); });  // Vanilla equivalent
```

### each(object)
D3 equivalent using d3.values (d3.entries and d3.map forEach would also work):
```js
d3.values({one: 1, two: 2, three: 3}).forEach(function(num) { alert(num); });
```

### map(array)
```js
[1, 2, 3].map(function(num) { return num * 3; }); // Vanilla equivalent
```

### map(object)
D3 equivalent with d3.values (d3.entries and d3.map values.map would also work):
```js
d3.values({one: 1, two: 2, three: 3}).map(function(num) { return num * 3; });
```

### reduce
```js
var sum = [1, 2, 3].reduce(function(memo, num) { return memo + num; }, 0); // Vanilla equivalent
```

### reduceRight
Given:
```js
var list = [[0, 1], [2, 3], [4, 5]];
```

```js
var flat = list.reduceRight(function(a, b) { return a.concat(b); }, []); // Vanilla equivalent
```

### find

There’s no proper Vanilla equivalent of Underscore’s find method, but you can approximate it with array.filter. This is typically slower because it doesn’t stop once the first match is found:
```js
var even = [1, 2, 3, 4, 5, 6].filter(function(num) { return num % 2 == 0; })[0];
```

A closer approximate is array.some, but this is less convenient because it requires the closure to set an enclosing variable:
```js
var even; [1, 2, 3, 4, 5, 6].some(function(num) { return num % 2 == 0 && (even = num, true); });
```

### contains
```js
[1, 2, 3].indexOf(3) >= 0; // Vanilla equivalent
```

### invoke
```js
[[5, 1, 7], [3, 2, 1]].forEach(function(array) { array.sort(); }); // Vanilla equivalent
```
Note: JavaScript’s built-in array.sort sorts *lexicographically* rather than numerically; you almost always want to say `array.sort(d3.ascending)`, or `array.sort(function(a, b) { return a - b; })` if you know you’re sorting numbers or dates.

### pluck
Given:
```js
var stooges = [{name: "moe", age: 40}, {name: "larry", age: 50}, {name: "curly", age: 60}];
```
```js
stooges.map(function(stooge) { return stooge.name; }); // Vanilla equivalent
```

### max
Given:
```js
var stooges = [{name: "moe", age: 40}, {name: "larry", age: 50}, {name: "curly", age: 60}];
```
Vanilla equivalent. You can omit the null argument if you know that stooges is non-empty or you’d prefer a TypeError:
```js
stooges.reduce(function(p, v) { return v.age > p.age ? v : p; }, null);
```
Using d3.max is not exactly equivalent because it returns the maximum value, rather than the corresponding object. Also, d3.max ignores null, undefined and NaN values. Often, this is what you want:
```js
d3.max(stooges, function(stooge) { return stooge.age; });
```

### min
Given:
```js
var numbers = [10, 5, 100, 2, 1000];
```
```js
numbers.reduce(function(p, v) { return Math.min(p, v); }, Infinity); // Vanilla equivalent
```

Using d3.min (not equivalent; see above regarding d3.max):
```js
d3.min(numbers);
```

### sortBy
```js
[1, 2, 3, 4, 5, 6].sort(function(a, b) { return Math.sin(a) - Math.sin(b); }); // Vanilla equivalent
```
In the vanilla equivalent, the comparator is invoked once per comparison rather than once per element; thus the vanilla version is potentially slower. More critically, array.sort doesn’t support nondeterministic comparators. You could fix that with a temporary array holding the mapped values, a second temporary array holding the indexes, and d3.permute:
```js
var array = [1, 2, 3, 4, 5, 6], sin = array.map(Math.sin);
d3.permute(array, d3.range(array.length).sort(function(i, j) { return sin[i] - sin[j]; }));
```

### groupBy

Underscore example:
```js
_.groupBy([1.3, 2.1, 2.4], function(num){ return Math.floor(num); });
```
D3 equivalent:
```js
d3.nest().key(Math.floor).map([1.3, 2.1, 2.4]);
```

Underscore example:
```js
_.groupBy(["one", "two", "three"], "length");
```

D3 equivalent:
```js
d3.nest().key(function(d) { return d.length; }).map(["one", "two", "three"]);
```

D3’s nest operator supports more than one level of grouping, and can also return nested entries that preserve order.

### countBy
Underscore example:

```js
_.countBy([1, 2, 3, 4, 5], function(num) {
  return num % 2 == 0 ? "even" : "odd";
});
```
D3 equivalent using nest.rollup:
```js
d3.nest()
    .key(function(num) { return num % 2 == 0 ? "even" : "odd"; })
    .rollup(function(values) { return values.length; })
    .map([1, 2, 3, 4, 5]);
```

### shuffle

D3 equivalent:
```js
d3.shuffle([1, 2, 3, 4, 5, 6]);
```

### toArray

Underscore example:

```js
(function(){ return _.toArray(arguments).slice(1); })(1, 2, 3, 4);
```

Vanilla equivalent:
```js
(function(){ return [].slice.call(arguments, 1); })(1, 2, 3, 4);
```

### size
Vanilla equivalent using Object.keys:
```js
Object.keys({one: 1, two: 2, three: 3}).length;
```

D3 equivalent using d3.keys:
```js
d3.keys({one: 1, two: 2, three: 3}).length;
```

D3 equivalent using d3.map, if you want to perform other operations:
```js
d3.map({one: 1, two: 2, three: 3}).keys().length;
```

## Array Functions

### first
Given:
```js
var numbers = [5, 4, 3, 2, 1];
```
Vanilla equivalent when no *n* is specified:
```js
numbers[0];
```
Vanilla equivalent when *n* is specified:
```js
numbers.slice(0, n);
```

### initial

Given:

```js
var numbers = [5, 4, 3, 2, 1];
```

Vanilla equivalent when no *n* is specified:
```js
numbers.slice(0, numbers.length - 1);
```
Vanilla equivalent when *n* is specified:
```js
numbers.slice(0, numbers.length - n);
```

### last

Given:
```js
var numbers = [5, 4, 3, 2, 1];
```

Underscore example:

Vanilla equivalent when no *n* is specified:
```js
numbers[numbers.length - 1];
```

Vanilla equivalent when *n* is specified:
```js
numbers.slice(numbers.length - n);
```

### rest, tail, drop

Given:

```js
var numbers = [5, 4, 3, 2, 1];
```

Underscore example:

```js
_.rect(numbers);
```

Vanilla equivalent when no *n* is specified:

```js
numbers.slice(1);
```

Vanilla equivalent when *n* is specified:

```js
numbers.slice(n);
```

### compact
Vanilla equivalent:

```js
[0, 1, false, 2, '', 3].filter(function(d) { return d; });
```

### flatten

TODO …

```js
_.flatten([1, [2], [3, [[4]]]]);
_.flatten([1, [2], [3, [[4]]]], true);
```

### without

TODO …

```js
_.without([1, 2, 1, 0, 3, 1, 4], 0, 1);
```

### union

TODO …

```js
_.union([1, 2, 3], [101, 2, 1, 10], [2, 1]);
```

### intersection

TODO …

```js
_.intersection([1, 2, 3], [101, 2, 1, 10], [2, 1]);
```

### difference

TODO …

```js
_.difference([1, 2, 3, 4, 5], [5, 2, 10]);
```

### uniq

Underscore example:

```js
_.uniq([1, 2, 1, 3, 1, 4]);
```

D3 equivalent for strings:

```js
d3.set(["1", "2", "1", "3", "1", "4"]).values();
```

TODO equivalent for non-string values

### zip

Underscore example:

```js
_.zip(['moe', 'larry', 'curly'], [30, 40, 50], [true, false, false]);
```

D3 equivalent:

```js
d3.zip(['moe', 'larry', 'curly'], [30, 40, 50], [true, false, false]);
```

### object

TODO …

```js
_.object(['moe', 'larry', 'curly'], [30, 40, 50]);
```

### indexOf

TODO … Vanilla array.indexOf

### lastIndexOf

TODO … Vanilla array.lastIndexOf

### sortIndex

TODO … d3.bisect

### range

Underscore example:

```js
_.range(10);
_.range(1, 11);
_.range(0, 30, 5);
_.range(0, -10, -1);
_.range(0);
```

D3 equivalent:

```js
d3.range(10);
d3.range(1, 11);
d3.range(0, 30, 5);
d3.range(0, -10, -1);
d3.range(0);
```

## Function (uh, ahem) Functions

…
