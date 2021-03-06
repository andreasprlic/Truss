<h3>Truss</h3>
<hr>
<h5>Purpose & Summary</h5>
<p><strong>Truss is a lightweight secure middleware for distributed computing.</strong> The goal of Truss is to provide a simple framework for securely routing jobs, and collecting the produced output, over a heterogeneous network of computers. This means that clients and servers running Truss do not have to be on the same operating system, hardware, or asserted trust level.</p>
<br>
<h5>A high level architecture overview</h5>
<center>
![alt tag](https://raw.github.com/MrColeC/Truss/master/Images/TrussArchitecture.png)
</center>

<h5>Truss accomplishes this by:</h5>
<ul>
  <li>Having a single lightweight code base that is used to implement both clients as well as servers</li>
  <li>Providing a simple and extensible means of authenticating the client (from using a local configuration file within the code, to LDAP integration or other forms of single sign on)</li>
  <li>Encrypting all network traffic with AES128, providing both a reasonable degree of security as well as minimal overhead when compared with plain text transmissions</li>
  <li>Using pre-shared keys to provide a password-authenticated Diffie-Hellman key agreement in order to prevent man-in-the-middle attacks</li>
  <li>Re-negotiating the established Diffie-Hellman agreements periodically in order to prevent an attackers ability to break the encryption and read all previous or future network traffic</li>
</ul>
<br>
<hr>
<h5>How to compile the code from source</h5>
<p>This project uses 100% Mavenized Java code. This means you will need the following in order to compile the code from source:</p>
<ol>
<li>A copy of code (available via Git)</li>
<li>A Java JDK</li>
<li>Maven installed on your system</li>
</ol>
<p>Once these prerequisites are made, all you need to do is go to the root of the checkout (this will contain the pom.xml for this project) and then run: <strong>mvn clean compile assembly:single</strong>. This will download all required dependencies and then compile the project into a single portable jar file.</p>
<br>
<hr>
<h5>Runtime (JVM) variables:</h5>
<table>
<tr><th>Description</th><th>Paramater</th><th>Options and Default Value</th><th>Applies To</th></tr>
<tr><td>To set the log verbosity</td><td>loglevel</td><td>off,info,warn,error,fatal (defaults to fatal)</td><td>All</td><tr>
<tr><td>To provide the username</td><td>user</td><td>(default is to prompt the user)</td><td>All</td></tr>
<tr><td>To provide the users password</td><td>pass</td><td>(default is to prompt the user)</td><td>All</td></tr>
<tr><td>To provide the pre shared key</td><td>key</td><td>(default is to prompt the user)</td><td>All</td></tr>
<tr><td>Servers IP address</td><td>sip</td><td>(default is 127.0.0.1)</td><td>Client</td></tr>
<tr><td>The servers port</td><td>sport</td><td>(default is 8080)</td><td>Client</td></tr>
<tr><td>The drop off points IP</td><td>dip</td><td>(default is 127.0.0.1)</td><td>Client</td></tr>
<tr><td>The drop off points port</td><td>dport</td><td>(default is 8080)</td><td>Client</td></tr>
<tr><td>Interactive mode</td><td>ic</td><td>(default is an automatic client, no GUI provided)</td><td>Client</td></tr>
<tr><td>The port to listen on</td><td>bind</td><td>(default is 8080)</td><td>Server/Drop Off</td></tr>
</table>
<br>
<h5>Examples of how to launch the code:</h5>
<strong>Note:</strong> The default password for all accounts is "pw". This can be changed in the Shiro.ini file inside the source code. Also, in that same file, Shiro can be integrated with other authentication systems.<br>
<strong>Note:</strong> The pre-shared key can be anything you want. Longer keys do provide additional security, but keep in mind that the pre-shared key is only used to facilitate the secure negotiation of a new completely random key and will have no lasting impact on the security of the infrastructure.<br>
<strong>Note:</strong> The ports that the server and drop off server bind to can be anything. However, using ports above 1024 is recommended so in order to not require root or escalated privileges (on some systems).
<h6>This would launch a server</h6>
java -Duser=server -Dpass=<i>password</i> -Dkey=<i>pre_shared_key</i> -Dloglevel=info -Dbind=<i>server_port</i> -jar Truss*.jar
<br>
<h6>This would launch a drop off server</h6>
java -Duser=dropoff -Dpass=<i>password</i> -Dkey=<i>pre_shared_key</i> -Dloglevel=info -Dbind=<i>server_port</i> -jar Truss*.jar
<br>
<h6>This would launch an interactive secure client</h6>
java -Duser=secure -Dpass=<i>password</i> -Dkey=<i>pre_shared_key</i> -Dloglevel=info -Dsip=<i>server_ip</i> -Dsport=<i>server_port</i> -Ddip=<i>drop_off_server_ip</i> -Ddport=<i>drop_off_server_port</i> -Dic -jar Truss*.jar
<br>
<h6>This would launch an interactive secure client</h6>
java -Duser=insecure -Dpass=<i>password</i> -Dkey=<i>pre_shared_key</i> -Dloglevel=info -Dsip=<i>server_ip</i> -Dsport=<i>server_port</i> -Ddip=<i>drop_off_server_ip</i> -Ddport=<i>drop_off_server_port</i> -Dic -jar Truss*.jar
<br>

