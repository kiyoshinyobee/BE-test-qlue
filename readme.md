# Shell
1) 	`ps httpd | wc -l`
2) 	`for xx in mig33/inner.folder/*.txt; do mv $xx ${xx%.txt}.dat; done`


# SQL
1) 	Query 1
```SQL
SELECT 
		ANY_VALUE(DAY(date)) as 'day',
		ANY_VALUE(SUM(CASE WHEN score > 0 THEN score ELSE 0 END)) as 'num_pos_scores',
		ANY_VALUE(SUM(CASE WHEN score < 0 THEN score ELSE 0 END)) as 'num_neg_scores'
	FROM assessments
	WHERE date BETWEEN '2011-03-01' AND '2011-05-01'
	GROUP BY day
```
2) 	Query 2
```SQL
SELECT
		DAY(date),
		score
	FROM assessments
	where score > 0 AND date BETWEEN '2011-01-01' AND '2011-05-01'
```


# NodeJS, Python, Golang, or PHP
```javascript
function getPrimes(numb) {
	let listNumb = [],
	    primes = []

	// add all list number lower than numb
	for (let i = 0; i < numb; i++) {
		if (i > 1) {
			listNumb.push(i)
		}
	}

	// iteration list numb
	while (listNumb.length) {
		// add first numb from list numb to prime
		primes.push(listNumb.shift())
		// re-assign list numb = (filter list numb, remove item where modulus division with new item in prime is not 0)
		listNumb = listNumb.filter(i => i % primes[primes.length - 1] !== 0)
	}

	return primes
}
```


# Javascript
```javascript
const http = require('http'),
      rdc = {}

// generate keys
rdc.generateKeys = function(initial) {
  return new Promise((resolve) => {
    const lsKey = []

    for (let i = 0; i < initial.length; i++) {
      const itemKeys = Object.keys(initial[i])

      itemKeys.forEach((itemKey) => {
        if (!lsKey.includes(itemKey)) {
          lsKey.push(itemKey)
        }
      })
    }

    resolve(lsKey)
  })
}

// generate values
rdc.generateValues = function(initial, keys) {
  return new Promise((resolve) => {
    const lsValues = []

    for (let i = 0; i < initial.length; i++) {
      const itemValues = []

      keys.forEach((itemKey) => {
        if (initial[i][itemKey] !== undefined) {
          itemValues.push(initial[i][itemKey])
        } else {
          itemValues.push(null)
        }
      })

      lsValues.push(itemValues)
    }

    resolve(lsValues)
  })
}

// node server
http.createServer(async(req, res) => {
  const initial = [
          { username: 'ali', hair_color: 'brown', height: 1.2 },
          { username: 'marc', hair_color: 'blue', height: 1.4 },
          { username: 'joe', hair_color: 'brown', height: 1.7 },
          { username: 'zehua', hair_color: 'black', height: 1.8 },
        ],
        keys = await rdc.generateKeys(initial),
        values = await rdc.generateValues(initial, keys)

  res.writeHead(200, { 'Content-Type': 'application/json' })
  res.end(JSON.stringify({
    h: keys,
    d: values,
  }))
}).listen(8080)
```


