# Bonus! Red Log4Jack

The screen to start is very complex, but I'm going to copy paste specific things so they're readable. It generally looked like this:


![General look](img/bonus_red/img1.png)

Confirmed the endpoint `http://solrpower.kringlecastle.com:8983/solr/` is running Solr

![Confirmed solr](img/bonus_red/img2.png)

Running the marshalsec marshalling service to exploit:

![Marshalsec](img/bonus_red/img3.png)

Code I'm going to compile which will be marshalled, waiting for java to pick it up an deserialize it, causing a shell to bounce back.

![Code to compile](img/bonus_red/img4.png)

The result:

![Result](img/bonus_red/img5.png)

Triggering the exploit:

![Triggering the exploit](img/bonus_red/img6.png)

JNDI reaches out to my ldap server responder:

![JNDI](img/bonus_red/img7.png)

LDAP server responds with a redirection to my waiting web server to deliver the `YuleLogExploit.class` file:

![LDAP responds](img/bonus_red/img8.png)

Netcat shell!

![Netcat shell](img/bonus_red/img9.png)

Found in `/home/solr`, the file `kringle.txt`

![Found in /home/solr](img/bonus_red/img10.png)

And submitting the answer:

![Submitting answer](img/bonus_red/img11.png)