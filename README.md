# Eureka! Clinical Parent pom.xml
[Georgia Clinical and Translational Science Alliance (Georgia CTSA)](http://www.georgiactsa.org), [Emory University](http://www.emory.edu), Atlanta, GA

# What does it do?
It is the parent pom used by all projects in the eurekaclinical organization. It specifies the following sections, so you can omit them in the pom of any Eureka! Clinical project:
* default software license (Apache 2)
* organization
* distribution management
* dependency repositories
* plugin repositories
* developers
* default plugin versions and configurations (in a pluginManagement section)
* default plugin dependencies
* setup to use Maven Central

## Version 3
We switched from the tomcat7-maven-plugin to cargo-maven2-plugin for running Eureka! 
Clinical microservices in an embedded tomcat. See below for details on how to
configure it in your maven projects.

We also changed the default setting of the Nexus release plugin's `autoReleaseAfterClose`
property to `false`. This causes the Maven release plugin to publish an artifact to Maven 
Central's staging repository, where it can be inspected prior to release. Actually 
releasing an artifact now requires an extra step.

## Version 2
Updates artifact versions.

## Version 1
Initial release.

## Specifying this pom as a parent
```
<parent>
    <groupId>org.eurekaclinical</groupId>
    <artifactId>eurekaclinical-parent</artifactId>
    <version>version</version>
</parent>
```

## Additional configuration

### Stages
The `stage-production` profile sets the `eurekaclinical.stage` property to `PRODUCTION`. This
property is a convention that eurekaclinical components use to change configuration in
production settings.

### Embedded tomcat
This pom.xml specifies a `tomcat` profile that is for running warfiles in 
embedded tomcat with SSL turned on. Start tomcat with the following command:
```
mvn process-resources cargo:run -Ptomcat
```
Press Control-C to stop tomcat.

The profile requires the following configuration files in your 
`src/main/resources` directory:
* `tomcat-eureka-config/logging.properties`: Configuration of logging that will be written to the 
tomcat `logs` directory.
* `tomcat-eureka-config/eureka/application.properties`: Configuration of Eureka! Clinical microservices.
* `tomcat-server-config/context.xml`: The tomcat context.xml, usually used to define data sources.
* `tomcat-server-config/localhost.keystore`: the self-signed SSL certificate that tomcat should serve.
* `tomcat-server-config/localhost.truststore`: the same SSL certificate, in order for warfiles to trust it.

In your profile, optionally create a `dependencies` section with any additional 
warfiles that you wish to run. 

In the cargo plugin's `deployables` section, add a `deployable` tag for the current project's
warfile with a `location` tag pointing to the path of the built warfile. Add any additional warfiles
that you want to deploy to the `deployables`. 

You may specify additional plugins to prepare the above configuration files, populate databases, and more. Their
executions should operate in the `process-resources` or earlier build phases.

### Maven Central
The Eureka! Clinical project releases its artifacts to Maven Central. If you are authorized to release projects for Eureka! Clinical, you need to configure your maven environment as follows:
1) Install and configure Gnu Privacy Guard (GPG) on your workstation.
2) Create a server profile in `~/.m2/settings.xml` with your Maven Central credentials as follows:
```
<server>
    <id>ossrh</id>
    <username>your username</username>
    <password>you password</password>
</server>
```
3) Create a profile in `~/.m2/settings.xml` with your GPG credentials as follows:
```
<profile>
    <id>ossrh</id>
    <activation>
        <activeByDefault>true</activeByDefault>
    </activation>
    <properties>
        <gpg.executable>gpg</gpg.executable>
        <gpg.passphrase>your passphrase</gpg.passphrase>
    </properties>
</profile>
```

Note that the Nexus staging plugin is configured with `autoReleaseAfterClose` set to `false`, which causes the Maven release plugin to release the artifact to Maven central's password protected staging repository.

## Getting help
Feel free to contact us at help@eurekaclinical.org.
