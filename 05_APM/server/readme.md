# Start APM Server
1. Change the IP or address in the apm.yml file to your address! 
2. Change password of elasticsearch user to your user
3. Run `docker-compose up` to start the apm server

## Example:
```
#-------------------------- Elasticsearch output --------------------------
output.elasticsearch:
  # Array of hosts to connect to.
  # Scheme and port can be left out and will be set to the default (`http` and `9200`).
  # In case you specify and additional path, the scheme is required: `http://elasticsearch:9200/path`.
  # IPv6 addresses should always be defined as: `https://[2001:db8::1]:9200`.
  hosts: ["https://myesserver:9200"]

  # Boolean flag to enable or disable the output module.
  #enabled: true

  # Set gzip compression level.
  #compression_level: 0

  # Protocol - either `http` (default) or `https`.
  #protocol: "https"

  # Authentication credentials - either API key or username/password.
  #api_key: "id:api_key"
  username: "elastic"
  password: "mypassword"
```


# Start Client example
--> Go to 05_apm/client! 
1. Change the output adress in the docker-compose.yml file in the client_example
2. Run `docker-compose up`
