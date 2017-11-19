# eurekaclinical-parent
[Atlanta Clinical and Translational Science Institute (ACTSI)](http://www.actsi.org), [Emory University](http://www.emory.edu), Atlanta, GA

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

## Version history
### Version 1

## Specifying this pom as a parent
```
<parent>
    <groupId>org.eurekaclinical</groupId>
    <artifactId>eurekaclinical-parent</artifactId>
    <version>version</version>
</parent>
```

## Additional configuration
The `stage-production` profile sets the `eurekaclinical.stage` property to `PRODUCTION`. This
property is a convention that eurekaclinical components use to change configuration in
production settings.

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

## Getting help
Feel free to contact us at help@eurekaclinical.org.
