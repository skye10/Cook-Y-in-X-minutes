### Work with dates in Javascript

#### Problem

You want to read, write and manipulate dates in Javascript

#### Assumptions
* [Node.js](https://nodejs.org/en/) is installed in your system

#### References
* Mozilla documentation on [Dates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)


***

#### Recipes

##### Now

```javascript
x = Date.now(); // Returns milliseconds from Unix epoch 1970-01-01T00:00:00Z
```

##### Current date/time

```javascript
x = new Date(); // Current datetime object in UTC
x.toLocaleString(); // String output in current locale timezone (e.g. Dallas)
x.toLocaleDateString(); // Date portion
x.toLocaleTimeString(); // Time portion
x.getTimezoneOffset(); // Minutes offset between UTC and locale
x1 = new Date(); // Current datetime in UTC
x1 - x; // Time difference in milliseconds
```

##### Specify a date/time

```javascript
x = new Date(); // Current datetime
x = new Date(0); // 1970 epoch - Midnight, Jan 1st, 1970, GMT
x = new Date(1); // 1 millisecond after epoch (Can be negative)
x = new Date("2020-09-10T00:12:12Z"); // 2020-09-10-T00:12:12Z
// All dates the same below
x = new Date("2020-09-10"); // 2020-09-10T05:00:00.000Z (UTC midnight!)
x = new Date("10 Sept, 2020"); // 2020-09-10T05:00:00.000Z (UTC midnight!)
x = new Date("Sept 10, 2020"); // 2020-09-10T05:00:00.000Z (UTC midnight!)
x = new Date("2020-09-10"); // 2020-09-10T05:00:00.000Z (UTC midnight!)
x = new Date("09/10/20"); // 2020-09-10T05:00:00.000Z (UTC midnight!)
```

> Note: Dates must be in the [RFC2822](https://tools.ietf.org/html/rfc2822#page-14) format.
>

##### Explicitly specify year, month, date

```javascript
// Note! Months start with 0, not 1
x = new Date(2020, 8, 10); // 2020-09-10T05:00:00.000Z (UTC midnight!)
```

##### Get year, month, date, etc

```javascript
x.getFullYear(); // 2020
x.getMonth(); // 8
x.getDate(); // 10
x.getDay(); // 4 (0=Sunday)
x.getHours(); // 5
x.getMinutes(); // 0
x.getSeconds(); // 0
x.getMilliseconds(); // 0

// UTC versions
x.getUTCFullYear(); // 2020
x.getUTCMonth(); // 8
x.getUTCDate(); // 10
// etc ...
```

##### Set year, month, date, etc

```javascript
x.setFullYear(2021);
x.setMonth(11);
x.setDate(2);
x.setDay(1); 
x.setHours(5); 
x.setMinutes(30); 
x.setSeconds(30); 
x.setMilliseconds(1000);

// UTC versions
x.setUTCFullYear(2021); 
x.setUTCMonth(8);
x.setUTCDate(10);
// etc ...
```

