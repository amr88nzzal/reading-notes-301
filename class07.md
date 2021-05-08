
#### HTTP
- is capable of all sorts of neat stuff 
- tells the browser what protocol to use
- is one of the most important breakthroughs in the history of computing
- it is capable of describing the location of something anywhere in the world from anywhere in the world. 
- It's the foundation of the web. 
- think of it like GPS coordinates for knowledge and information.

#### REST
- The whole world wide web is built on an architectural style called “REST”. 
- REST provides a definition of a “resource”, which is what it points to.
  - A web page is a “representation” of a resource. Resources are just concepts. URLs--those things that you type into the browser
  - representations don't get used a lot. 
    - In most cases, a resource has only a single representation. 
    - But we're hoping that representations will be used more in the future because there's a bunch of new formats popping up all over the place.
- URLs tell the browser that there's a concept somewhere. 
  - A browser can then go ask for a specific representation of the concept. 
  - Specifically, the browser asks for the web page representation of the concept.

#### “Web Services” or "APIs"
- the basic concept is that machines could use the web just like people do
- computers can use those same protocols to send messages back and forth to each other. 
- We've been doing that for a long time but none of the techniques we use today work well when you need to be able to talk to all of the machines in the entire world.
- We need to be able to talk to all machines about all the stuff that's on all the other machines. 
  - So we need some way of having one machine tell another machine about a resource that might be on yet another machine.
- a "redirect" is when you tell the server to go get the data from a different place


> When Fielding and his buddies started building the web, being able to talk to any machine anywhere in the world was a primary concern. Most of the techniques we use at work to get computers to talk to each other didn't have those requirements. You just needed to talk to a small group of machines.

#### How do the machines tell each other where things are?
- The URL
  - If everything that machines need to talk about has a corresponding URL, you've created the machine equivalent of a noun. 
  - Machines don't have a universal noun - that's why they suck. 
  - Every programming language, database, or other kind of system has a different way of talking about nouns. 
  - That's why the URL is so important. It let's all of these systems tell each other about each other's nouns

#### Polymorphism
  - a powerful concept in programming and CS theory that is equalvalent to different how nouns can have the same verb applied to them.
  -  Each system would retrieve information from others using a simple HTTP GET. 
  - If one system needs to add something to another, it would use an HTTP POST. 
  - If a system wants to replace something in another, it uses an HTTP PUT, or, to do a partial update, it'll hopefully use PATCH. 

#### GET
- when you go to a web page, the browser does an HTTP GET on the URL you type in and back comes a web page.
- Whether the noun is an image, text, video, an mp3, a slideshow, whatever. I can GET all of those things the same way given a URL.
- Especially when you're using a web browser because browsers pretty much just GET stuff. 
- They don't do a lot of other types of interaction with resources. 
- This is a problem because it has led many people to assume that HTTP is just for GETing. 
- But HTTP is actually a general purpose protocol for applying verbs to nouns.
