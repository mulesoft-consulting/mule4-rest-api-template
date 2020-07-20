> API template requires this parent-pom files to be published in chosen artifact repository
# BOM file
## Getting Started
##### Update bom -> pom.xml
1. Update the <orgid> with Anypoint Platform Org Id
2. Publish JSON logger to Anypoint Platform Exchange and update version <json.logger.ver>
3. Replace the below repository with appropriate artefactory repo where BOM will be published 
```
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
```
4. Publish bom -> pom.xml file to chosen artifact repository



# Parent-POM file
## Getting Started
##### Update parent-pom -> pom.xml
1. Update <parent> section with published bom file
2. Publish parent-pom -> pom.xml file to chosen artifact repository