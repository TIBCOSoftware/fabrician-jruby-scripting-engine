jruby-scripting-engine
======================

This project builds a JRuby grid library for use in creating Silver Fabric enablers in JRuby.

To build the grid library, you must have Maven installed and set in your path. Then, run the
following:

  mvn package
  
If successful, the grid library will be created under the project root's target/ directory.
It can then be copied to your Silver Fabric Broker's 

  SF_HOME/webapps/livecluster/deploy/resources/gridlib

directory.

To use JRuby for a Silver Fabric enabler, make sure your "language" and "languageVersion" 
properties are set as follows in your enabler's container.xml:

    <script class="com.datasynapse.fabric.common.script.Script">
        <property name="name" value="enabler.rb"/>
        <property name="language" value="ruby"/>
        <property name="languageVersion" value="jruby 1.7.4"/>
    </script>
    
An example enabler script (referenced as "enabler.rb" in the XML above) in JRuby might look 
like the following:

--- START ---
require 'java'
java_import com.datasynapse.fabric.admin.info.AllocationInfo
java_import com.datasynapse.fabric.util.GridlibUtils
java_import com.datasynapse.fabric.util.ContainerUtils
java_import com.datasynapse.fabric.common.RuntimeContextVariable
java_import com.datasynapse.fabric.common.ActivationInfo
java_import java.lang.System

def prepareWorkDirectory
    System.out.println("preparing work directory")
    # do stuff here
end

def doInit(*args)
    stringHello= "Hello World"
    stringDate = java.util.Date.new
    puts "#{stringHello.to_s}"
    puts "Date := #{stringDate.to_s}"
    # etc
end

def doStart
    System.out.println("doStart() called")
    # do stuff here
end
    
def doInstall(info)
    System.out.println("doInstall() called")
    # do stuff here
end
    
# ... etc ...
--- END ---

NOTE: this is not a complete enabler implementation and only serves as an example guide to get started. 
Consult the Silver Fabric documentation for more information.
