## HATEOS
It stands for Hypermedia as the Engine of Application State (HATEOAS).
It is the way to provide links to the resources in the API response so that
client doesn't have to deal with URI constuction and the business flow.
Client just makes a request and further required URIs are handed over to them.

As per wiki is a constraint of the REST application architecture that distinguishes
it from other network application architectures.

You visit websites frequently, and you do not need any kind of documentation right?
We just go to the home page and when you go to the home page you find links to other pages.
We do not need any documentation for now next where to go. You just remember the website home address 
and that's it any other links need to navigate the site will be provided to you in the response.

This is the advantage of using HTTP(Hypertext Transfer Protocol). Hypertext - which has a link to other text,
these links are called as hyperlinks. These hyperlinks helps you to navigate from one page to other.

Let's see REST API , what if we use the same (hyperlink) concept here.
For e.g. GET messages/1 (here 1 is messageId) we get the response as :
```
{
    "id" : "1",
    "message" : "Hey Kirti!",
    "date" : "2021-05-08",
    "author" : "Thomas"
}
```
What if you could also send links to the comments' resource URI
```
{
    "id" : "1",
    "message" : "Hello Kirti!",
    "date" : "2021-05-08",
    "author" : "Thomas",
    "commentsUri" : "/messages/1/comments",
    "likesUri" : "/messages/1/likes",
    "sharesUri" : "/messages/1/shares"
}
```
It means that along with asked message resource info, server is sending the collection URI for the comments, shares and likes.
It is similar to hyperlink websites. Whether client wants to use or not doesn't matter. But if client wants it's there.
It achieves the loose coupling. (Client doesn't need to know beforehand what id is to construct futher URIs like comments, shares)

This way client no need to hardcode the URIs to interact with the resources, and the application state.
i.e. hypertext/ hypermedia sent in the response is driving the clients' interaction with the application state
and so the name  hypertext/ hypermedia being driver/ engine of the application state

Now look at the above example , the client does not need remember URIs but now it has to remember property values and so property name
and basically the same issue. There needs to be a better way to manage these links.
And so for that we can use 'rel' attribute (similar to in a html which specifies relationship between current and the link document)

So here is modified response can look like
```
{
    "id" : "1",
    "message" : "Hello Kirti!",
    "date" : "2021-05-08",
    "author" : "Thomas",
    "links": [
        { 
            "href" : "/messages/1",
            "rel"  : "self"
        },
        { 
            "href" : "/messages/1/comments",
            "rel"  : "comments"
        },
        { 
            "href" : "/messages/1/likes",
            "rel"  : "likes"
        },
        { 
            "href" : "/messages/1/shares",
            "rel"  : "shares"
        }
    ]
}
```
Way to send URIs in response can differ. The above is one of the JSON forms.
The rel attribute is part of HTTP specification. Only standard values are allowed for it. You can refer this [link](https://www.iana.org/assignments/link-relations/link-relations.xml).

### Reference
 1. [wiki](https://en.wikipedia.org/wiki/HATEOAS)
 2. [Java Brains](https://www.youtube.com/watch?v=NK3HNEwDXUk&ab_channel=JavaBrains)
