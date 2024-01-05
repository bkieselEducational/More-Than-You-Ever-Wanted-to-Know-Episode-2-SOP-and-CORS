# More Than You Ever Wanted to Know: Episode 2 - SOP and CORS

## What is the Same Origin Policy (SOP)?

The Same Origin Policy is a web security feature that is built into the browser itself! What it does is, ensures a certain level of security by blocking access to the HTTP response sent by a server from a different Origin. Before we go any further, let's clarify what an 'Origin' is! An Origin is the address derived when concatenating 3 pieces of information about a server. 1) Protocol (some call this a 'scheme'): This is the Protocol that will be used to establish communications between the client and server. In our case, this value will be either, HTTP or HTTPS. 2) Domain Name: The human readable name that we bind to an IP Address to make the web more user-friendly. In your case, this will look something like: my-awesome-capstone.onrender.com. Again, Domain Names are mapped to IP Addresses. The IP Address is the way that we route to a specific host/computer connected to the internet using the IP Layer of the network stack. 3) Port Number: Port numbers are really another layer of routing. Port numbers are used by the TCP protocol to route packets to different servers on the same host/computer. So ultimately, our Origin may look like: https://my-awesome-capstone.onrender.com:443.</br>
</br>
Now that we know what an Origin is, we can begin to appreciate what this policy is doing for us. So if the browser blocks access to the response of a potentially nefarious source, this helps protect the client from downloading and running code from a source that may be malicious. At a minimum, we know it's not our code and it's a good safety measure to block it by default. But what about when we don't want to block access to the response from a different Origin?...

## What is Cross-Origin Resource Sharing (CORS)?

CORS was developed to essentially, circumvent the Same Origin Policy when desired. Meaning, it allows a developer to define some policies on their server that will allow access to the responses of the specific Cross-Origin Domains that they specify! How this is actually implemented is by use of HTTP Headers which are particular to CORS functionality. the headers are as follows:</br>
</br>
Origin: Sent by the browser with the request to indicate the origin of the request.

Access-Control-Allow-Origin: Returned by the server to specify which origins are allowed to access the resource. It can either be a single origin or "*", indicating any origin.

Access-Control-Allow-Methods: Specifies the HTTP methods (GET, POST, PUT, DELETE, etc.) permitted when accessing the resource.

Access-Control-Allow-Headers: Indicates which HTTP headers can be used during the actual request.

Access-Control-Allow-Credentials: A boolean value indicating whether the request can include credentials like cookies or HTTP authentication.

Access-Control-Expose-Headers: Lists the headers that the browser should expose to the requesting client.

Access-Control-Max-Age: Specifies how long the results of a preflight request can be cached, in seconds.

By the proper usage of the above headers, we can instruct the browser to allow access to the resources we desire and continue to block access to everything else!! Ensuring a certain level of security for our application.</br>
</br>
Another aspect of CORS that deserves a mention here is the Pre-Flight request. This is a special HTTP request that employs the OPTIONS method and is sent to a Cross-Origin server by the browser BEFORE sending the actual request to the Cross-Origin server. This allows the browser to get a response WITHOUT a body from the server that will convey the server's CORS configuration. Based on this special response, the browser can decide to commence with the sending of the request OR if the policy states that the browser would be blocking access to the response body anyway, the request is simply never sent in the first place! This can actually be QUITE beneficial for security as certain CSRF requests may not even get sent in the first place!! While there are ways to subvert the sending of a Pre-Flight OPTIONS request, it is a great default mechanism for SOP and CORS to employ!

# The OSI / Network Stack
As I mentioned this above, I wanted to also provide a visual aid in the hopes of making this more clear!
<img width="634" alt="network_stack" src="https://github.com/bkieselEducational/More-Than-You-Ever-Wanted-to-Know-Episode-2-SOP-and-CORS/assets/131717897/dcf1c510-45ec-48ce-a6e0-b63a18a600ae">
