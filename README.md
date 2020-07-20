# API Template

### Prerequisites
1. Publish [bom and parent-pom files](https://github.com/mulesoft-consulting/mule4-rest-api-template/tree/master/parent-pom-files) to chosen artifact repo 
2. Publish [error-handler-library](https://github.com/mulesoft-consulting/error-handler-library) to chosen artifact repo

### Getting Started
1. Project pom file has solutions-parent-pom as parent
Eg:-
```
<parent>
		<groupId>com.mulesoft</groupId>
		<artifactId>solutions-parent-pom</artifactId>
		<version>0.0.1</version>
    </parent>
```
2. Project pom file has maven dependency plugin to unpack [error-hanling-library](https://github.com/mulesoft-consulting/error-handler-library) . Make sure <artifactItem> details are configured accordingly 
```
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-dependency-plugin</artifactId>
				<version>${maven.dependency.plugin.version}</version>
				<executions>
					<execution>
						<id>unpack</id>
						<phase>generate-sources</phase>
						<goals>
							<goal>unpack</goal>
						</goals>
						<configuration>
							<artifactItems>
								<artifactItem>
									<!-- TODO: Replace with the Published error-handling artifact library details -->
									<groupId>com.mulesoft</groupId>
									<artifactId>error-handler-library</artifactId>
									<version>${error.handler.library.version}</version>
									<!-- *************************************************** -->
									<classifier>mule-application</classifier>
									<overWrite>true</overWrite>
									<outputDirectory>src/main/mule/</outputDirectory>
									<includes>**/error-*.xml</includes>
								</artifactItem>
								<artifactItem>
									<!-- TODO: Replace with the Published error-handling artifact library details -->
									<groupId>com.mulesoft</groupId>
									<artifactId>error-handler-library</artifactId>
									<version>${error.handler.library.version}</version>
									<!-- *************************************************** -->
									<classifier>mule-application</classifier>
									<overWrite>true</overWrite>
									<outputDirectory>src/main/resources/</outputDirectory>
									<includes>**/*.yaml</includes>
								</artifactItem>
							</artifactItems>
						</configuration>
					</execution>
				</executions>
			</plugin>
```
3. Make sure JSON-logger is published in Anypoint platform Org/Business Group
4. Publish the asset in Exchange - as [REST API - RAML] - from [here](https://github.com/mulesoft-consulting/mule4-rest-api-template/tree/master/rest-api-template-spec)
5. Remove this repository and replace with artifact repository where Parent-POM files are published

        <repository>
            <id>mulesoft-consulting</id>
            <url>https://pkgs.dev.azure.com/mulesoft-consulting/_packaging/mulesoft-consulting/maven/v1</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
6. Add or edit the [settings.xml](https://github.com/mulesoft-consulting/mule4-rest-api-template/blob/master/settings.xml) file in ${user.home}/.m2
7. Execute command: **mvn clean install** in the project folder (command prompt), and all references will be in place on build success
 
### Test
- Please make sure you have **API Manager Environment credentials** configured in Anypoint studio. This is required for _API autodiscovery_ configuration.

1. Right-click project root, select Run As - Run As Configurations... 
2. Select the project from 'Mule Applications'
3. Add '-Denv=local' to Program arguments (Under (x)-Arguments) tab
4. Add '-Dencrypt.key=secure12345' to Program arguments (Under (x)-Arguments) tab
5. Click Run, and wait for the project to the build and deployed successfully
6. Execute command -  curl -H 'client\_id:a' -H 'client\_secret:b' -H 'x-correlation-id:abc' [http://localhost:8082/api/ping](http://localhost:8082/api/ping) , and this should return [ { "message": "Pong" } ]



