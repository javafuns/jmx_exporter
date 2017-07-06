# T3 protocol support 
In order to use t3 protocol, you need to modify the source code:  
Forked Repository: https://github.com/javafuns/jmx_exporter

# Build Prometheus JMX Exporter 
Prometheus monitors only HTTP endpoints, so use JMX Exporter HTTP Server to expose JMX MBeans and serve requests from Prometheus:
```
$ cd jmx_prometheus_httpserver/
$ mvn clean install
```
After command completes, you will find artifacts at 'target/' folder, one of which is:
```
target/jmx_prometheus_httpserver-0.10-SNAPSHOT-jar-with-dependencies.jar
```
Remember this jar, as it will be used later.

# Run Prometheus JMX Exporter in Docker Container
When running Prometheus JMX Exporter HTTP Server, you need to provide necessary jars and config file for it:
```
docker run -p 8888:8888 -v /Users/gavin/github/javafuns/wlfullclient.jar:/usr/prometheus/wlfullclient.jar -v /Users/gavin/github/javafuns/jmx_exporter/jmx_prometheus_httpserver/target/jmx_prometheus_httpserver-0.10-SNAPSHOT-jar-with-dependencies.jar:/usr/prometheus/jmx_prometheus_httpserver-jar-with-dependencies.jar -v /Users/gavin/github/javafuns/jmx_exporter/jmx_prometheus_httpserver/prometheus-config.yaml:/usr/prometheus/prometheus-config.yaml --name prometheus-jmx-exporter-httpserver
prometheus-jmx-exporter-httpserver
```
NOTE:
- For wlfullclient.jar, please refer to [Creating a wlfullclient.jar](https://docs.oracle.com/middleware/1221/wls/SACLT/jarbuilder.htm).
- Please DO remember replacing file paths (which start with '/Users/gavin/github/javafuns/') with correct ones in your environment for above docker command.  
- Please also DO remember changing jmx_exporter/jmx_prometheus_httpserver/prometheus-config.yaml as it's only a sample.