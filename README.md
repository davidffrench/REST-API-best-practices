# <a name="_Toc404943963">Introduction</a>

Representational State Transfer (REST) is an architectural
style defined by Roy Fielding in 2000 in his PhD dissertation. REST describes a
web architecture that is not specific to web APIs. However, it has become the
most popular style of web API, overtaking SOAP in 2008. REST APIs are simple to
use, scalable, portable and easy to integrate with. The aim of this paper is to
look at what constraints are involved in creating a RESTful API and what the
best practices are for web REST APIs.

# <a name="_Toc404943964">REST Constraints</a>

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Client-Server

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Stateless

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Cache

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Uniform interface

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Layered System

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Code-On-Demand (optional)

## <a name="_Toc404943965">Client-Server</a>

The Client-Server constraint is focused on separation of
concerns. By separating the front end UI from the back end data storage
concerns, portability and scalability are improved. This also allows the
separate components to evolve independently.

## <o:p>&nbsp;</o:p>

## <a name="_Toc404943966">Stateless</a>

The server should not store any state of the current
session.<span style='mso-spacerun:yes'>  </span>This means every request sent
from the client to the server should include all information necessary to
fulfil that request. Session state is managed solely by the client. 

The pros of this constraint are visibility, reliability and
scalability. Visibility is improved because the server only has to deal with
one request and the information that was sent with it. Reliability and
scalability are improved because the server is not storing any session
information so session information does not have to be copied across multiple
server instances in case of a server failure and this allows for easy
scalability for the same reason. 

The con is that common information will have to get sent
with each request (e.g. user authentication information) which will decrease
network performance. Having the client store all session state reduces the
servers control with consistent application behaviour because of multiple
client versions

## <span style='font-size:11.0pt;line-height:115%;font-family:"Calibri","sans-serif";
mso-ascii-theme-font:minor-latin;mso-fareast-font-family:Calibri;mso-fareast-theme-font:
minor-latin;mso-hansi-theme-font:minor-latin;mso-bidi-font-family:"Times New Roman";
mso-bidi-theme-font:minor-bidi;color:windowtext;font-weight:normal'><o:p>&nbsp;</o:p></span>

## <a name="_Toc404943967">Cache</a>

The cache constraint is to improve network efficiency and
hence improve user-perceived performance. Each request can either be cacheable
or non-cacheable. If a response is cacheable, the client can use the cached
response for the same request later on. 

The major benefit of caching is performance. Allowing
certain responses to be cacheable allows for fewer requests to the server and
much faster retrieval of cached data for the client.

The disadvantage is if cached data differs from data that
would have been sent back if the request had reached the server. This needs to
be maintained by having a time limit on the how long the response should be
cached for.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943968">Uniform Interface</a>

This constraint is what distinguishes REST from other
network-based architectural styles. The constraint states that all services and
service consumers must share a single, overarching technical interface. The
uniform interface is generally applied using methods and media types provided
by HTTP. This constraint will be the main area of focus for best practices because
the API design is how other developers will see the API and interact with it. Four
sub constraints are defined to achieve the uniform interface constraint, these
are

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Identification of resources

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Manipulation of resources through
representations

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Self-descriptive messages

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>Hypermedia as the engine of application state
(HATEOAS)

### Identification of resources

Fielding defines a resource as “Any information that can be
named: a document or image, a temporal service (e.g. &quot;today's weather in
Los Angeles&quot;), a collection of other resources, a non-virtual object (e.g.
a person)”. In web based REST APIs, resources are identified using URIs. The
resources are conceptually separate from the representation returned to the
client. The server sends a representation of a resource using HTML, XML, JSON
or other formats.

### Manipulation of resources through representations

The representation of the resource that the client stores
should have all the information necessary to manipulate the resource itself
through the API (modify or delete).

### Self-descriptive messages

The message response from the API should include the
information necessary to tell the client how to process the message. With web
REST APIs, this is done using internet media types. In the response header, the
Content-type field will have a value describing the message body format e.g. application/json.
Responses should also outline the cache criteria.

### Hypermedia as the engine of application state (HATEOAS)

One initial base resource should be the entry point to the
API. Clients should then receive applicable actions from the server. Hypermedia
in web REST APIs are hyperlinks within hypertext. For example, if the client
retrieves a resource representation, the response should include other applicable
actions that can be taken on that resource like modifying or delete with the
URI hyperlink for each.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943969">Layered System</a>

The layered system builds on top of the Client-Server
architecture and describes a system that is made up of multiple architectural
layers. The constraint outlines that each layer should only know about the
immediate layer it is interacting with. 

By restricting the knowledge of what other layers a layer
knows about, this decreases complexity and allows for easier scalability by allowing
load balancing of services. Also, additional middleware will be easier to
integrate.

The main disadvantage is increased overhead and latency.
This can be mitigated with the cache constraint, allowing cached content at the
boundaries of the separate layers where applicable.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943970">Code-On-Demand (optional)</a>

This constraint allows client functionality to be extended
by the server sending executable code in the form of applets or scripts. This
means that additional modules can be executed on the client when necessary or
needed. 

This constraint is optional so it can be excluded without
violating the principles of REST.

# <o:p>&nbsp;</o:p>

# <a name="_Toc404943971">RESTful Web API Best Practices</a>

## <a name="_Toc404943972">URL structure</a>

The base URL is the entry point of the API. The path after
the base should identify a resource or collection of resources. The query
parameter is appended to the end of the resource path.

<span
style='font-size:10.0pt;font-family:"Courier New";mso-fareast-font-family:"Times New Roman";
mso-fareast-language:EN-GB'>http://example.com/users/1234/activities?activityType=running<o:p></o:p></span>

<span
style='font-size:10.0pt;font-family:"Courier New";mso-fareast-font-family:"Times New Roman";
mso-fareast-language:EN-GB'>\<u><span style='mso-spacerun:yes'>               
</span></u>/\<u><span style='mso-spacerun:yes'>         </span><span
style='mso-spacerun:yes'>           </span></u>/\<u><span
style='mso-spacerun:yes'>          </span><span
style='mso-spacerun:yes'>         </span></u>/<o:p></o:p></span>

<span
style='mso-tab-count:1'>                </span><span
style='mso-spacerun:yes'>     </span>l<span
style='mso-spacerun:yes'>                                                
</span>l<span
style='mso-spacerun:yes'>                                                   
</span>l

Base URL<span style='mso-tab-count:
2'>                             </span><span style='mso-spacerun:yes'>   
</span>Resource<span style='mso-tab-count:2'>                         </span><span
style='mso-spacerun:yes'>    </span>Query Parameter

In the above example, the resource should be viewed in a
hierarchical way. ‘/Users’ is a top level collection. ‘/1234’ is the id that
identifies a unique user. ‘/activities’ is a collection of activity resources
specific to the user 1234.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943973">Resource Naming</a>

The URIs that identify resources are arguably the most important
to get right because they are the most visible part of the API. <span
style='mso-spacerun:yes'> </span>

### Only 2 URIs per resource

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>/users

<![if !supportLists]><span
style='font-family:Symbol;mso-fareast-font-family:Symbol;mso-bidi-font-family:
Symbol'><span style='mso-list:Ignore'>·<span style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><![endif]>/users/1234

The first is a collection of resources, the second is a
specific resource in the collection. In this case, all users and a specific
user.

### Nouns, not verbs

Keep verbs out of the resource name. The HTTP method is what
describes the action for the request. Resource names should be nouns but plural
nouns are preferable. Readability is paramount with a consistent pattern. With
the verb approach, different developers will come up with vastly different
naming schemes and they are not easy to learn. Using nouns, the API is easier
to understand and read. Plural nouns are always preferred to keep consistency
and understanding. The /users collection compared /user tells the reader that
it identifies all users, not just one. 

**Examples with verbs -
Bad<o:p></o:p>**

/getUsers

/createUser

/saveUser

/getUserActivities

/updateUserActivity

/deleteActivities

/deleteUserActivity

<o:p>&nbsp;</o:p>

**Examples with nouns –
Good<o:p></o:p>**

The HTTP methods on the right are what would be used as an equivalent
to the bad URIs.

/users<span
style='mso-tab-count:4'>                                                   </span>GET(getUsers),
POST(createUser)

/users/1234<span
style='mso-tab-count:3'>                                        </span>PUT(saveUser)

/users/1234/activities<span
style='mso-tab-count:2'>                    </span>GET(getUserActivities),
DELETE(deleteActivities)

/users/1234/activities/4321<span
style='mso-tab-count:1'>         </span>PUT(updateUserActivity),
DELETE(deleteUserActivity)

<o:p>&nbsp;</o:p>

### Lower case

Consistency is key with casing. Lower case is easier to type
in and no confusion can occur when trying to remember the casing. Mixed case
might also cause ambiguity.

### Keep It Intuitive

URIs should be human-guessable, meaningful and predictable.
The name should tell the user what they are looking at.
‘/users/1234/activities’ should give a hint that the URI identifies the
activities collection for user 1234. When URIs are meaningful like this, a user
should be able to predict or guess other URIs if they know some of the API.

### Hackable

The hierarchy of resources should allow the user to remove the
leaf path and access the parent resource. By removing the ‘activities’ leaf
path from the example URIs above, we are left with ‘/users/1234’ which we would
expect identifies a unique user. Again, by removing the remaining leaf path
‘1234’, we expect ‘/users’ identifies a collection of users. Lower case names

<o:p>&nbsp;</o:p>

## <a name="_Toc404943974">When/what to use query parameters for</a> 

URI query parameters are used for filtering, searching, sorting
and pagination.

### Filtering or searching

Send a unique value for the field(s) to be filtered/searched,
for example <span style='background:#D6E3BC;mso-shading-themecolor:accent3;
mso-shading-themetint:102'>/users?firstname=david&amp;age=24</span>. Each
additional field should be preceded with an ‘&amp;’. This will return the users
that only have a name of ‘david’ and an age of 24. 

### Sorting

Sorting needs two criteria, the field to sort and the
direction of the sort. The direction should be ASC (ascending) or DESC (descending).
For example <span style='background:#D6E3BC;mso-shading-themecolor:accent3;
mso-shading-themetint:102'>/users?sort=email&amp;dir=DESC</span>.

### Pagination

Pagination also requires two parameters. The item to start on
(start) and how many items to return (limit). For example <span
style='background:#D6E3BC;mso-shading-themecolor:accent3;mso-shading-themetint:
102'>/users?start=60&amp;limit=20</span> will return the items from 60-79.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943975">HTTP Methods</a> 

<table class=MsoTableLightListAccent3 border=1 cellspacing=0 cellpadding=0
 style='border-collapse:collapse;border:none;mso-border-alt:solid #9BBB59 1.0pt;
 mso-border-themecolor:accent3;mso-yfti-tbllook:1184;mso-padding-alt:0cm 5.4pt 0cm 5.4pt;
 mso-border-insideh:1.0pt solid #9BBB59;mso-border-insideh-themecolor:accent3;
 mso-border-insidev:1.0pt solid #9BBB59;mso-border-insidev-themecolor:accent3'>
 <tr style='mso-yfti-irow:-1;mso-yfti-firstrow:yes'>
  <td width=123 style='width:92.4pt;border:solid #9BBB59 1.0pt;mso-border-themecolor:
  accent3;background:#9BBB59;mso-background-themecolor:accent3;padding:0cm 5.4pt 0cm 5.4pt'>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

**<span
  style='color:white;mso-themecolor:background1'>Resource<o:p></o:p></span>**

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

  </td>
  <td width=123 valign=top style='width:92.4pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-left:none;mso-border-left-alt:solid #9BBB59 1.0pt;
  mso-border-left-themecolor:accent3;background:#9BBB59;mso-background-themecolor:
  accent3;padding:0cm 5.4pt 0cm 5.4pt'>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

**<span
  style='color:white;mso-themecolor:background1'>POST<o:p></o:p></span>**

<span style='color:
  white;mso-themecolor:background1;mso-bidi-font-weight:bold'>create<o:p></o:p></span>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

  </td>
  <td width=123 valign=top style='width:92.4pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-left:none;mso-border-left-alt:solid #9BBB59 1.0pt;
  mso-border-left-themecolor:accent3;background:#9BBB59;mso-background-themecolor:
  accent3;padding:0cm 5.4pt 0cm 5.4pt'>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

**<span
  style='color:white;mso-themecolor:background1'>GET<o:p></o:p></span>**

<span style='color:
  white;mso-themecolor:background1;mso-bidi-font-weight:bold'>read<o:p></o:p></span>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

  </td>
  <td width=123 valign=top style='width:92.45pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-left:none;mso-border-left-alt:solid #9BBB59 1.0pt;
  mso-border-left-themecolor:accent3;background:#9BBB59;mso-background-themecolor:
  accent3;padding:0cm 5.4pt 0cm 5.4pt'>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

**<span
  style='color:white;mso-themecolor:background1'>PUT<o:p></o:p></span>**

<span style='color:
  white;mso-themecolor:background1;mso-bidi-font-weight:bold'>update<o:p></o:p></span>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

  </td>
  <td width=123 valign=top style='width:92.45pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-left:none;mso-border-left-alt:solid #9BBB59 1.0pt;
  mso-border-left-themecolor:accent3;background:#9BBB59;mso-background-themecolor:
  accent3;padding:0cm 5.4pt 0cm 5.4pt'>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

**<span
  style='color:white;mso-themecolor:background1'>DELETE<o:p></o:p></span>**

<span style='color:
  white;mso-themecolor:background1;mso-bidi-font-weight:bold'>delete<o:p></o:p></span>

**<span
  style='color:white;mso-themecolor:background1'><o:p>&nbsp;</o:p></span>**

  </td>
 </tr>
 <tr style='mso-yfti-irow:0'>
  <td width=123 valign=top style='width:92.4pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-top:none;mso-border-top-alt:solid #9BBB59 1.0pt;
  mso-border-top-themecolor:accent3;background:#D6E3BC;mso-background-themecolor:
  accent3;mso-background-themetint:102;padding:0cm 5.4pt 0cm 5.4pt'>

**<o:p>&nbsp;</o:p>**

**/users<o:p></o:p>**

**<o:p>&nbsp;</o:p>**

  </td>
  <td width=123 style='width:92.4pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>

Create a new user

  </td>
  <td width=123 style='width:92.4pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>

List users

  </td>
  <td width=123 style='width:92.45pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>

Bulk update users

or error

  </td>
  <td width=123 style='width:92.45pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>

Delete all users 

or error

  </td>
 </tr>
 <tr style='mso-yfti-irow:1;mso-yfti-lastrow:yes'>
  <td width=123 valign=top style='width:92.4pt;border:solid #9BBB59 1.0pt;
  mso-border-themecolor:accent3;border-top:none;mso-border-top-alt:solid #9BBB59 1.0pt;
  mso-border-top-themecolor:accent3;background:#D6E3BC;mso-background-themecolor:
  accent3;mso-background-themetint:102;padding:0cm 5.4pt 0cm 5.4pt'>

**<o:p>&nbsp;</o:p>**

**/users/1234<o:p></o:p>**

**<o:p>&nbsp;</o:p>**

  </td>
  <td width=123 style='width:92.4pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>

error

  </td>
  <td width=123 style='width:92.4pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>

List unique user

  </td>
  <td width=123 style='width:92.45pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>

Update user

  </td>
  <td width=123 style='width:92.45pt;border-top:none;border-left:none;
  border-bottom:solid #9BBB59 1.0pt;mso-border-bottom-themecolor:accent3;
  border-right:solid #9BBB59 1.0pt;mso-border-right-themecolor:accent3;
  mso-border-top-alt:solid #9BBB59 1.0pt;mso-border-top-themecolor:accent3;
  mso-border-left-alt:solid #9BBB59 1.0pt;mso-border-left-themecolor:accent3;
  padding:0cm 5.4pt 0cm 5.4pt'>

Delete user

  </td>
 </tr>
</table>

<o:p>&nbsp;</o:p>

The four HTTP methods map to CRUD. Create = POST, Read =
GET, Update = PUT and Delete = DELETE. The HTTP method determines what action
is performed on the resource. Web REST APIs use the HTTP protocol for requests/responses,
HTTP outlines a set of methods that can be used for requests and the four above
are the main ones used in REST APIs. In the above example, most APIs would not
allow a PUT or DELETE on a collection (/users) as this could be dangerous.

GET, PUT and DELETE are idempotent but POST is not. This
means, no matter how many times the idempotent request methods are sent, the
outcome will always be the same. With POST, a new resource will be created
every time.<span style='mso-spacerun:yes'>  </span>

<o:p>&nbsp;</o:p>

## <a name="_Toc404943976">What to include in HTTP headers</a> 

HTTP headers should include metadata for the request and
response. This includes the body format, caching and authorisation fields. Below
are three examples of common header fields:

**Content-Type:** The
format type of the request or response body. Used with POST and PUT. Example: <span
style='background:#D6E3BC;mso-shading-themecolor:accent3;mso-shading-themetint:
102'>Content-Type: application/json.</span>

**Accept:** Request
only - Lists Content-Types acceptable for the response. Example: <span
style='background:#D6E3BC;mso-shading-themecolor:accent3;mso-shading-themetint:
102'>Accept: text/plain; application/json.</span>

**Allow:** Response
only - Valid methods for the resource, if an invalid method was used.

## <a name="_Toc404943977">Caching</a>

The browser has a built in caching framework which can be
leveraged using cache specific HTTP headers in the response, these are <span
style='color:#76923C;mso-themecolor:accent3;mso-themeshade:191'>Cache-Control </span>and
<span style='color:#76923C;mso-themecolor:accent3;mso-themeshade:191'>Etag.<o:p></o:p></span>

**<span
style='color:#76923C;mso-themecolor:accent3;mso-themeshade:191'>Cache-Control:</span>**<span
style='color:#76923C;mso-themecolor:accent3;mso-themeshade:191'> </span>This
specifies how long the response should be cached for in seconds.<span
style='mso-spacerun:yes'>  </span>Example: <span style='background:#D6E3BC;
mso-shading-themecolor:accent3;mso-shading-themetint:102'>Cache-Control:<span
style='mso-spacerun:yes'>  </span></span>`<span style='font-size:10.0pt;
line-height:115%;mso-fareast-font-family:Calibri;mso-fareast-theme-font:minor-latin;
background:#D6E3BC;mso-shading-themecolor:accent3;mso-shading-themetint:102'>max-age=3600.<o:p></o:p></span>`

**<span
style='color:#76923C;mso-themecolor:accent3;mso-themeshade:191'>Etag:</span>**
A unique identifier for a specific version of a resource. Example: <span
style='background:#D6E3BC;mso-shading-themecolor:accent3;mso-shading-themetint:
102'>ETag: “x234dff”.</span>

When the cached response times out and another request is
made for the same resource, the browser will send the ETag token as a value of
a request header called <span style='color:#76923C;mso-themecolor:accent3;
mso-themeshade:191'>If-None-Match. </span>The server should check this token
against the current resource version and send back a response with a status
code of ‘304 Not modified’ if they match. The cache time-out will get then get
reset.

**<span
style='color:#76923C;mso-themecolor:accent3;mso-themeshade:191'>If-None-Match:</span>**<span
style='color:#76923C;mso-themecolor:accent3;mso-themeshade:191'> </span>Etag
token sent in new request. If the resource hasn’t changed, the response is ‘304
Not Modified’ and the cache time out is reset.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943978">Error handling</a>

### Standard HTTP status codes for error responses.<span
style='mso-spacerun:yes'>  </span>

HTTP status codes starting with 4xx are client errors and
5xx are server errors. Here are some examples of common error response status
codes.

<span style='mso-tab-count:1'>                </span>**400 Bad Request:** Malformed request
syntax

<span style='mso-tab-count:1'>                </span>**401 Unauthorized:** Authentication is
required or has failed

<span style='mso-tab-count:1'>                </span>**404 Not Found:** Requested resource could
not be found

<span style='mso-tab-count:1'>                </span>**405 Method Not Allowed:** HTTP method
used is not allowed on the resource

### Detailed error description 

The error message in the response should explain the problem
in human readable format. Let it be verbose, you shouldn’t be trying to save
bandwidth on errors. 

### Internal error code

Include the internal error code so it can be looked up for
more information. To go one step further, include a URL link in the response to
the specific internal error in your documentation.

### Extra: Allow HTTP status code override

Allow a URL query parameter on all requests that will always
return a HTTP status code of 200. Twitter’s query param to allow this is ‘suppress_response_codes=true’.
The original http status code should then be included in the response body. This
can be useful when some proxies only allow 200 status codes through or for
debugging reasons.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943979">Versioning</a>

There is some debate on how to version APIs or whether
versioning should be included at all. Versioning an API breaks the HATEOAS
constraint of REST but pragmatic REST APIs that don’t adhere to this constraint
might still need to version. If the API needs to be versioned, the two most
popular ways this can be achieved is to include it as a custom request header
or include it as part of the URL. The most visible method and easiest to work
with is to keep it in the URL, for example /v1/users. Some standards should be
used.

### Include the letter v

Including the letter v in your version name automatically
indicates that part of the URL path specifies the version.

### Keep to whole version numbers

Even though there will be numerous internal build numbers
for bug fixes and enhancements, APIs should not change version very often. Keeping
the version to whole numbers like v1 or v2 forces the API to rarely release a
new version and limits the number of legacy API versions that need to be
maintained.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943980">Security and Authorization</a>

A full discussion on this topic is outside the scope of this
document but I will cover the basic best practices. 

### HTTPS on all requests to the API

HTTPS means using HTTP over the SSL/TLS protocol. The
purpose of HTTPS is to prevent man-in-the-middle and wiretapping attacks. Using
this is especially important if the API is using HTTP basic authentication.

### OAuth 2

This provides authentication through third parties such as
facebook or twitter. This will require an extra library but the major benefit
is outsourcing your full authorization to these secure third parties. OAuth 2
also allows custom authorization, on the initial login request, the server
returns a JSON Web Token that is stored on the client. Each subsequent request
sends this JWT as Bearer token in the Authorization request header field.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943981">Session state</a> 

The server should not store any state of the current
session.<span style='mso-spacerun:yes'>  </span>This means every request sent
from the client to the server should include all information necessary to
fulfil that request. Session state is managed solely by the client.

The session can be stored on the client in many forms, such
as cookies or tokens.

<o:p>&nbsp;</o:p>

## <a name="_Toc404943982">HATEOAS</a> 

Think of it as state are webpages and transitions are
hyperlinks. It boils down to including links in each response message for the
next request message. This way the server drives the app state, not the client.
For example, a GET on /users/1234 will include links in the response for other
appropriate actions to take next, such as PUT /users/1234 or DELETE
/users/1234.

### HAL (Hypertext Application Language)

HAL provides a set of conventions for expressing hyperlinks
in either JSON or XML. This is one of the most common formats for implementing
HATEOAS. The media type for HAL is application/hal+json. HAL responses include
a link to the resource just retrieved and other associated resources and it
specifies how to embed links in nested data. More can be read here [http://stateless.co/hal_specification.html](http://stateless.co/hal_specification.html).
Here is an example to show the structure of a response.

<span
style='font-size:10.0pt;font-family:"Courier New";mso-fareast-font-family:"Times New Roman";
mso-fareast-language:EN-GB'><!--[if gte vml 1]><v:shapetype id="_x0000_t75"
 coordsize="21600,21600" o:spt="75" o:preferrelative="t" path="m@4@5l@4@11@9@11@9@5xe"
 filled="f" stroked="f">
 <v:stroke joinstyle="miter"/>
 <v:formulas>
  <v:f eqn="if lineDrawn pixelLineWidth 0"/>
  <v:f eqn="sum @0 1 0"/>
  <v:f eqn="sum 0 0 @1"/>
  <v:f eqn="prod @2 1 2"/>
  <v:f eqn="prod @3 21600 pixelWidth"/>
  <v:f eqn="prod @3 21600 pixelHeight"/>
  <v:f eqn="sum @0 0 1"/>
  <v:f eqn="prod @6 1 2"/>
  <v:f eqn="prod @7 21600 pixelWidth"/>
  <v:f eqn="sum @8 21600 0"/>
  <v:f eqn="prod @7 21600 pixelHeight"/>
  <v:f eqn="sum @10 21600 0"/>
 </v:formulas>
 <v:path o:extrusionok="f" gradientshapeok="t" o:connecttype="rect"/>
 <o:lock v:ext="edit" aspectratio="t"/>
</v:shapetype><v:shape id="_x0000_i1025" type="#_x0000_t75" style='width:451.5pt;
 height:138.75pt' o:ole="">
 <v:imagedata src="David%20Ffrench%20-%20Research%20Assignment(REST%20Constraints,%20Best%20Practices%20and%20Grading%20your%20API)_files/image001.emz"
  o:title=""/>
</v:shape><![endif]--><![if !vml]>![](David%20Ffrench%20-%20Research%20Assignment(REST%20Constraints,%20Best%20Practices%20and%20Grading%20your%20API)_files/image002.png)<![endif]><!--[if gte mso 9]><xml>
 <o:OLEObject Type="Embed" ProgID="Word.OpenDocumentText.12"
  ShapeID="_x0000_i1025" DrawAspect="Content" ObjectID="_1480426511">
 </o:OLEObject>
</xml><![endif]--><o:p></o:p></span>

<span
style='font-size:10.0pt;font-family:"Courier New";mso-fareast-font-family:"Times New Roman";
mso-fareast-language:EN-GB'><o:p>&nbsp;</o:p></span>

<a
name="_Toc404943983"><span class=Heading1Char><span style='font-size:14.0pt'>REST
API Grading: Richardson Maturity Model</span></span></a><span style='mso-bookmark:
_Toc404943983'></span><span style='font-size:10.0pt;font-family:"Courier New";
mso-fareast-font-family:"Times New Roman";mso-fareast-language:EN-GB'><o:p></o:p></span>

The Richardson Maturity Model outlined by Leonard Richardson
is a way to grade your API based on four levels. It breaks down the main
elements of REST into three steps. 

<span style='mso-fareast-language:
EN-GB;mso-no-proof:yes'><!--[if gte vml 1]><v:shape id="Picture_x0020_1"
 o:spid="_x0000_i1030" type="#_x0000_t75" style='width:451.5pt;height:267pt;
 visibility:visible;mso-wrap-style:square'>
 <v:imagedata src="David%20Ffrench%20-%20Research%20Assignment(REST%20Constraints,%20Best%20Practices%20and%20Grading%20your%20API)_files/image003.jpg"
  o:title=""/>
</v:shape><![endif]--><![if !vml]>![](David%20Ffrench%20-%20Research%20Assignment(REST%20Constraints,%20Best%20Practices%20and%20Grading%20your%20API)_files/image004.jpg)<![endif]></span>

(Image credit: Martin Fowler)

The model has simplified the REST constraints but is a good
basic way to grade your web REST API. The levels are to be taken as building
blocks, to reach the next level the previous level has to be met. Reaching
level 1 of the RMM is common with REST APIs trying to represent CRUD-driven
objects as resources. When level 3 is reached, the API is truly RESTful.

## <a name="_Toc404943984">Level 0: The swamp of POX (plain old XML)</a>

The API uses HTTP as the transport protocol. It doesn’t use
HTTP to indicate application state as it will use one method which is usually POST
for most URIs. No resources are clearly defined and all requests are sent to a
single endpoint. Examples of this level are SOAP and XML-RPC

## <a name="_Toc404943985">Level 1: Resources</a>

Level 1 is when your API can distinguish between different
resources. Requests are sent to individual resource URIs. However, a single
method like POST is still used.

## <a name="_Toc404943986">Level 2: HTTP Verbs</a>

So far, the previous levels have mostly used a single HTTP
method like POST. This level starts using HTTP methods as they are used in HTTP
itself. GET, POST, PUT and DELETE are used for various resources.

## <a name="_Toc404943987">Level 3: Hypermedia Controls</a>

The last level is when HATEOAS is implemented in your API.
According to the Richard Maturity Model, APIs that reach this level are
considered RESTful.
