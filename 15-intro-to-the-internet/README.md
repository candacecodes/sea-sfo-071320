# Intro to the Internet

## Outline

- History of the Internet
- How the Web Works
- What Happens When I Press Enter or Click on A Link
- The Request/Response Cycle
- Making Requests from Postman

## History of the Internet

The internet is a network of computers all connected by cables. Most often, it's a network of smaller networks together. Think home networks, school networks, business networks, and government networks. It's commonly cited that the internet was developed by the military through DARPA (Department of Defense Advanced Research Projects Agency) and was first connected in October 1969. It really was the result of a few different types of technologies that came together to make the technology of the internet possible.

These networks are connected through literal cables, and the reason that we can get information from one continent to another is through underwater fiber optic cables. These cables are thick (for a cable) and branch of at different points until they eventually reach your wall where you likely have a wifi router installed.

![url](./images/internet-cables.png)

Fun fact, the internets largest foe isn't governments, thieves, or corporations. It's probably sharks. They bite the cables and no one knows exactly why...

![url](./images/shark.jpeg)

The World Wide Web is a service that exists on top of the internet and is commonly how most people consume and distribute information on the internet. The web was created in 1989 by Sir Tim Berners-Lee and his colleagues at CERN (European Organization for Nuclear Research).

What distinguishes the web from the internet is that it contains websites and webpages which are connected through hypertext links which are composed of a URI (uniform resources identifier) and some text. Websites on the internet are written in HTML and are accessible in browsers which communicate using the HTTP or HTTPS protocol and can render HTML (Hypertext Markup Language).

Sir Tim Berners-Lee and his colleagues created the internet as a social invention in order to connect people in the world. He said that he didn't ask for permission when he created it, he just did it. That's a directive for you to also be creative and find a need for your own inventions.

## How the Web Works

HTTP (Hypertext Transfer Protocol) is the language of the web and describes how webpages and files are sent over the internet. The protocol is based on a model of client and server: the client is either a program or a browser, and the server is the computer that has information about the web page.

The server that we make this request to is always located using a URL or URI which is composed of a few parts. Consider this URI: [https://go.flatironschool.com/getting_started](https://go.flatironschool.com/getting_started). The first part is the protocol `http://` or `https://` at the beginning of the URI, which describes the language that we're using to communicate with this website. The next is the domain which can either be an IP address or a string like `go.flatironschool.com`. When the domain is formatted as a string, we can divide each part of the string into separate parts: `com` is the top-level domain, `flatironschool` is the second-level domain, and we can continue with subdomains like `go` in the example above. Following the domain is a port address which is formatted like `go.flatironschool.com:80`, but these ports are implicit when accessing servers over either HTTP or HTTPS. And lastly is the resource that you want from this domain. In our example, it's the `/getting_started` resource.

![url](./images/url.png)

## What Happens when I Press Enter or Click a Link?

As we are browsing the internet and we click a link or type an address to our address bar, we say that a request is being made to a server. We're asking another computer somewhere else in the world to send us the webpage (a document) or some other information over the internet so that our browser can read it and present it to us. What exactly our browser gets back from the server is what we call a response, and this entire cycle is called the request-response lifecycle. When we make a request, we should get a response.

![url](./images/request-response.png)

There's actually a bunch of stuff that happens after the request is fired off and before the server even knows about the request. This whole process is called DNS lookup and is how we translate a domain name (or a string of text) into an IP address which is the permanent address of a web server.

When the browser receives the response, it has some information about the response itself, like its status, as well as a response body. The response body in the case of webpages is the actual HTML of the page. When the browser begins to read this HTML, it sometimes sees that other resources need to be requested for the webpage to be complete. These are usually things like images, fonts, data, or scripts.

In a very specific order, the browser loads all the assets it needs and begins to render the page. The HTML defines the structure as well as most of the external assets needed. The CSS defines how the page should look. The JavaScript defines how the page will behave once loaded and how the user can interact with it.

## Requests and Responses In-Depth

### RESTful Routes

| HTTP Verb | Path                  | Description                                     |
| --------- | --------------------- | ----------------------------------------------- |
| GET       | /newsletters          | # Show all newsletters                          |
| POST      | /newsletters          | # Create a new newsletter                       |
| GET       | /newsletters/new      | # Render the form for creating a new newsletter |
| GET       | /newsletters/:id/edit | # Render the form for editing a newsletter      |
| GET       | /newsletters/:id      | # Show a specific newsletter                    |
| PATCH     | /newsletters/:id      | # Update a newsletter                           |
| DELETE    | /newsletters/:id      | # Delete a newsletter                           |

### Requests

Breaking down the anatomy of requests we can see that there are a few distinct pieces. The request is made up of a request method, the requested resource's path, the protocol, the user-agent, some headers, and a request body.

> Headers are extra information that we send that aren't part of the request body itself, but tells the server how to formulate the response.

```text
GET /getting_started HTTP/1.1
User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
Host: go.flatironschool.com
Accept-Language: en-us
Accept-Encoding: gzip, deflate
Connection: Keep-Alive
```

The types of request methods, also called HTTP verbs, that we'll see here are GET, POST, PATCH, DELETE which map to READ, CREATE, UPDATE, and DESTROY pretty nicely at first. These allow us to do most of the work that is necessary on the internet.

The main difference between GET requests and POST and PATCH requests is that both POST and PATCH requests will have a request body, which is information that we send to the server to be processed. We'll talk about ways to format that information later on.

### Responses

HTTP Responses are formatted similarly to requests except for a few components. They have the protocol listed, the response status, some headers, and most responses will have a response body attached.

Here, headers are extra information that the server wants to communicate with the browser about this request. This could be information on how to cache the response body or just information about the server itself.

The two most important pieces to keep in mind are the status code and the response body. The status code tells us in summary what happened. When you go to a web page on your browser and you see what you requested, most likely the response code is `200 OK`. Other common response codes are `404 Not Found` and `500 Internal Server Error`.

```text
HTTP/1.1 404 Not Found
Date: Sun, 18 Oct 2012 10:36:20 GMT
Server: Apache/2.2.14 (Win32)
Content-Length: 230
Connection: Closed
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html>
<head>
   <title>404 Not Found</title>
</head>
<body>
   <h1>Not Found</h1>
   <p>The requested URL /t.html was not found on this server.</p>
</body>
</html>
```

## Making Requests from Postman or Insomnia

Postman is a client that lets you make all type of requests in a fairly easy to use UI. You can download it free from its website and it's great for testing APIs as well as learning how different types of request work and what's needed for each.

> Here, make a request using Postman to a website of your choosing. Show the response as HTML in its raw form and how it's just text. Then show the preview of the HTML in the preview tab.
