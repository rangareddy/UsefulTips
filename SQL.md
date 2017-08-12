

## SQL Formatter
- Java Code
   ```java 
    import org.hibernate.engine.jdbc.internal.BasicFormatterImpl;
    
    String formattedSQL = new BasicFormatterImpl().format(sql);
    ```
    ###### Maven Dependency:
    ```xml
    <dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-core</artifactId>
			<version>5.2.10.Final</version>
	</dependency>
