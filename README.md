# Runnin aiohttp server in gunicorn+nginx

1. Install `nginx`: `sudo apt install nginx`;
2. Install python libs: `pip install -r requirements.txt`;
3. Update `/etc/nginx/nginx.conf`:
  ```
  upstream backend {
		server unix:/tmp/aiohttp.sock fail_timeout=0;
	}

	server {
		listen          80;
		server_name	gateway;
		location / {
			proxy_pass      http://backend;
		}
  }

  ```
4. Run `app` server: `./run.sh`
