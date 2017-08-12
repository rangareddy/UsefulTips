## JSON Utility using Jackson

### JSONUtility.java
```java 
import org.apache.commons.io.IOUtils;
import org.codehaus.jackson.map.ObjectMapper;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import java.io.*;
import java.util.Objects;
public class JSONUtility {

    private static final Logger LOGGER = LoggerFactory.getLogger(JSONUtility.class);
    private static final ObjectMapper objectMapper = new ObjectMapper();

    public static String getJSONString(final Object data) throws RuntimeException {
        try {
            return objectMapper.writeValueAsString(data);
        } catch (IOException e) {
            LOGGER.error(e.getMessage() + data);
            throw new RuntimeException(e);
        }
    }

    public static <T> T getJSONData(final String fileName, final Class<T> clazz) throws FileNotFoundException {
        Objects.requireNonNull(fileName, "File name must not be null.");
        return getJSONData(new File(fileName), clazz);
    }

    public static <T> T getJSONData(File file, final Class<T> clazz) throws FileNotFoundException {
    	Objects.requireNonNull(clazz, "Clazz must not be null.");
        InputStream inputStream = null;
        if (file.exists()) {
            inputStream = new FileInputStream(file);
        } else {
            inputStream = JSONUtility.class.getClassLoader().getResourceAsStream(file.getName());
        }
        if (inputStream == null) {
            throw new FileNotFoundException("File <" + file.getAbsolutePath() + "> is not found.");
        }
        return getJSONData(inputStream, clazz);
    }
    
    private static <T> T getJSONData(final InputStream inputStream, Class<T> clazz) {
    	Objects.requireNonNull(inputStream, "InputStream must not be null.");
        try {
            return objectMapper.readValue(inputStream, clazz);
        } catch (Exception ex) {
            LOGGER.error(ex.getMessage());
        } finally {
            IOUtils.closeQuietly(inputStream);
        }
        return null;
    }

    public static <T> T getJSONData(final byte[] data, final Class<T> clazz) throws Exception {
    	Objects.requireNonNull(data, "data must not be null.");
        try {
            return objectMapper.readValue(data, clazz);
        } catch (Exception ex) {
            LOGGER.error("Exception occurred while getting the JSON Data. ", ex);
            throw ex;
        }
    }

    public static boolean createNewJSONFile(final String filePath, final Object data) {
    	Objects.requireNonNull(filePath, "File path must not be null.");
        return createNewJSONFile(new File(filePath), data);
    }

    public static boolean createNewJSONFile(File file, final Object data) {
    	Objects.requireNonNull(file, "File must not be null.");
        String fileFullPath = file.getAbsolutePath();
        if (!fileFullPath.endsWith("json")) {
            fileFullPath = fileFullPath + ".json";
            file = new File(fileFullPath);
        }
        boolean isFileCreated = false;
        if (!file.exists()) {
            try {
                objectMapper.writerWithDefaultPrettyPrinter().writeValue(file, data);
                isFileCreated = true;
            } catch (IOException e) {
                LOGGER.error("Unable to write the data to the file " + file.getAbsolutePath() + ". Exception is " + e);
            }
        } else {
            LOGGER.error("File already exists in the following path ." + file.getAbsolutePath());
        }
        return isFileCreated;
    }
}
```
###### Maven Dependency:

```xml

<dependency>
  <groupId>org.slf4j</groupId>
	<artifactId>slf4j-api</artifactId>
	<version>1.7.5</version>
</dependency>

<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-log4j12</artifactId>
  <version>1.7.5</version>
</dependency>

<dependency>
  <groupId>commons-io</groupId>
  <artifactId>commons-io</artifactId>
  <version>1.3.2</version>
</dependency>

<dependency>
  <groupId>org.codehaus.jackson</groupId>
  <artifactId>jackson-core-asl</artifactId>
  <version>1.9.13</version>
</dependency>

<dependency>
  <groupId>org.codehaus.jackson</groupId>
  <artifactId>jackson-mapper-asl</artifactId>
  <version>1.9.13</version>
</dependency>

```
