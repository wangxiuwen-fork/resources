# Install gradle 3.3 in Ubuntu
    
    sudo -E add-apt-repository ppa:cwchien/gradle
    apt-cache search gradle
    sudo apt-get install gradle-3.3

After installation:

    $ gradle -v
    
    ------------------------------------------------------------
    Gradle 3.3
    ------------------------------------------------------------
    
    Build time:   2017-01-03 15:31:04 UTC
    Revision:     075893a3d0798c0c1f322899b41ceca82e4e134b
    
    Groovy:       2.4.7
    Ant:          Apache Ant(TM) version 1.9.6 compiled on June 29 2015
    JVM:          1.8.0_66 (Oracle Corporation 25.66-b17)
    OS:           Linux 3.13.0-37-generic amd64
    
## Proxy pour gradle

Set it in gradle.properties.

https://docs.gradle.org/current/userguide/build_environment.html#sec:accessing_the_web_via_a_proxy
    
    systemProp.http.proxyHost=www.somehost.org
    systemProp.http.proxyPort=8080
    systemProp.http.proxyUser=userid
    systemProp.http.proxyPassword=password
    systemProp.http.nonProxyHosts=*.nonproxyrepos.com|localhost
    
    systemProp.https.proxyHost=www.somehost.org
    systemProp.https.proxyPort=8080
    systemProp.https.proxyUser=userid
    systemProp.https.proxyPassword=password
    systemProp.https.nonProxyHosts=*.nonproxyrepos.com|localhost


