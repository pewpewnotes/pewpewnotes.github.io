[###](###) Logstash Errors

1. `logstash not found`
* Usually Ubuntu installs it in non standard location, 
  go to `/usr/share/logstash/bin` and see if its in there, then simply add it to your 
  path `export PATH=$PATH:/usr/share/logstash/bin`
  
2. `logstash not working`

Its slow, be patient, you need atleast 4gb ram for it to work. Give it a running of atleast
30mins before making conclusions xD

3. `Weird warnings and stuffs`

```
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.jruby.util.SecurityHelper (file:/Users/chrisuser/logstash-6.7.0/logstash-core/lib/jars/jruby-complete-9.2.6.0.jar) to field java.lang.reflect.Field.modifiers
WARNING: Please consider reporting this to the maintainers of org.jruby.util.SecurityHelper
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
```
This is a standard issue with jruby and java (idk why java but well its there :(  )
to fix this you need to modify jvm.options file in `/etc/logstash/jvm.options` 
Simply append this: 

```
--add-opens=java.base/java.lang=ALL-UNNAMED
--add-opens=java.base/java.security=ALL-UNNAMED
--add-opens=java.base/java.util=ALL-UNNAMED
--add-opens=java.base/java.security.cert=ALL-UNNAMED
--add-opens=java.base/java.util.zip=ALL-UNNAMED
--add-opens=java.base/java.lang.reflect=ALL-UNNAMED
--add-opens=java.base/java.util.regex=ALL-UNNAMED
--add-opens=java.base/java.net=ALL-UNNAMED
--add-opens=java.base/java.io=ALL-UNNAMED
--add-opens=java.base/java.lang=ALL-UNNAMED
--add-opens=java.base/javax.crypto=ALL-UNNAMED
--add-opens=java.management/sun.management=ALL-UNNAMED
```
Do note that it will prevent working using java 8, this fixes for java 11.

Whatever happens, use java 8, or else the system just behaves wayyyy unpredictably.

### Optimising logstash for lowend machines

Basically increase the processor number to two and increase ram, messing with jvm options helps but don't fix everything. 

#### List of plugins available.
There are many, find the list in docs for logstash.
