# [https://github.com/luckchoudog/logger-library](https://github.com/luckchoudog/logger-library)
#HOW TO USE：
## Step 1. Add the JitPack repository to your build file
    allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
## Step 2. Add the dependency
    dependencies {
	        compile 'com.github.luckchoudog:logger-library:-SNAPSHOT'
	}
## exsample:


        Logger.d("hello");
        Logger.d("hello %s %d", "world", 5);   // String.format
        Logger.e("hello");
        Logger.w("hello");
        Logger.v("hello");
        Logger.wtf("hello");
        Logger.json(JSON_CONTENT);
        Logger.xml(XML_CONTENT);
        Logger.log(Logger.DEBUG, "tag", "message", new Throwable());
        Logger.t("mytag").d("hello");//Separate setting tag

        //Global settings , use in application
        Logger.init("YOUR_TAG")                 // default PRETTYLOGGER or use just init()
                .methodCount(1)                 // default 2
                .hideThreadInfo()               // default shown
                .logLevel(LogLevel.FULL)        // default LogLevel.FULL . Use LogLevel.NONE for the release versions
                .methodOffset(0)                // default 0
                .logAdapter(new AndroidLogAdapter()); //default AndroidLogAdapter

### String format arguments are supported

    Logger.d("hello %s", "world");
### Array, Map, Set and List are supported

    Logger.d(list);
    Logger.d(map);
    Logger.d(set);
    Logger.d(new String[]);


### Settings (optional)

Change the settings with init. This should be called only once. Best place would be in application class. All of them are optional. You can just use the default settings if you don't init Logger.

    Logger
      .init(YOUR_TAG)                 // default PRETTYLOGGER or use just init()
      .methodCount(3)                 // default 2
      .hideThreadInfo()               // default shown
      .logLevel(LogLevel.NONE)        // default LogLevel.FULL
      .methodOffset(2)                // default 0
      .logAdapter(new AndroidLogAdapter()); //default AndroidLogAdapter
    }
##### Note: Use LogLevel.NONE for the release versions.
### Use another log util instead of android.util.log

Implement LogAdapter
set it with init

    Logger.init()..logAdapter(new CustomLogAdapter())
## Change TAG
### All logs tag

    Logger.init(YOUR_TAG);
### Log based

    Logger.t("mytag").d("hello");//
## Change method count (Default: 2)

### All logs

    Logger.init().methodCount(1);
### Log based

    Logger.t(1).d("hello");
## Change method stack offset (Default: 0)

To integrate logger with other libraries, you can set the offset in order to avoid that library's methods.

    Logger.init().methodOffset(5);
## Hide thread information

    Logger.init().methodCount(1).hideThreadInfo();