The 9th question on BFE.dev.
```javascript
I B C A L K A
D R F C A E A
G H O E L A D 
```
In this question, we are asked to decode message from this two-dimensional array. We should start at top left and then move diagonally down right, when we get to the edge, we should swich to diagonally up right, and move like this way until can’t neither move down right, nor up right.

This question is easy to understand but it’s a little difficult to implement.

So we should firstly check the edge condition, when message.length or message[0].length is zero, return empty string.

Then we init result as an empty string, row and col equals to zero, and directionY equals to 1 which is used to control direction.

After that, we can make a while loop to iterate through the message. And judging conditions in this while loop, should be col less than cols first, which means that we can continue the while loop before we get to the edge of message’s the rightmost col. Then we need to use Logic And with row greater than minus 1 also Logic And row less than rows, in this way we can ensure that row won’t beyond the bondary of message in vertical direction.

After that we use addtion assignment operator here, making result equals to message[row][col] and plus it self. Then let col plus 1 and let row plus directionY, and then we need to control the edge case. When row greater than rows minus 1, it means we have arrived to the bottom of the two dimensional array, so we need to change the direction of it and row minus 2. Else if row less than zero, it meas we have arrived to the top of the dimensional array, so we need to make directionY as 1, and row plus 2.

Then our while loop has finished, and we can return the result.

The whole code is here.
```javascript
function decode(message) {
  if (message.length === 0 || message[0].length === 0) return ''
  
  const rows = message.length
  const cols = message[0].length

  let result = ''
  let row = 0, col = 0
  let directionY = 1

  while(col < cols && row > -1 && row < rows) {
    result += message[row][col]
    col += 1
    row += directionY

    if (row > rows - 1) {
      directionY = -1
      row -= 2
    } else if (row < 0) {
      directionY = 1
      row += 2
    }
  }
  return result
}
```
