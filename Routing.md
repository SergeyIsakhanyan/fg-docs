# Routing

Routing is the ability to move between different parts of an application when a user enters a URL or clicks an element (link, button, icon, image etc) 
within the application. Originally web applications consisted in interconnected `html documents` that one could navigate through links between them. There is two 
types of routing in `JS`:

- server-side routing
- client-side routing

### server-side routing
Every time a user clicked a link on a website a new document would be generated in the server and sent back to the browser to be rendered in their screen.

### client-side routing
For achieving `client-side rendering` we need to create app/website as `SPA(Single-Page Application)`. SPA's are based on a single document model. 
This means that web applications’ lifespan happens on a single html page, along with the transitions between the different views.

#### How it works
A Javascript router is a piece of software in charge to organize the states of the application, switching between different views.
The router will be in charge of simulating transitions between documents by watching changes on the URL. 
When the document is reloaded or the URL is modified somehow, it will detect that change and render the view that is associated with the new URL.
