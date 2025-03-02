# Performance Optimization

## Caching Strategies

### Using Redis for Caching

Redis is an in-memory data structure store that can be used as a cache.

### Installing Dependencies

```bash
npm install redis
```

### Example

```javascript
const express = require("express");
const redis = require("redis");
const app = express();
const port = 3000;

const client = redis.createClient();

app.get("/data", (req, res) => {
  const key = "data";
  client.get(key, (err, data) => {
    if (data) {
      res.send(`Cache hit: ${data}`);
    } else {
      const newData = "Some data";
      client.setex(key, 3600, newData);
      res.send(`Cache miss: ${newData}`);
    }
  });
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## Load Balancing

Use a load balancer to distribute incoming traffic across multiple servers.

### Example with Nginx

```nginx
http {
  upstream myapp {
    server 127.0.0.1:3000;
    server 127.0.0.1:3001;
  }

  server {
    listen 80;

    location / {
      proxy_pass http://myapp;
    }
  }
}
```

## Profiling and Monitoring

### Using PM2 for Process Management

PM2 is a process manager for Node.js applications.

### Installing Dependencies

```bash
npm install pm2 -g
```

### Example

```bash
pm2 start app.js
pm2 monit
```
