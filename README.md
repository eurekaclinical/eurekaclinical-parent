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

## Getting help
Feel free to contact us at help@eurekaclinical.org.
