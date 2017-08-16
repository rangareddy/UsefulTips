# UsefulTips

### Converting Iterable to List:
```java
public static <E> List<E> makeCollection(Iterable<E> iterable) {
	List<E> list = new ArrayList<E>();
	for (E item : iterable) {
	    list.add(item);
	}
	return list;
}
```	
### Reading File data:
```java
InputStream in = new FileInputStream(new File("C:\\Ranga\abc.txt"));
String str = IOUtils.toString(in, "UTF-8");
```
### Timer Util:
```java
import java.util.concurrent.TimeUnit;
public class TimerUtil {

	private long startTime;
	private long endTime;

	public TimerUtil() {
		startTime();
	}

	public void startTime() {
		this.startTime = System.nanoTime();
	}

	public void endTime() {
		this.endTime = System.nanoTime();
	}

	public long timeDiff() {
		return endTime - startTime;
	}

	public long time(TimeUnit unit) {
		return unit.convert(timeDiff(), TimeUnit.NANOSECONDS);
	}

	public String toMinuteSeconds() {
		return "Total execution time: " + String.format("%d min, %d sec", time(TimeUnit.MINUTES),
				time(TimeUnit.SECONDS) - time(TimeUnit.MINUTES));
	}
}
```
### Getting all files in directory:
```java
import java.io.*;
import java.util.*;
import org.apache.commons.io.FileUtils;
import org.apache.commons.io.filefilter.FileFilterUtils;
import org.apache.commons.io.filefilter.TrueFileFilter;

public static List<File> getAllFile(String directoryName) {
	Collection<File> listFiles = FileUtils.listFiles(new File(directoryName), TrueFileFilter.TRUE,
			FileFilterUtils.makeSVNAware(null));
	return new ArrayList<>(listFiles);
}
```
