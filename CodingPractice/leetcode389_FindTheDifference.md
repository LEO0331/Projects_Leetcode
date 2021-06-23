# Description
You are given two strings s and t. String t is generated by random shuffling string s and then add one more letter at a random position. Return the letter that was added to t.
```
Input: s = "abcd", t = "abcde" Output: "e" Explanation: 'e' is the letter that was added.
Input: s = "", t = "y" Output: "y"
Input: s = "a", t = "aa" Output: "a"
Input: s = "ae", t = "aea" Output: "a"
```
# Concept
Hash, Map, Bitwise
# Solution
1. two maps compare each key-value or one map to check the numbers of values by deductions 
```
/*
 * @param {string} s
 * @param {string} t
 * @return {character}
 */
var findTheDifference = function(s, t) {
    let map = new Map()
    let m = new Map()
    for(let i=0; i<s.length; i++){
        if(map.has(s[i])) map.set(s[i], map.get(s[i])+1)
        else map.set(s[i], 1)
    }
    for(let i=0; i<t.length; i++){
        if(m.has(t[i])) m.set(t[i], m.get(t[i])+1)
        else m.set(t[i], 1)
    }
    for(const [key, value] of m){
        if(map.get(key) !== value) return key
    }
    /*
    for(c of t){
        if (!map.has(c)) return c //if added char is not part of the map
        else map.set(c, map.get(c)-1)
        if (map.get(c) < 0) return c //<= -1, if added char is part of the map but value is -1
    }
    */
};
```
2. Bitwise operators, reduce() and charCodeAt()
```
var findTheDifference = function(s, t) { //https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt
    const sum1 = s.split('').reduce((acc, cur) => acc + cur.charCodeAt(0), 0) //cur.charCodeAt()
    const sum2 = t.split('').reduce((acc, cur) => acc + cur.charCodeAt(0), 0)
    /*
    let sum1 = 0
    for(let i = 0; i < s.length; i++) {
        sum1 += s[i].charCodeAt() //charCodeAt(0)
    }
    let sum2 = 0
    for (let i = 0; i < t.length; i++) {
        sum2 += t[i].charCodeAt()
    }
    OR
    let ans = 0
    for(let c of t) ans ^= c.charCodeAt() - 97
    for(let c of s) ans ^= c.charCodeAt() - 97
    return String.fromCharCode(ans+97)
    */
    return String.fromCharCode(sum2 - sum1)
    /*
    let x = 0
    for (const char of s) {
        x ^= char.charCodeAt()
    }
    for (const char of t) {
        x ^= char.charCodeAt()
    }
    OR
    for (let i = 0; i < s.length; i++) {
    	  x ^= s.charCodeAt(i)
    }
    for (let i = 0; i < t.length; i++) {
    	  x ^= t.charCodeAt(i)
    }
    return String.fromCharCode(x)
    */
};
```
# Complement 
X^X=0 and X^0=X for every NUMBER X