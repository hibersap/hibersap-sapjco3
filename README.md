**The SAP Java Connector**  
The SAP Java Connector (SAP JCo) is a library that allows a Java application to communicate with any SAP system.
However, there is no publically available Maven repository maintained by SAP and since the SAP JCo has a commercial license, it cannot be deployed to a public repository like Maven Central.

This is a Maven wrapper for the SAP JCo library so it can be used with the Hibersap project.

**Using SAP JCo with Hibersap**  
To use the SAP JCo with Hibersap in your own Maven projects, you need to download the SAP JCo distribution from SAP (http://service.sap.com/connectors) and either install the jar downloaded from SAP to your local Maven repository (variant a) or deploy it to e.g. an enterprise Maven repository like Nexus or Artifactory (variant b):

(a) mvn install:install-file -DgroupId=org.hibersap -DartifactId=com.sap.conn.jco.sapjco3 -Dversion=3.0.15 -Dpackaging=jar -Dfile=path/to/sapjco3.jar

(b) mvn deploy:deploy-file -DrepositoryId=[your.repo.id] -DgroupId=org.hibersap -DartifactId=com.sap.conn.jco.sapjco3 -Dversion=3.0.15 -Dpackaging=jar -Dfile=path/to/sapjco3.jar

**Versioning**  
It is recommended to use the actual version number of SAP JCo so it is possible to add new versions later. Hibersap declares the dependency to sapjco3 as optional, which means a project with a dependency to Hibersap does not transitively get the dependency to sapjco3 and you need to explicitly declare this dependency. (Basically it does not even need to have the same Maven coordinates.)

**Native Library**  
In addition to the JAR archive every SAP JCo distribution contains a native library which is needed during runtime. It is also recommended to install the native lib to your Maven repo so you can add it to your application's distribution and use it for integration testing. If you build distributions for different operation systems and architectures, you may add a Maven classifier to the native lib's coordinates.

