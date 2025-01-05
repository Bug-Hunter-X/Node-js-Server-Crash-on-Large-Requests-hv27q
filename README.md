# Node.js Server Crash on Large Requests

This repository demonstrates a common error in Node.js servers where the server crashes when receiving large requests.  The issue arises from not properly handling the incoming data stream, leading to a RangeError: Invalid string length. 

The `bug.js` file showcases the problematic code, while `bugSolution.js` provides a corrected version with error handling.

## Bug
The original code lacks error handling for the incoming request data. When a large request is made, the `req.on('data', ...)` listener attempts to concatenate the entire request body into the `body` variable without a mechanism to handle potential memory issues. This causes the server to crash with a `RangeError: Invalid string length`.

## Solution
The solution involves two key changes:
1. Adding an error handler using `req.on('error', ...)` to catch errors like the RangeError and respond appropriately.
2. Implementing proper error handling during JSON parsing using a `try...catch` block.