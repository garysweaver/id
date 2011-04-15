Id
=====

A simple Java webapp called "id" that outputs the hostname and domain when you hit it.

e.g. if service.acme.net resolves to tomcat-01.acme.net or tomcat-02.acme.net, a request to http://service.acme.net/id/ would result in either the response (without the quotes) "tomcat-01.acme.net" or "tomcat-02.acme.net", depending on which server served the request.

### Technical Detail

It is basically just the scriptlet:

    <%= java.net.InetAddress.getLocalHost().getHostName() %>

The precompiled version uses JSPC to precompile this to make it just a little bit faster on first hit. This was compiled in Java 1.4 to hopefully be compatible with most environments. If you have any trouble with the precompiled JSP, use the war without precompiled JSP download.

### Download

War without precompiled JSP: [id.war][war]

OR

War with JSP precompiled with JSPC in Java 1.4: [id.war][jspc]

### Deploy

Copy it into the webapps directory in Tomcat or the appropriate place in your Java application server, assuming you have it configured to automatically extract/deploy war files.

### Use

Using a browser or other means, make a request to the id webapp (for example: http://yourserver/id/ ) to see the host and domain of the server.

### Build

If you need to build it, first install Maven 2 and Java, then use the command:

    mvn clean install
    
The built war should be in target/id.war

By default, this compiles the JSP using the current version of Java available to Maven, which can be defined by JAVA_HOME. If you need to build the non-precompiled version, then remove the JSPC plugin section from the pom.xml before building.

e.g. in OS X 10.6 (Snow Leopard), to build with Java 1.4 on newer systems, you must first [install Java 1.4][java4snowleopard], then use the following to set the Java version to 1.4 prior to build (if using bash, the default):

    export JAVA_HOME=/System/Library/Frameworks/JavaVM.framework/Versions/1.4/Home/

To ensure the class was built in the version less or equal to the version of Java on the server:

1. Change your current directory to (webapps)/WEB-INF/classes/
2. Use the command:

        javap -verbose index_jsp
3. In the first several lines of the output you will see something like:

          minor version: 0
          major version: 48

Use the table below to determine the version of Java the class was actually compiled in (from [Réal's How To][javaclassversion].):

    major  minor Java platform version 
    45       3           1.0
    45       3           1.1
    46       0           1.2
    47       0           1.3
    48       0           1.4
    49       0           1.5 (5.0)
    50       0           1.6 (6.0)
    51       0           1.7 (7.0)

### License

Copyright (c) 2011 Gary S. Weaver, released under the [MIT license][lic].

[war]: https://github.com/garysweaver/id/raw/master/dist/notcompiled/id.war
[jspc]: https://github.com/garysweaver/id/raw/master/dist/compiled/id.war
[java4snowleopard]: http://tedwise.com/2009/09/25/using-java-1-5-and-java-1-4-on-snow-leopard/
[javaclassversion]: http://www.rgagnon.com/javadetails/java-0544.html
[lic]: http://github.com/garysweaver/id/blob/master/LICENSE
