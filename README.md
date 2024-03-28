# ngrok-dev


## Some examples
### Run a local www
```
docker run -d -p 8888:80 nginx
```
### Run the ngrok agent
```
ngrok http http://localhost:8888
```
```
ngrok http http://localhost:8888 \
  --oauth google \
  --oauth-allow-domain radarsec.com
```
### From the docs ...
```
ngrok http 80 \
  --oauth google \
  --oauth-allow-email my-user@gmail.com \
  --oauth-allow-domain example.com
```
