What is Off-peak Bandwidth?
===========================

In its simplest terms, off-peak bandwidth is when an external network connection is not near its maximum rate for the previous month.  
  
So if we bought a 25 Gbit/s off another ISP, then that connection would be considered off-peak while it's doing less than 20-25 Gbit/s. Anything above 20-25 Gbit/s would be on-peak.  
  

### Can you provide a concrete example?

  
Feral runs its own ISP which means we buy traffic from more than one ISP. One of those ISPs is called GTT where we have 40 Gbit/s of capacity to and from. We're constantly monitoring the rate of this traffic and over the course of a month we can see that it might use 20 Gbit/s at the busiest times. When this connection gets close to the 20 Gbit/s our system considers the connection to be on-peak traffic and starts switching off any bandwidth that's considered off-peak.  
  

When are connections considered off-peak?
-----------------------------------------

  
There is no specific cross-over point when connections are considered off-peak as it varies depending on what else is happening on the network and the connection itself. For example, we may purchase extra bandwidth with one provider to encourage growth meaning that it's considered off-peak for much longer than normal.  
  
You should also bear in mind that the off-peak bandwidth is assessed per connection. So while GTT might be considered on-peak, connections via AMS-IX will probably still be off-peak.  
  
Our peak hour is typically Saturday evening in Europe for 2-3 hours. This small timeframe is when you're likely to see connections move to on-peak only.  
  

### Which connections are likely to be off-peak?

  
The answer to this depends heavily on the connection. We are eager to promote traffic to ISPs with open peering policies as it lowers the costs for everyone involved. This means that connections flowing over exchanges such as AMS-IX, NL-IX, LINX, and so forth are all likely to be considered permanently off-peak.  
  
Access to exchanges through third-parties such as via IX Reach and Open Peering are also likely to remain off-peak for much longer.  
  
The majority of IPv6 traffic currently flows via AMS-IX which means that it is likely to always be considered off-peak.  
  

### What is the current status of traffic?

  
Our status page reports network statistics in real-time and gives an indication of whether a connection is off-peak: <http://status.feral.io/>  
  

What will happen when a connection moves from off to on-peak?
-------------------------------------------------------------

  
If your slot has off-peak bandwidth then traffic flowing over that connection will instantly stop. You will see immediate failures when trying to make the connection with something along the lines of "no route to host" or "connection failed".  
  
When the connection moves back to off-peak, you will be able to make new connections to the IP.  
  

### What if my IP was using an on-peak connection?

  
If this is the case your server will not accept connections from your IP. However, we allow you to change the connection your IP uses so you can bypass this restriction easily.  
  
Please use the reroute tool to bypass this: <https://network.feral.io/reroute>  
  

Technically, how is it enforced?
--------------------------------

  
When a connection moves to on-peak, off-peak only servers will begin dropping packets. This typically happens within the minute.  
  
If you login to your server via SSH you can check the connections that are definitely on-peak with the following command: ip rule  
  
When no connections are on-peak it will produce a result such as:  
  

    [lion ~] ip rule
    0:  from all lookup local 
    10000:  from all lookup protected 
    32766:  from all lookup main 
    32767:  from all lookup default

  
  
When a connection moves to on-peak, you will see an extra entry:  
  

    [lion ~] ip rule
    0:  from all lookup local 
    10000:  from all lookup protected 
    10107:  from all lookup gtt
    32766:  from all lookup main 
    32767:  from all lookup default

  
  
The highlighted entry shows that GTT has moved to on-peak traffic and is dropping connections.  
  

Summary
-------

  
In conclusion, you should see all connections as off-peak 90-95% of the time. When it's not, you can bypass them via [using the reroute page](https://network.feral.io/reroute%0D%0A).  

