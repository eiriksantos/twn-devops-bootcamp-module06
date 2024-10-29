# twn-devops-bootcamp-module06
Artifact Repository Manager with Nexus

## Publish Artifact to Repository

### Provision a Droplet for Nexus

### Install Nexus on the Droplet
1. Install java
```
$ apt install openjdk-17-jre-headless
```
2. Install Sonatype Nexus
```
$ wget https://download.sonatype.com/nexus/3/nexus-3.73.0-12-unix.tar.gz
$ tar -zxvf nexus-3.73.0-12-unix.tar.gz
```

### Create a user for Nexus service and start it
```
# create nexus user
$ adduser nexus

# change the user owner and group owner of the nexus directories
$ chown -R nexus:nexus /opt/nexus-3.73.0-12
$ chown -R nexus:nexus /opt/sonatype-work/

# modify the run_as_user="nexus"
$ vim /opt/nexus-3.73.0-12/bin/nexus.rc

# run nexus service
$ su - nexus
$ /opt/nexus-3.73.0-12/bin/nexus start

# configure inbound access for the Ubuntu Droplet on port 8081
```

### Login to the Nexus web console using the admin user
```
# retrieve admin password
$ cat /opt/sonatype-work/nexus3/admin.password

# login to the nexus web console
```

### Create a User and a Role in Nexus web console


### (Gradle Demo) Configure gradle files
1. configure build.gradle
2. configure gradle.properties
3. configure settings.gradle
4. build the artifact
    ```
    $ gradle build
    ```
5. publish the artifact to the nexus repo
    ```
    $ gradle publish
    ```
6. Check the nexus web console and browse for the artifact

### (Maven Demo)
1. configure pom.xml
2. configure ~/.m2/settings.xml
3. build the artifact
    ```
    $ mvn package
    ```
4. publish the artifact to the nexus repo
    ```
    $ mvn deploy
    ```

## Nexus REST API

### Query the repositories
```
# Using ejcs user
❯ curl -u ejcs:nexus -X GET 'http://146.190.80.152:8081/service/rest/v1/repositories'
[ {
  "name" : "maven-snapshots",
  "format" : "maven2",
  "type" : "hosted",
  "url" : "http://146.190.80.152:8081/repository/maven-snapshots",
  "attributes" : { }
} ]%  

# Using admin user
❯ curl -u admin:nexus -X GET 'http://146.190.80.152:8081/service/rest/v1/repositories'
[ {
  "name" : "nuget-hosted",
  "format" : "nuget",
  "type" : "hosted",
  "url" : "http://146.190.80.152:8081/repository/nuget-hosted",
  "attributes" : { }
},
...output omitted...                                                                        
```

### Query for components inside the repository
```
$ curl -u ejcs:nexus -X GET 'http://IP_ADDRESS:8081/service/rest/v1/components?repository=maven-snapshots'
```

