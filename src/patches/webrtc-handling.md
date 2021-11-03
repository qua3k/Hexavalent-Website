# WebRTC IP Handling

WebRTC enables users to communicate peer-to-peer in real time, and it does so by
using the Interactive Connectivity Establishment (ICE) protocol. In turn, ICE
uses techniques such as STUN and TURN to enumerate interfaces and determine the
best route, leading the server to learn more about the local network
configuration than a typical HTTP request, such as the client's `RFC1918`
addresses.

However, the largest concern stems from the fact that the default configuration
reveals clients' ISP public address even when they are behind a proxy. We expose
a toggle to change the IP handling mode and set the default to
"Default Route Only".

## See also

*   [https://datatracker.ietf.org/doc/html/rfc8828](https://datatracker.ietf.org/doc/html/rfc8828)

Credits: the Hexavalent team