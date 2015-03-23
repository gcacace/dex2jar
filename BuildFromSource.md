## Environment Required ##
  1. [Maven](http://maven.apache.org/)
  1. [Mercurial](http://mercurial.selenic.com/)
  1. [JDK6+](http://www.oracle.com)

## Progress ##
  1. get source from googlecode
```
# clone new hg repository from googlecode
hg clone https://dex2jar.googlecode.com/hg dex2jar
cd dex2jar
# or update exists hg repository from googlecode
cd dex2jar
hg pull https://dex2jar.googlecode.com/hg
```
  1. switch to branche 0.0.9.x
```
hg up -r 0.0.9.x
```
  1. build the project
```
mvn install
```

if build successfull, the zip file is under dex-tools/target/.
