# Steps for this lecture
1. Clone the opbeans-java repository
```
git clone https://github.com/elastic/opbeans-java
```
2. Then build the app by running 
```docker build -t opbeans/opbeans-java:latest .```
3. Start the docker compose file by running 
```
docker-compose up
```

# In case you want to instrument your own Java App

Run the java app with the following settings
```
java -javaagent:./elastic-apm-agent-1.33.0.jar \
-Delastic.apm.service_name=test-application \
-Delastic.apm.server_urls=http://10.0.2.4:8200 \
-Delastic.apm.secret_token= \
-Delastic.apm.environment=development \
-Delastic.apm.application_packages=org.example \
-jar myapp.jar

```
