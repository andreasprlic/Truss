<h3>Truss</h3>
<hr>
<p><strong>Truss is a lightweight secure middleware for distributed computing.</strong> The goal of Truss is to provide a simple framework of securly routing jobs, and collecting the produced output, over a heterogenous network of computers. This means that clients and servers running Truss do not have to be on the same operating system, hardware, or asserted trust level.</p>

<p>Truss accomplishes this by:</p>
<ul>
  <li>Having a single lightweight code base that is used to implement both clients as well as servers</li>
  <li>Providing a simple and extensible means of authenticating the client (from using a local configuration file within the code, to LDAP integration or other forms of single sign on)</li>
  <li>Encrypting all network traffic with AES128, providing both a reasonably degree of security as well as minimal additional costs over plain test transmissions</li>
  <li>Using pre-shared keys to provide a password-authenticated Diffie-Hellman key agreement in order to prevent man-in-the-middle attacks</li>
  <li>Re-negotiating the established Diffie-Hellman agreements periodically in order to prevent an attackers ability to break the encryption and read all previous or future network traffic</li>
  <li></li>
  <li></li>
</ul>

<b>Runtime (JVM) variables:</b><br>
<table>
<tr><th>Description</th><th>Paramater</th><th>Options and Default Value</th><th>Applies To</th></tr>
<tr><td>To set the log verbosity</td><td>loglevel</td><td>off,info,warn,error,fatal (defaults to fatal)</td><td>All</td><tr>
<tr><td>To provide the username</td><td>user</td><td>(default is to prompt the user)</td><td>All</td></tr>
<tr><td>To provide the users password</td><td>pass</td><td>(default is to prompt the user)</td><td>All</td></tr>
<tr><td>To previde the pre shared key</td><td>key</td><td>(default is to prompt the user)</td><td>All</td></tr>
<tr><td>Servers IP address</td><td>sip</td><td>(default is 127.0.0.1)</td><td>Client</td></tr>
<tr><td>The servers port</td><td>sport</td><td>(default is 8080)</td><td>Client</td></tr>
<tr><td>The drop off points IP</td><td>dip</td><td>(default is 127.0.0.1)</td><td>Client</td></tr>
<tr><td>The drop off poitns port</td><td>dport</td><td>(default is 8080)</td><td>Client</td></tr>
<tr><td>The port to listen on</td><td>bind</td><td>(default is 8080)</td><td>Server/Drop Off</td></tr>
<tr><td>Interactive mode</td><td>ic</td><td>(default is an automatic client)</td><td>Client</td></tr>
</table>

<h5>Paramater Example:</h5>
-Duser=<i>user_name</i> -Dpass=<i>password</i> -Dkey=<i>pre_shared_key</i> -Dloglevel=info -Dsip=192.168.0.121 -Dsport=8080 -Ddip=192.168.0.121 -Ddport=8081 -Dic
