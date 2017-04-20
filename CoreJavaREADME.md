# UsefulTips



### Converting Iterable to List:
   - ```java
        public static <E> List<E> makeCollection(Iterable<E> iterable) {
	        List<E> list = new ArrayList<E>();
	        for (E item : iterable) {
	            list.add(item);
	        }
	        return list;
	    }
        ```
### Reading File data:
   - ```java
        InputStream in = new FileInputStream(new File("C:\\Ranga\abc.txt"));
        String str = IOUtils.toString(in, "UTF-8");
        ```
