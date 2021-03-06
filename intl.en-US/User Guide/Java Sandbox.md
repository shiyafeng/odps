# Java Sandbox {#concept_aln_lrf_vdb .concept}

Java sandbox related restrictions of MaxCompute MapReduce and UDF programs running in distributed environments are as follows:

-   Direct access to local files is not allowed. You can only access files by using interfaces provided by MaxCompute MapReduce/Graph in the following way:
    -   Read resources specified by the ‘-resources’ option, including files, JAR packages, and resource tables.
    -   Output log information through ‘System.out’ and ‘System.err’.  You can view log information by running the log command on the MaxCompute console.
-   Direct access to the distributed file system is not allowed. You can only access table records by using MaxCompute MapReduce/Graph.
-   JNI call restrictions are not allowed.
-   Creation of Java threads is not allowed. Initiation of sub-processes to run Linux commands is not allowed.
-   Network access, including obtaining local IP addresses, is not allowed.
-   Java reflection is restricted. “suppressAccessChecks” permission is denied. A private attribute or method cannot be set to accessible for obtaining  private attributes or calling private methods.

Specifically for the user code, “access denied” is thrown if you follow these steps:

Methods for accessing local files are as follows:

java.io.File:

```
      public boolean delete ()
      public void deleteOnExit()
      public boolean exists()
      public boolean canRead()
      public boolean isFile()
      public boolean isDirectory()
      public boolean isHidden()
      public long lastModified()
      public long length ()
      public String[] list()
      public String[] list(FilenameFilter filter)
      public File[] listFiles()
      public File[] listFiles(FilenameFilter filter)
      public File[] listFiles(FileFilter filter)
      public boolean canWrite()
      public boolean createNewFile()
      public static File createTempFile(String prefix, String suffix)
      public static File createTempFile(String prefix, String suffix,File directory)
      public boolean mkdir ()
      public boolean mkdirs ()
      public boolean renameTo(File dest)
      public boolean setLastModified(long time)
      public boolean setReadOnly()
```

java.io.RandomAccessFile:

```
      RandomAccessFile(String name, String mode)
      RandomAccessFile(File file, String mode)
```

java.io.FileInputStream:

```
      FileInputStream(FileDescriptor fdObj)
      FileInputStream(String name)
      FileInputStream(File file)
```

java.io.FileOutputStream:

```
      FileOutputStream(FileDescriptor fdObj)
      FileOutputStream(File file)
      FileOutputStream(String name)
      FileOutputStream(String name, boolean append)
```

java.lang.Class:

```
public ProtectionDomain getProtectionDomain()
```

java.lang.ClassLoader:

```
    ClassLoader ()
    ClassLoader(ClassLoader parent)
```

java. lang. Runtime:

```
    public Process exec(String command)
    public Process exec(String command, String envp[])
    public Process exec(String cmdarray[])
    public Process exec(String cmdarray[], String envp[])
    public void exit(int status)
    public static void runFinalizersOnExit(boolean value)
    public void addShutdownHook(Thread hook)
    public boolean removeShutdownHook(Thread hook)
    public void load(String lib)
    public void loadLibrary(String lib)
```

java.lang.System:

```
    public static void exit(int status)
    public static void runFinalizersOnExit(boolean value)
    public static void load(String filename)
    public static void loadLibrary( String libname)
    public static Properties getProperties()
    public static void setProperties(Properties props)
    public static String getProperty(String key) // Only some keys are allowed for file access.
    public static String getProperty(String key, String def) // Only some keys are allowed for file access.
    public static String setProperty(String key, String value)
    public static void setIn(InputStream in)
    public static void setOut(PrintStream out)
    public static void setErr(PrintStream err)
    public static synchronized void setSecurityManager(SecurityManager s)
```

List of keys allowed by System.getProperty is as follows:

```
    java. version
    java. vendor
    java. vendor. url
    java. class. version
    os. name
    os. version
    os. arch
    file. separator
    path. separator
    line. separator
    java. specification. version
    java. specification. vendor
    java. specification. name
    java. vm. specification. version
    java. vm. specification. vendor
    java. vm. specification. name
    java. vm. version
    java. vm. vendor
    java. vm. name
    file. encoding
    user.timezone
```

java. lang. Thread:

```
    Thread ()
    Thread(Runnable target)
    Thread(String name)
    Thread(Runnable target, String name)
    Thread(ThreadGroup group, ...)
    public final void checkAccess()
    public void interrupt ()
    public final void suspend ()
    public final void resume ()
    public final void setPriority (int newPriority)
    public final void setName(String name)
    public final void setDaemon(boolean on)
    public void final stop ()
    public final synchronized void stop(Throwable obj)
    public static int enumerate(Thread tarray[])
    public void setContextClassLoader(ClassLoader cl)
```

java. lang. ThreadGroup:

```
    ThreadGroup (String name)
    ThreadGroup (Threadgroup parent, String name)
    public final void checkAccess ()
    public int enumerate (Thread list [])
    public int enumerate (Thread list [], boolean recurse)
    public int enumerate (Threadgroup list [])
    public int enumerate (Threadgroup list [], boolean recurse)
    public final ThreadGroup getParent ()
    public final void setDaemon (boolean daemon)
    public final void setMaxPriority (int pri)
    public final void suspend ()
    public final void resume ()
    public final void destroy ()
    public final void interrupt ()
    public void final stop ()
```

java. lang. reflect. AccessibleObject:

```
    public static void setAccessible (...)
    public void setAccessible (...)
```

java.net. InetAddress:

```
    public String getHostName ()
    public static InetAddress[] getAllByName(String host)
    public static InetAddress getLocalHost()
```

java.net.DatagramSocket:

```
public InetAddress getLocalAddress()
```

java.net.Socket:

```
Socket(...)
```

java.net.ServerSocket:

```
    ServerSocket (...)
    public Socket accept ()
    protected final void implAccept (Socket s)
    public static synchronized void setSocketFactory(...)
    public static synchronized void setSocketImplFactory(...)
```

java.net. DatagramSocket:

```
    DatagramSocket (...)
    public synchronized void receive(DatagramPacket p)
```

java.net.MulticastSocket:

```
MulticastSocket(...)
```

java.net.URL:

```
    URL(...)
    public static synchronized void setURLStreamHandlerFactory(...)
    java.net.URLConnection
    public static synchronized void setContentHandlerFactory(...)
    public static void setFileNameMap(FileNameMap map)
```

java.net.HttpURLConnection:

```
    public static void setFollowRedirects(boolean set)
    java.net.URLClassLoader
    URLClassLoader(...)
```

java.security.AccessControlContext:

```
    public AccessControlContext(AccessControlContext acc, DomainCombiner combiner)
    public DomainCombiner getDomainCombiner()
```

