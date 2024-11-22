The entry point for your Redis implementation is in `app/main.js`.

Study and uncomment the relevant code: 

```javascript
// Uncomment this block to pass the first stage
const server = net.createServer((connection) => {
  // Handle connection
});

server.listen(6379, "127.0.0.1");
```

Push your changes to pass the first stage:

```
git add .
git commit -m "pass 1st stage" # any msg
git push origin master
```
