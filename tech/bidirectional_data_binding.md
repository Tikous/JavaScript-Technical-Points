```javascript
let obj = {}
let input = document.getElementById('input')
let span = document.getElementById('span')

Object.defineProperty(obj, 'text', {
  configurable: true,
  enumerable: true,
  get() {
    console.log('get data')
  },
  set(newVal) {
    console.log('data update')
    input.value = newVal
    span.innerHTML = newVal
  }
})

input.addEventListener('keyup', function(e) {
  obj.text = e.target.value
})
```