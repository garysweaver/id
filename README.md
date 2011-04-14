Id
=====

A simple Java webapp called "id" that outputs the hostname and domain when you hit it. For example, if the load balanced virtual host you use to made a request to the server were service.acme.net but the actual host was tomcat-01.acme.net the output from making a request to http://service.acme.net/id/ would be tomcat-01.acme.net.

### About

While there are other better ways of getting information from the running JVM and ensuring your application server is up and running, id is an ok option if you just want a webapp that returns the server's hostname. It is basically just a JSP containing the scriplet:

    <%= java.net.InetAddress.getLocalHost().getHostName() %>

### Download

Right-click to download [id.war][war].

### Deploy

Copy it into the webapps directory in Tomcat or the appropriate place in your Java application server (assuming you have it configured to automatically extract/deploy war files).

### Use

Using a browser or other means, make a request to the id webapp (for example: http://yourserver/id/ ) to see the host and domain of the server.

### Build

If you need to build it, first install Maven 2 and Java, then use the command:

    mvn clean install
    
The built war should be in target/id.war

### License

Copyright (c) 2010 Gary S. Weaver, released under the [MIT license][lic].

[war]: https://github.com/garysweaver/id/raw/master/dist/id.war
[lic]: http://github.com/garysweaver/id/blob/master/LICENSE
