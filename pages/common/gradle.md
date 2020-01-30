# gradle

> Gradle is an open source build automation system.
> More information: <https://gradle.org>.

- Compile a package:

`gradle build`

- Exclude test task:

`gradle build -x {{test}}`

- Run in offline mode to prevent gradle from accessing the network during builds:

`gradle build --offline`

- Clear the build directory:

`gradle clean`

- Compile and Release package:

`gradle assembleRelease`

- Download jar with dependencies:

````
// Script to Download jar-file and its dependencies
// Create file called build.gradle (in Downloads folder for example)
// Run CLI command gradle copyDependencies

apply plugin: 'groovy'

repositories {
    mavenCentral()
}

dependencies {
    compile group: 'org.hibernate', name: 'hibernate-core', version: '5.4.4.Final'
}

task copyDependencies(type: Copy) {
    from configurations.runtime
    into "lib"
}
````

- Upload jar to Maven repository:

````
// Script to upload prebuild jar to Azure DevOps
// 1) Create file called build.gradle (in Downloads folder for exmple)
// 2) Create file in same directory called settings.gradle with the content: "rootProject.name = '<NAME_OF_JAR>'"
// 2) Create file in same directory called gradle.properties with the content: 
//		username = ncdmz\\<INITIALS>
//		password = <PASSWORD>
// 3) Modify 'group', version etc. below
// 4) Run CLI command gradle publish

plugins {
    id 'maven-publish'
}

group = 'com.netcompany'
version = '1.0.0'

println "USERNAME: '" + username + "'" 
println "PASSWORD: '" + password + "'" 

publishing {
    publications {
        maven(MavenPublication) {
            artifact('lib/db2jcc_license_cu.jar') {
                extension 'jar'
            }
        }
    }
    repositories {
	    maven {
	    url 'https://source.netcompany.com/tfs/Netcompany/_packaging/MDCEJOUR_Feed/maven/v1'
	    credentials {
	        username project.username
	        password project.password
	    	}
		}
    }
}
````