FROM java

RUN mkdir /usr/prometheus

#RUN apt-get update && apt-get install -y maven

## Download prometheus java httpserver jar.
##RUN ["mvn", "dependency:get", "-DremoteRepositories=http://repo1.maven.org/maven2/", "-DgroupId=io.prometheus.jmx", "-DartifactId=jmx_prometheus_httpserver", "-Dversion=LATEST", "-Dtransitive=false", "-Ddest=/usr/prometheus"]
#ADD http://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/0.9/jmx_prometheus_httpserver-0.9-jar-with-dependencies.jar /usr/prometheus/

#COPY prometheus-config.yaml /usr/prometheus/
#COPY wlfullclient.jar /usr/prometheus/
#COPY jmx_prometheus_httpserver-jar-with-dependencies.jar /usr/prometheus/

#RUN cd /usr/prometheus

WORKDIR /usr/prometheus

EXPOSE 8888

#java -cp wlfullclient.jar:jmx_prometheus_httpserver-jar-with-dependencies.jar io.prometheus.jmx.WebServer 8888 /u01/prometheus-config.yaml

ENTRYPOINT ["java", "-cp", "/usr/prometheus/wlfullclient.jar:/usr/prometheus/jmx_prometheus_httpserver-jar-with-dependencies.jar", "io.prometheus.jmx.WebServer"]

CMD ["8888", "/usr/prometheus/prometheus-config.yaml"]

