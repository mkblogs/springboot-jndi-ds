# Spring Boot JNDI Example using `JndiDataSourceLookup`
In this example, read the `db.properties` file and created JNDI DataSource using Tomcat JNDI Context
## Code for setting
```java
 protected void postProcessContext(Context context) {
	 	log.info("in side post process");
        ContextResource resource = new ContextResource();
        resource.setName(jndiName);
        resource.setType(DataSource.class.getName());
        resource.setProperty("driverClassName", driverClassName);
        resource.setProperty("url", url);
        resource.setProperty("username", username);
        resource.setProperty("password", password);
        context.getNamingResources().addResource(resource);
    }
```
## Code for reading the from JNDI Context
```java
 JndiDataSourceLookup dsLookup = new JndiDataSourceLookup();
 dsLookup.setResourceRef(true);
 DataSource dataSource = dsLookup.getDataSource(jndiName);
```
### application.yml
---
spring:
 - datasource:
  -  jndi-name: jdbc/MysqlJNDI