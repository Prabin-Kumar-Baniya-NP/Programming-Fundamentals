## 1. What happens when you enter google.com in the web browser?

- Below are the steps that are being followed:

1. Check the browser cache first if the content is fresh and present in cache display the same.
2. If not, the browser checks if the IP of the URL is present in the cache (browser and OS) if not then request the OS to do a DNS lookup using UDP to get the corresponding IP address of the URL from the DNS server to establish a new TCP connection.
3. A new TCP connection is set between the browser and the server using three-way handshaking.
4. An HTTP request is sent to the server using the TCP connection.
5. The web servers running on the Servers handle the incoming HTTP request and send the HTTP response.
6. The browser process the HTTP response sent by the server and may close the TCP connection or reuse the same for future requests.
7. If the response data is cacheable then browsers cache the same.
8. Browser decodes the response and renders the content.
