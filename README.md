
<h1>Introduction</h1>

<p>Representational State Transfer (REST) is an architectural
style defined by Roy Fielding in 2000 in his PhD dissertation. REST describes a
web architecture that is not specific to web APIs. However, it has become the
most popular style of web API, overtaking SOAP in 2008. REST APIs are simple to
use, scalable, portable and easy to integrate with. The aim of this paper is to
look at what constraints are involved in creating a RESTful API and what the
best practices are for web REST APIs.</p>

<h1><a>REST Constraints</a></h1>
<ul>
  <li>Client-Server</li>
  <li>Stateless</li>
  <li>Cache</li>
  <li>Uniform interface</li>
  <li>Layered System</li>
  <li>Code-On-Demand (optional)</li>
</ul>

<h2><a>Client-Server</a></h2>

<p>The Client-Server constraint is focused on separation of
concerns. By separating the front end UI from the back end data storage
concerns, portability and scalability are improved. This also allows the
separate components to evolve independently.</p>


<h2><a>Stateless</a></h2>

<p>The server should not store any state of the current
session.<span>  </span>This means every request sent
from the client to the server should include all information necessary to
fulfil that request. Session state is managed solely by the client. </p>

<p>The pros of this constraint are visibility, reliability and
scalability. Visibility is improved because the server only has to deal with
one request and the information that was sent with it. Reliability and
scalability are improved because the server is not storing any session
information so session information does not have to be copied across multiple
server instances in case of a server failure and this allows for easy
scalability for the same reason. </p>

<p>The con is that common information will have to get sent
with each request (e.g. user authentication information) which will decrease
network performance. Having the client store all session state reduces the
servers control with consistent application behaviour because of multiple
client versions</p>

<h2><a>Cache</a></h2>

<p>The cache constraint is to improve network efficiency and
hence improve user-perceived performance. Each request can either be cacheable
or non-cacheable. If a response is cacheable, the client can use the cached
response for the same request later on. </p>

<p>The major benefit of caching is performance. Allowing
certain responses to be cacheable allows for fewer requests to the server and
much faster retrieval of cached data for the client.</p>

<p>The disadvantage is if cached data differs from data that
would have been sent back if the request had reached the server. This needs to
be maintained by having a time limit on the how long the response should be
cached for.</p>

<p></p>

<h2><a>Uniform Interface</a></h2>

<p>This constraint is what distinguishes REST from other
network-based architectural styles. The constraint states that all services and
service consumers must share a single, overarching technical interface. The
uniform interface is generally applied using methods and media types provided
by HTTP. This constraint will be the main area of focus for best practices because
the API design is how other developers will see the API and interact with it. Four
sub constraints are defined to achieve the uniform interface constraint, these
are</p>

<ul>
  <li>Identification of resources</li>
  <li>Manipulation of resources through representations</li>
  <li>Self-descriptive messages</li>
  <li>Hypermedia as the engine of application state(HATEOAS)</li>
</ul>

<h3>Identification of resources</h3>

<p>Fielding defines a resource as “Any information that can be
named: a document or image, a temporal service (e.g. today's weather in
Los Angeles), a collection of other resources, a non-virtual object (e.g.
a person)”. In web based REST APIs, resources are identified using URIs. The
resources are conceptually separate from the representation returned to the
client. The server sends a representation of a resource using HTML, XML, JSON
or other formats.</p>

<h3>Manipulation of resources through representations</h3>

<p>The representation of the resource that the client stores
should have all the information necessary to manipulate the resource itself
through the API (modify or delete).</p>

<h3>Self-descriptive messages</h3>

<p>The message response from the API should include the
information necessary to tell the client how to process the message. With web
REST APIs, this is done using internet media types. In the response header, the
Content-type field will have a value describing the message body format e.g. application/json.
Responses should also outline the cache criteria.</p>

<h3>Hypermedia as the engine of application state (HATEOAS)</h3>

<p>One initial base resource should be the entry point to the
API. Clients should then receive applicable actions from the server. Hypermedia
in web REST APIs are hyperlinks within hypertext. For example, if the client
retrieves a resource representation, the response should include other applicable
actions that can be taken on that resource like modifying or delete with the
URI hyperlink for each.</p>

<p></p>

<h2><a>Layered System</a></h2>

<p>The layered system builds on top of the Client-Server
architecture and describes a system that is made up of multiple architectural
layers. The constraint outlines that each layer should only know about the
immediate layer it is interacting with. </p>

<p>By restricting the knowledge of what other layers a layer
knows about, this decreases complexity and allows for easier scalability by allowing
load balancing of services. Also, additional middleware will be easier to
integrate.</p>

<p>The main disadvantage is increased overhead and latency.
This can be mitigated with the cache constraint, allowing cached content at the
boundaries of the separate layers where applicable.</p>

<p></p>

<h2><a>Code-On-Demand (optional)</a></h2>

<p>This constraint allows client functionality to be extended
by the server sending executable code in the form of applets or scripts. This
means that additional modules can be executed on the client when necessary or
needed. </p>

<p>This constraint is optional so it can be excluded without
violating the principles of REST.</p>

<h1></h1>

<h1><a>RESTful Web API Best Practices</a></h1>

<h2><a>URL structure</a></h2>

<p>The base URL is the entry point of the API. The path after
the base should identify a resource or collection of resources. The query
parameter is appended to the end of the resource path.</p>

mso-fareast-language:EN-GB'>http://example.com/users/1234/activities?activityType=running</span></p>


<p>
  Base URL
<span></span>
<span></span>
Resource
<span></span>
<span></span>
Query Parameter
</p>

<p>In the above example, the resource should be viewed in a
hierarchical way. ‘/Users’ is a top level collection. ‘/1234’ is the id that
identifies a unique user. ‘/activities’ is a collection of activity resources
specific to the user 1234.</p>

<p></p>

<h2><a>Resource Naming</a></h2>

<p>The URIs that identify resources are arguably the most important
to get right because they are the most visible part of the API. <span> </span></p>

<h3>Only 2 URIs per resource</h3>

<p>
<span></span>
/users

</p>
<p>
<span></span>
/users/1234

</p>


<p>The first is a collection of resources, the second is a
specific resource in the collection. In this case, all users and a specific
user.</p>

<h3>Nouns, not verbs</h3>

<p>Keep verbs out of the resource name. The HTTP method is what
describes the action for the request. Resource names should be nouns but plural
nouns are preferable. Readability is paramount with a consistent pattern. With
the verb approach, different developers will come up with vastly different
naming schemes and they are not easy to learn. Using nouns, the API is easier
to understand and read. Plural nouns are always preferred to keep consistency
and understanding. The /users collection compared /user tells the reader that
it identifies all users, not just one. </p>

<p><b>Examples with verbs -
Bad</b></p>

<p>/getUsers</p>

<p>/createUser</p>

<p>/saveUser</p>

<p>/getUserActivities</p>

<p>/updateUserActivity</p>

<p>/deleteActivities</p>

<p>/deleteUserActivity</p>

<p></p>

<p><b>Examples with nouns –
Good</b></p>

<p>The HTTP methods on the right are what would be used as an equivalent
to the bad URIs.</p>

<p>/users<span>                                                   </span>GET(getUsers),
POST(createUser)</p>

<p>/users/1234<span>                                        </span>PUT(saveUser)</p>

<p>/users/1234/activities<span>                    </span>GET(getUserActivities),
DELETE(deleteActivities)</p>

<p>/users/1234/activities/4321<span>         </span>PUT(updateUserActivity),
DELETE(deleteUserActivity)</p>

<p></p>

<h3>Lower case</h3>

<p>Consistency is key with casing. Lower case is easier to type
in and no confusion can occur when trying to remember the casing. Mixed case
might also cause ambiguity.</p>

<h3>Keep It Intuitive</h3>

<p>URIs should be human-guessable, meaningful and predictable.
The name should tell the user what they are looking at.
‘/users/1234/activities’ should give a hint that the URI identifies the
activities collection for user 1234. When URIs are meaningful like this, a user
should be able to predict or guess other URIs if they know some of the API.</p>

<h3>Hackable</h3>

<p>The hierarchy of resources should allow the user to remove the
leaf path and access the parent resource. By removing the ‘activities’ leaf
path from the example URIs above, we are left with ‘/users/1234’ which we would
expect identifies a unique user. Again, by removing the remaining leaf path
‘1234’, we expect ‘/users’ identifies a collection of users. Lower case names</p>

<p></p>

<h2><a>When/what to use query parameters for</a> </h2>

<p>URI query parameters are used for filtering, searching, sorting
and pagination.</p>

<h3>Filtering or searching</h3>

<p>Send a unique value for the field(s) to be filtered/searched,
for example <span>/users?firstname=david&amp;age=24</span>. Each
additional field should be preceded with an ‘&amp;’. This will return the users
that only have a name of ‘david’ and an age of 24. </p>

<h3>Sorting</h3>

<p>Sorting needs two criteria, the field to sort and the
direction of the sort. The direction should be ASC (ascending) or DESC (descending).
For example <span>/users?sort=email&amp;dir=DESC</span>.</p>

<h3>Pagination</h3>

<p>Pagination also requires two parameters. The item to start on
(start) and how many items to return (limit). For example <span>
/users?start=60&amp;limit=20</span> will return the items from 60-79.</p>

<p></p>

<h2><a>HTTP Methods</a> </h2>

<table class=MsoTableLightListAccent3 border=1 cellspacing=0 cellpadding=0
 style='border-collapse:collapse;border:none;mso-border-alt:solid #9BBB59 1.0pt;
 mso-border-themecolor:accent3;mso-yfti-tbllook:1184;mso-padding-alt:0cm 5.4pt 0cm 5.4pt;
 mso-border-insideh:1.0pt solid #9BBB59;mso-border-insideh-themecolor:accent3;
 mso-border-insidev:1.0pt solid #9BBB59;mso-border-insidev-themecolor:accent3'>
 <tr style='mso-yfti-irow:-1;mso-yfti-firstrow:yes'>
  <td width=123 style='width:92.4pt;border:solid #9BBB59 1.0pt;mso-border-themecolor:
  accent3;background:#9BBB59;mso-background-themecolor:accent3;padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:5'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:5'><b><span
  style='color:white;mso-themecolor:background1'>Resource</span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:5'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  </td>
  <td width=123 valign=top style='width:92.4pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-left:none;mso-border-left-alt:solid #9BBB59 1.0pt;
  mso-border-left-themecolor:accent3;background:#9BBB59;mso-background-themecolor:
  accent3;padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'>POST</span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><span style='color:
  white;mso-themecolor:background1;mso-bidi-font-weight:bold'>create</span></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  </td>
  <td width=123 valign=top style='width:92.4pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-left:none;mso-border-left-alt:solid #9BBB59 1.0pt;
  mso-border-left-themecolor:accent3;background:#9BBB59;mso-background-themecolor:
  accent3;padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'>GET</span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><span style='color:
  white;mso-themecolor:background1;mso-bidi-font-weight:bold'>read</span></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  </td>
  <td width=123 valign=top style='width:92.45pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-left:none;mso-border-left-alt:solid #9BBB59 1.0pt;
  mso-border-left-themecolor:accent3;background:#9BBB59;mso-background-themecolor:
  accent3;padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'>PUT</span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><span style='color:
  white;mso-themecolor:background1;mso-bidi-font-weight:bold'>update</span></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  </td>
  <td width=123 valign=top style='width:92.45pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-left:none;mso-border-left-alt:solid #9BBB59 1.0pt;
  mso-border-left-themecolor:accent3;background:#9BBB59;mso-background-themecolor:
  accent3;padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'>DELETE</span></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><span style='color:
  white;mso-themecolor:background1;mso-bidi-font-weight:bold'>delete</span></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:1'><b><span
  style='color:white;mso-themecolor:background1'></span></b></p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:0'>
  <td width=123 valign=top style='width:92.4pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-top:none;mso-border-top-alt:solid #9BBB59 1.0pt;
  mso-border-top-themecolor:accent3;background:#D6E3BC;mso-background-themecolor:
  accent3;mso-background-themetint:102;padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:68'><b></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:68'><b>/users</b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:68'><b></b></p>
  </td>
  <td width=123 style='width:92.4pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:64'>Create a new user</p>
  </td>
  <td width=123 style='width:92.4pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:64'>List users</p>
  </td>
  <td width=123 style='width:92.45pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:64'>Bulk update users</p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:64'>or error</p>
  </td>
  <td width=123 style='width:92.45pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:64'>Delete all users </p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:64'>or error</p>
  </td>
 </tr>
 <tr style='mso-yfti-irow:1;mso-yfti-lastrow:yes'>
  <td width=123 valign=top style='width:92.4pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-top:none;mso-border-top-alt:solid #9BBB59 1.0pt;
  mso-border-top-themecolor:accent3;background:#D6E3BC;mso-background-themecolor:
  accent3;mso-background-themetint:102;padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:4'><b></b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:4'><b>/users/1234</b></p>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal;mso-yfti-cnfc:4'><b></b></p>
  </td>
  <td width=123 style='width:92.4pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal'>error</p>
  </td>
  <td width=123 style='width:92.4pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal'>List unique user</p>
  </td>
  <td width=123 style='width:92.45pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal'>Update user</p>
  </td>
  <td width=123 style='width:92.45pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>
  <p align=center style='margin-bottom:0cm;margin-bottom:.0001pt;
  text-align:center;line-height:normal'>Delete user</p>
  </td>
 </tr>
</table>

<p></p>

<p>The four HTTP methods map to CRUD. Create = POST, Read =
GET, Update = PUT and Delete = DELETE. The HTTP method determines what action
is performed on the resource. Web REST APIs use the HTTP protocol for requests/responses,
HTTP outlines a set of methods that can be used for requests and the four above
are the main ones used in REST APIs. In the above example, most APIs would not
allow a PUT or DELETE on a collection (/users) as this could be dangerous.</p>

<p>GET, PUT and DELETE are idempotent but POST is not. This
means, no matter how many times the idempotent request methods are sent, the
outcome will always be the same. With POST, a new resource will be created
every time.<span>  </span></p>

<p></p>

<h2><a>What to include in HTTP headers</a> </h2>

<p>HTTP headers should include metadata for the request and
response. This includes the body format, caching and authorisation fields. Below
are three examples of common header fields:</p>

<p><b>Content-Type:</b> The
format type of the request or response body. Used with POST and PUT. Example: <span>Content-Type: application/json.</span></p>

<p><b>Accept:</b> Request
only - Lists Content-Types acceptable for the response. Example: <span>Accept: text/plain; application/json.</span></p>

<p><b>Allow:</b> Response
only - Valid methods for the resource, if an invalid method was used.</p>

<h2><a>Caching</a></h2>

<p>The browser has a built in caching framework which can be
leveraged using cache specific HTTP headers in the response, these are <span>Cache-Control </span>and
<span>Etag.</span></p>

<p><b><span>Cache-Control:</span></b><span> </span>This
specifies how long the response should be cached for in seconds.<span>  </span>Example: <span>Cache-Control:<span>  </span></span><code><spa>max-age=3600.</span></code></p>

<p><b><span>Etag:</span></b>
A unique identifier for a specific version of a resource. Example: <span>ETag: “x234dff”.</span></p>

<p>When the cached response times out and another request is
made for the same resource, the browser will send the ETag token as a value of
a request header called <span>If-None-Match. </span>The server should check this token
against the current resource version and send back a response with a status
code of ‘304 Not modified’ if they match. The cache time-out will get then get
reset.</p>

<p><b><span>If-None-Match:</span></b><span> </span>Etag
token sent in new request. If the resource hasn’t changed, the response is ‘304
Not Modified’ and the cache time out is reset.</p>

<p></p>

<h2><a>Error handling</a></h2>

<h3>Standard HTTP status codes for error responses.<span>  </span></h3>

<p>HTTP status codes starting with 4xx are client errors and
5xx are server errors. Here are some examples of common error response status
codes.</p>

<p><span style='mso-tab-count:1'>                </span><b
style='mso-bidi-font-weight:normal'>400 Bad Request:</b> Malformed request
syntax</p>

<p><span style='mso-tab-count:1'>                </span><b
style='mso-bidi-font-weight:normal'>401 Unauthorized:</b> Authentication is
required or has failed</p>

<p><span style='mso-tab-count:1'>                </span><b
style='mso-bidi-font-weight:normal'>404 Not Found:</b> Requested resource could
not be found</p>

<p><span style='mso-tab-count:1'>                </span><b
style='mso-bidi-font-weight:normal'>405 Method Not Allowed:</b> HTTP method
used is not allowed on the resource</p>

<h3>Detailed error description </h3>

<p>The error message in the response should explain the problem
in human readable format. Let it be verbose, you shouldn’t be trying to save
bandwidth on errors. </p>

<h3>Internal error code</h3>

<p>Include the internal error code so it can be looked up for
more information. To go one step further, include a URL link in the response to
the specific internal error in your documentation.</p>

<h3>Extra: Allow HTTP status code override</h3>

<p>Allow a URL query parameter on all requests that will always
return a HTTP status code of 200. Twitter’s query param to allow this is ‘suppress_response_codes=true’.
The original http status code should then be included in the response body. This
can be useful when some proxies only allow 200 status codes through or for
debugging reasons.</p>

<p></p>

<h2><a>Versioning</a></h2>

<p>There is some debate on how to version APIs or whether
versioning should be included at all. Versioning an API breaks the HATEOAS
constraint of REST but pragmatic REST APIs that don’t adhere to this constraint
might still need to version. If the API needs to be versioned, the two most
popular ways this can be achieved is to include it as a custom request header
or include it as part of the URL. The most visible method and easiest to work
with is to keep it in the URL, for example /v1/users. Some standards should be
used.</p>

<h3>Include the letter v</h3>

<p>Including the letter v in your version name automatically
indicates that part of the URL path specifies the version.</p>

<h3>Keep to whole version numbers</h3>

<p>Even though there will be numerous internal build numbers
for bug fixes and enhancements, APIs should not change version very often. Keeping
the version to whole numbers like v1 or v2 forces the API to rarely release a
new version and limits the number of legacy API versions that need to be
maintained.</p>

<p></p>

<h2><a>Security and Authorization</a></h2>

<p>A full discussion on this topic is outside the scope of this
document but I will cover the basic best practices. </p>

<h3>HTTPS on all requests to the API</h3>

<p>HTTPS means using HTTP over the SSL/TLS protocol. The
purpose of HTTPS is to prevent man-in-the-middle and wiretapping attacks. Using
this is especially important if the API is using HTTP basic authentication.</p>

<h3>OAuth 2</h3>

<p>This provides authentication through third parties such as
facebook or twitter. This will require an extra library but the major benefit
is outsourcing your full authorization to these secure third parties. OAuth 2
also allows custom authorization, on the initial login request, the server
returns a JSON Web Token that is stored on the client. Each subsequent request
sends this JWT as Bearer token in the Authorization request header field.</p>

<p></p>

<h2><a>Session state</a> </h2>

<p>The server should not store any state of the current
session.<span>  </span>This means every request sent
from the client to the server should include all information necessary to
fulfil that request. Session state is managed solely by the client.</p>

<p>The session can be stored on the client in many forms, such
as cookies or tokens.</p>

<p></p>

<h2><a>HATEOAS</a> </h2>

<p>Think of it as state are webpages and transitions are
hyperlinks. It boils down to including links in each response message for the
next request message. This way the server drives the app state, not the client.
For example, a GET on /users/1234 will include links in the response for other
appropriate actions to take next, such as PUT /users/1234 or DELETE
/users/1234.</p>

<h3>HAL (Hypertext Application Language)</h3>

<p>HAL provides a set of conventions for expressing hyperlinks
in either JSON or XML. This is one of the most common formats for implementing
HATEOAS. The media type for HAL is application/hal+json. HAL responses include
a link to the resource just retrieved and other associated resources and it
specifies how to embed links in nested data. More can be read here <a
href="http://stateless.co/hal_specification.html">http://stateless.co/hal_specification.html</a>.
Here is an example to show the structure of a response.</p>


<h1><a>REST API Grading: Richardson Maturity Model</a> </h1>


<p>The Richardson Maturity Model outlined by Leonard Richardson
is a way to grade your API based on four levels. It breaks down the main
elements of REST into three steps. </p>

<p class=MsoCaption>(Image credit: Martin Fowler)</p>

<p>The model has simplified the REST constraints but is a good
basic way to grade your web REST API. The levels are to be taken as building
blocks, to reach the next level the previous level has to be met. Reaching
level 1 of the RMM is common with REST APIs trying to represent CRUD-driven
objects as resources. When level 3 is reached, the API is truly RESTful.</p>

<h2><a>Level 0: The swamp of POX (plain old XML)</a></h2>

<p>The API uses HTTP as the transport protocol. It doesn’t use
HTTP to indicate application state as it will use one method which is usually POST
for most URIs. No resources are clearly defined and all requests are sent to a
single endpoint. Examples of this level are SOAP and XML-RPC</p>

<h2><a>Level 1: Resources</a></h2>

<p>Level 1 is when your API can distinguish between different
resources. Requests are sent to individual resource URIs. However, a single
method like POST is still used.</p>

<h2><a>Level 2: HTTP Verbs</a></h2>

<p>So far, the previous levels have mostly used a single HTTP
method like POST. This level starts using HTTP methods as they are used in HTTP
itself. GET, POST, PUT and DELETE are used for various resources.</p>

<h2><a>Level 3: Hypermedia Controls</a></h2>

<p>The last level is when HATEOAS is implemented in your API.
According to the Richard Maturity Model, APIs that reach this level are
considered RESTful.</p>
