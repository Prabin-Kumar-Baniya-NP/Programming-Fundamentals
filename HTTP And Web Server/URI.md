# URI

### [From Udacity - HTTP and Web Server Course]

- A URI is a name for a resource — such as this lesson page, or a Wikipedia article, or a data source like the Google Maps API. URIs are made out of several different parts, each of which has its own syntax. Many of these parts are optional, which is why URIs for different services look so different from one another.

- Here is an example of a URI: https://en.wikipedia.org/wiki/Fish

- This URI has three visible parts, separated by a little bit of punctuation:
  - https is the scheme;
  - en.wikipedia.org is the hostname;
  - and /wiki/Fish is the path.

## Scheme

- The first part of a URI is the scheme, which tells the client how to go about accessing the resource.
- Some URI schemes you've seen before include http, https, and file.
- File URIs tell the client to access a file on the local filesystem. HTTP and HTTPS URIs point to resources served by a web server.
- mailto is used for links to email addresses.
- data is used to put a piece of hardcoded data directly into a web page, for instance a small image.
- magnet is used for links to some file-sharing services such as BitTorrent.

## Hostname

- In an HTTP URI, the next thing that appears after the scheme is a hostname — something like www.udacity.com or localhost. This tells the client which server to connect to.

- You'll often see web addresses written as just a hostname in print. But in the HTML code of a web page, you can't write <a href="www.google.com">this</a> and get a working link to Google. A hostname can only appear after a URI scheme that supports it, such as http or https. In these URIs, there will always be a :// between the scheme and hostname.

- By the way, not every URI has a hostname. For instance, a mailto URI just has an email address: mailto:spam@example.net is a well-formed mailto URI. This also reveals a bit more about the punctuation in URIs: the : goes after the scheme, but the // goes before the hostname. Mailto links don't have a hostname part, so they don't have a //.

## Path

- In an HTTP URI (and many others), the next thing that appears is the path, which identifies a particular resource on a server.
- A server can have many resources on it — such as different web pages, videos, or APIs. The path tells the server which resource the client is looking for.

