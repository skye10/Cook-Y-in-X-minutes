### Generate negative binomial random numbers

#### Problem

You want to generate negative binomial samples

#### Dependencies
* [Node.js](https://nodejs.org/en/) is installed in your system
* jstat module (javascript statistical package)

#### References
* [Simulating discrete random variables](https://stats.idre.ucla.edu/stata/code/imulating-discrete-geometric-poisson-and-zero-inflated-poisson-negative-binomial-and-zero-inflated-negative-binomial-random-variables/) (UCLA)
* Luc Devroye, Non Uniform Random Variate Generation, pp. 488-489.


***

#### Theory

##### Negative Binomial Distribution (nbinom)

The probability distribution of the number of trials *X* to produce *r* successes in Bernoulli trials, where  *p* is the probability of each success.
$$
\mu = \frac{r(1-p)}{p}, \; \sigma^2=\frac{r(1-p)}{p^2}
$$
Simplifying,
$$
p = \frac{\mu}{\sigma^2}, \; r =\frac{\mu^2}{(\sigma^2-\mu)}
$$

##### Interpretation

Negative Binomial is a useful overdispersed alternative to the Poisson distribution -- the mixing distribution of the Poisson rate is a Gamma distribution. This idea is used to generate negative binomial random variables below.

***

#### Recipes

Negative binomial generation in Javascript. Dependencies:

* jsat 1.9.4 (Javascript statistical library)
  * https://www.npmjs.com/package/jstat
  * http://jstat.github.io/

```javascript
let jstat = require('jstat');

// Negative Binomial
// p = mean/var, r = mean^2/(var - mean)
function gen_nbinom(p, r, N) {
    let a;
    let u;
    let g;
    let v = [];
    let avg = 0;
    for (let i=1; i<=N; i++) {
        a = p/(1.0-p);
        u = jstat.gamma.sample(r, 1.0) / a; // standard gamma (beta=1)
        g = jstat.poisson.sample(u);
        v.push(g);
    }
    return v;
}
```

Which returns an arrary of N random numbers, based on {p, r}, which can be calculated as {mean/var, and mean^2/(var - mean)}. 

Here's the above function as a generator, which makes is more memory efficient:

```javascript
/* Generator invocation
   nb = nbinom_gen(0.5, 1.3, 1000);
   nb.next().value  
*/ 
function* nbinom_gen(p, r, N) {
    let a = p/(1.0-p);
    let u;
    let g;
    let i = 0;
    while (i < N) {
        u = jstat.gamma.sample(r, 1.0) / a;
        g = jstat.poisson.sample(u);
        i++;
        yield g;
    }
}
```

