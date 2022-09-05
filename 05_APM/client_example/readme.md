Run the java app with the following settings
```
java -javaagent:./elastic-apm-agent-1.33.0.jar \
-Delastic.apm.service_name=test-application \
-Delastic.apm.server_urls=http://10.0.2.15:8200 \
-Delastic.apm.secret_token= \
-Delastic.apm.environment=production \
-Delastic.apm.application_packages=org.example \
-jar husStgr_v1.0.jar

```
