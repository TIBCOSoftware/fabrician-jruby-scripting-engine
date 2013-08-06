[fabrician.org](http://fabrician.org/)
==========================================================================
JRuby Scripting Engine Guide
==========================================================================

Introduction
--------------------------------------
This project builds a JRuby grid library for use in creating Silver Fabric enablers in JRuby.


Installation
--------------------------------------
To build the grid library, you must have Maven installed and set in your path. Then, run the
following:

```bash
  mvn install
```

If successful, the grid library will be created and uploaded to a running Broker.


Example
--------------------------------------

To use JRuby for a Silver Fabric Enabler, make sure your "language" and "languageVersion" 
properties are set as follows in your enabler's container.xml:

```xml
    <script class="com.datasynapse.fabric.common.script.Script">
        <property name="name" value="enabler.rb"/>
        <property name="language" value="ruby"/>
        <property name="languageVersion" value="jruby 1.7.4"/>
    </script>
```
    
An example enabler script (referenced as "enabler.rb" in the XML above) in JRuby might look 
like the following:

```ruby
require 'java'
java_import com.datasynapse.fabric.admin.info.AllocationInfo
java_import com.datasynapse.fabric.util.GridlibUtils
java_import com.datasynapse.fabric.util.ContainerUtils
java_import com.datasynapse.fabric.common.RuntimeContextVariable
java_import com.datasynapse.fabric.common.ActivationInfo
java_import java.lang.System

def prepareWorkDirectory
    $proxy.prepareWorkDirectory()
    
    System.out.println("preparing work directory")
    # do stuff here
end

def doInit(*args)
    $proxy.doInit(args)
    
    stringHello= "Hello World"
    stringDate = java.util.Date.new
    puts "#{stringHello.to_s}"
    puts "Date := #{stringDate.to_s}"
    # etc
end

def doStart
    $proxy.doStart()
    
    System.out.println("doStart() called")
    # do stuff here
end
    
def doInstall(info)
    $proxy.doInstall(info)
    
    System.out.println("doInstall() called")
    # do stuff here
end
    
# ... etc ...
```

NOTE: this is not a complete enabler implementation and only serves as an example guide to get started. 
Consult the Silver Fabric documentation for more information.