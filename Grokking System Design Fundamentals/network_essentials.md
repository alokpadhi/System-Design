# HTTP vs. HTTPS

Here is a detailed summary of the "HTTP vs. HTTPS" page, with examples:

***

### **What is HTTP?**
- **HTTP (HyperText Transfer Protocol):**  
  The foundational protocol for transmitting data on the web. It fetches and displays content from web servers in response to user requests.

#### **Key Features:**
- **Stateless:** Each request is independent; the server does not remember previous client actions.
- **Text-Based:** Information is transmitted in plain, readable text.
- **Port 80:** Communicates over network port 80.

#### **Example Use Case:**  
Browsing a public blog, informational website, or resources where you’re not entering sensitive data (e.g., reading a cooking recipe). No encryption or confidentiality is needed, so HTTP’s speed may be an advantage.

***

### **What is HTTPS?**
- **HTTPS (HyperText Transfer Protocol Secure):**  
  An extension of HTTP, adding SSL/TLS encryption for secure data transmission.

#### **Key Features:**
- **Encryption:** Data is encoded during transit, so even if intercepted, it’s unreadable.
- **Authentication:** Confirms the website you reach is legitimate, preventing “man-in-the-middle” attacks.
- **Data Integrity:** Ensures data isn’t tampered with en route.
- **Port 443:** Communicates over network port 443.

#### **Example Use Case:**  
Online shopping, banking, or logging in to social networks—any transaction handling passwords, credit card details, or personal information. Eavesdroppers can’t steal data, and browsers show a padlock icon for secure sites.

***

### **Key Differences Between HTTP and HTTPS**

| Feature      | HTTP                          | HTTPS                            |
|--------------|------------------------------|----------------------------------|
| Security     | No encryption; plain text     | SSL/TLS encrypted                |
| Port         | 80                           | 443                              |
| Performance  | Slightly faster               | Slightly slower (encryption cost)|
| SEO          | Lower ranking                 | Higher ranking (preferred by search engines) |
| Use Case     | Public/non-sensitive content  | Confidential/sensitive transactions |

***

### **Why Does HTTPS Matter?**
1. **Security:** Essential to prevent cyberattacks, eavesdropping, and data breaches.
2. **Trust:** Users trust and prefer sites with HTTPS (padlock icon in browsers).
3. **SEO Ranking:** Search engines rank HTTPS sites above HTTP sites.
4. **Compliance:** Meeting regulatory requirements for user data protection.

***

### **Conclusion and Quick Reference**

- **HTTP:** For public blogs and information sites (no sensitive data).
- **HTTPS:** For e-commerce, financial sites, and *all* sites where user privacy, credentials, or payment details are involved.

***

**Example Comparison:**  
Logging into your bank should always use HTTPS, safeguarding your credentials and transactions. Reading a public news article may use HTTP, as there is no risk if the data is seen by others.

By adopting HTTPS, sites secure user data, build trust, improve search visibility, and comply with industry regulations. In the modern web landscape, HTTPS is a necessity for any site involving user interactivity or data privacy.

[ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/http-vs-https)

# TCP vs. UDP

Here is a detailed summary of the "TCP vs. UDP" page, with examples:

***

### **TCP (Transmission Control Protocol)**
- **Definition:** A connection-oriented protocol ensuring reliable, ordered, and error-checked delivery of data between applications.
- TCP is a reliable way for computers to send data to each other over the internet, making sure all the information arrives correctly and in the right order.
- Think of TCP like sending a registered letter through the postal service - it establishes a connection first, breaks your message into smaller pieces (packets), numbers them, sends them separately, and then puts them back together at the destination while confirming   each piece arrived safely. If any packets get lost or damaged during transmission, TCP automatically requests they be sent again.
- This makes TCP perfect for things like web browsing, email, and file downloads where you need every bit of data to arrive perfectly, even if it takes a little longer. The protocol handles all the complex networking details behind the scenes, so applications don't    need to worry about lost or corrupted data - TCP guarantees that what you send is exactly what gets received.
- **Key Characteristics:**
  - **Reliability:** Guarantees data reaches the receiver intact and in order; lost/corrupted packets are retransmitted.
  - **Connection-Oriented:** Requires establishing a connection before data transfer.
  - **Flow Control:** Adjusts data rate to prevent overwhelming the network.
  - **Congestion Control:** Monitors network traffic and adapts transmission speed accordingly.
  - **Acknowledgments and Retransmissions:** Uses acknowledgment messages to confirm receipt; will resend lost data.
- **Use Cases:** Web browsing (HTTP/HTTPS), email (SMTP, POP3, IMAP), and file transfers (FTP).
- **Example:**  
  - **Loading a web page:** The browser and server establish a TCP connection to ensure that all the data (HTML, CSS, scripts, images) arrives correctly and in sequence.

***

### **UDP (User Datagram Protocol)**
- **Definition:** A connectionless protocol for sending datagrams without guaranteeing delivery, order, or error-checking.
- UDP is a fast way for computers to send data to each other over the internet without worrying about whether it arrives perfectly - speed is more important than accuracy.
- Think of UDP like sending a postcard through regular mail - you write your message, put the address on it, and drop it in the mailbox without any confirmation that it arrived. Unlike TCP's "registered letter" approach, UDP doesn't establish a connection first, doesn't number the packets, and doesn't wait for confirmation that each piece arrived safely.
- UDP operates on a "fire and forget" principle - it sends data as fast as possible and hopes it reaches its destination. The protocol has minimal overhead with just an 8-byte header compared to TCP's much larger header, making it significantly faster
- **Key Characteristics:**
  - **Low Overhead:** No need for connection setup/teardown—less latency.
  - **Unreliable Delivery:** No guarantees; data may arrive late, out of order, or not at all.
  - **Speed:** Faster than TCP, suitable for applications needing quick delivery.
  - **No Congestion Control:** Data continues at the same rate regardless of congestion.
- **Use Cases:** Real-time streaming (audio/video), online gaming, VoIP.
- **Example:**  
  - **Streaming a live sports match:** Video is sent via UDP for lowest latency. Occasional loss or out-of-order segments may cause momentary glitches, but the stream continues smoothly and quickly for viewers.
  - **Online Gaming**: When playing multiplayer games, UDP sends your movement data instantly - if one packet showing your character's position gets lost, it doesn't matter because the next packet with your updated position is already on the way.
  - **Voice Calls**: VoIP services like Skype use UDP because real-time conversation requires immediate delivery - a slightly garbled word is better than a delayed conversation.

***

### **Key Differences Table**

| Aspect        | TCP                                   | UDP                              |
|---------------|---------------------------------------|-----------------------------------|
| Reliability   | High (guaranteed, in-order delivery)  | Low (no guarantees)               |
| Connection    | Connection-oriented                   | Connectionless                    |
| Speed         | Slower (due to checks/retransmits)    | Faster (minimal protocol overhead)|
| Use Cases     | Browsing, email, file transfers       | Streaming, gaming, live audio     |
| Data Integrity| High                                  | Lower (may lose/corrupt packets)  |

***

**Summary:**  
TCP is favored for applications where data accuracy is crucial. UDP is chosen for real-time scenarios where speed is more important than perfect delivery—some data loss is acceptable for lower latency and smoother, faster experience.Here is a detailed summary of the "TCP vs. UDP" page with examples:

***

### **TCP (Transmission Control Protocol)**
- **Definition:**  
  TCP is a reliable, connection-oriented protocol. It guarantees that data is delivered accurately and in the correct order between sender and receiver.
- **Characteristics:**  
  - Ensures every byte is delivered exactly once and in order.
  - Requires an initial handshake (connection setup) before data transfer.
  - Provides error checking, acknowledgments, retransmission of lost data, flow and congestion control.
- **Common Use Cases:**  
  - Web browsing (HTTP/HTTPS)
  - Email (SMTP, IMAP, POP3)
  - File transfer (FTP)
- **Example:**  
  Loading a webpage over HTTPS: TCP ensures all text, images, and scripts arrive at the browser in the right order. If any data is lost in transit, it’s resent.

***

### **UDP (User Datagram Protocol)**
- **Definition:**  
  UDP is a lightweight, connectionless protocol. It sends messages (“datagrams”) to the recipient without ensuring delivery, order, or error correction.
- **Characteristics:**  
  - No connection setup required—lower delay and overhead.
  - No built-in guarantee of delivery, ordering, or duplicate protection.
  - No congestion or flow control—messages sent as fast as possible.
- **Common Use Cases:**  
  - Live streaming (video/audio)
  - Online gaming
  - VoIP (Voice over IP)
- **Example:**  
  Watching a live sports stream: UDP delivers video and audio with minimal delay. If some packets are lost or out of order, the stream may stutter or have minor glitches momentarily, but playback continues with the latest data.

***

### **Key Differences**

|   Feature     |         TCP           |           UDP            |
|:-------------:|:---------------------:|:------------------------:|
| Reliability   | Guaranteed, retransmit| No guarantee             |
| Ordering      | In order              | Not guaranteed           |
| Connection    | Connection-oriented   | Connectionless           |
| Speed         | Slower, more overhead | Faster, less overhead    |
| Use Case      | Accuracy critical     | Speed critical           |

***

**Summary:**  
**TCP** is used when you cannot tolerate errors or out-of-order data (websites, email, downloads).  
**UDP** is preferred when speed and low latency matter more than perfection (live video/audio, games, real-time chat).

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/tcp-vs-udp)

# HTTP: 1.0 vs. 1.1 vs 2.0 vs. 3.0

Here’s a focused summary of the “HTTP: 1.0 vs. 1.1 vs. 2.0 vs. 3.0” page, with examples:

***

### **HTTP/1.0 (1996)**
- **Key Features:**  
  - Simple request-response; each request opens a new TCP connection (no connection reuse)
  - Stateless and uses basic headers
- **Example Use:**  
  - Early static web pages and simple blogs, where each image or file loaded opened a new connection (slow for modern needs).

***

### **HTTP/1.1 (1997)**
- **Key Features:**  
  - Persistent connections (keep-alive) allow multiple requests per connection, reducing latency
  - Chunked transfer encoding for streaming data
  - Better caching and host header support for virtual hosting
- **Example Use:**  
  - E-commerce sites serving images, scripts, and styles, loading many resources efficiently via a single connection.

***

### **HTTP/2.0 (2015)**
- **Key Features:**  
  - Binary protocol (not text-based)
  - **Multiplexing:** Many requests and responses share a single connection—no head-of-line blocking
  - **Header compression (HPACK)**
  - **Server push:** Server can send resources before requested
- **Example Use:**  
  - Social platforms/streaming sites (e.g., YouTube, Facebook) where dozens of resources are loaded in parallel with reduced load times.

***

### **HTTP/3.0 (2020)**
- **Key Features:**  
  - Built on the QUIC protocol (over UDP instead of TCP)
  - Faster connection establishment (0-RTT handshake) and lower latency
  - Handles packet loss gracefully, improving real-world performance
  - Built-in TLS 1.3 encryption for security
- **Example Use:**  
  - Real-time apps: video conferencing (Zoom), online gaming, live streaming—where speed, reliability, and reduced lag are crucial even on unstable mobile connections.

***

### **Key Differences Table**

| Feature          | HTTP/1.0      | HTTP/1.1               | HTTP/2.0         | HTTP/3.0 (QUIC)        |
|------------------|---------------|------------------------|------------------|------------------------|
| Connection Model | Per request   | Persistent             | Multiplexed      | One QUIC (UDP-based)   |
| Protocol         | Text          | Text                   | Binary           | Binary over QUIC/UDP   |
| Latency          | High          | Low                    | Very low         | Lowest (network loss)  |
| Security         | Optional      | Optional               | Optional         | Required (TLS 1.3)     |
| Use Case         | Static pages  | Dynamic/web apps       | Rich apps/sites  | Real-time/streaming    |

***

### **Why Upgrade?**
- Improved speed, security, and support for modern, high-demand applications.
- Example: Video conferencing software relies on HTTP/3.0 for smoother, lag-free communications globally.

***

**Summary:**  
- **HTTP/1.0:** Basic, one connection per request—obsolete for modern web.
- **HTTP/1.1:** Reused connections, chunking—still widely used.
- **HTTP/2.0:** Multiplexed, compressed, more efficient—now standard for large-scale web services.
- **HTTP/3.0:** Even faster and more reliable for dynamic, global, real-time apps thanks to QUIC and built-in encryption.Here is a detailed summary of the HTTP version evolution with practical examples:

***

### **HTTP/1.0 (1996)**
- **Connection:** Opens a new connection for each request/response pair, then closes it.
- **Use Case Example:**  
  - Early static websites or blogs where each image, page, or CSS file load would start a whole new TCP connection.

***

### **HTTP/1.1 (1997)**
- **Connection:** Supports persistent (keep-alive) connections, enabling multiple requests/responses on one connection.
- **Improvements:** Chunked transfer encoding, better caching, virtual hosting (multiple domains per IP via Host header).
- **Use Case Example:**  
  - Modern websites with many images/scripts/stylesheets benefit by loading all resources efficiently over one connection.

***

### **HTTP/2.0 (2015)**
- **Protocol:** Binary (not text-based), uses header compression and a single connection (multiplexing) for simultaneous many streams.
- **Server Push:** Server can proactively send needed resources to client.
- **Use Case Example:**  
  - High-traffic sites (like YouTube or Facebook) load dozens of resources in parallel for smooth, fast user experience.

***

### **HTTP/3.0 (2020)**
- **Built On:** QUIC (UDP) for reliable, fast, encrypted transport.
- **Features:** Faster handshakes (0-RTT), better packet loss handling, integrated encryption (TLS 1.3).
- **Use Case Example:**  
  - Video conferencing and live streaming (e.g., Zoom/Teams) benefit from lower latency and smooth transmission over less reliable networks.

***

**Summary Table:**

| Feature           | 1.0            | 1.1                  | 2.0                | 3.0 (QUIC)              |
|-------------------|----------------|----------------------|--------------------|-------------------------|
| Connection Model  | Per request    | Persistent           | Multiplexed single | Multiplexed over QUIC   |
| Protocol          | Text           | Text                 | Binary             | Binary (UDP-based)      |
| Security          | Optional       | Optional             | Often with TLS     | Always, TLS 1.3         |
| Speed/Latency     | Slow           | Faster               | Fastest (till 3.0) | Fastest in poor networks |
| Sample Use Case   | Static sites   | Ecommerce, web apps  | Social media, SaaS | Realtime/gaming/stream  |

***

**Conclusion:**  
Newer HTTP versions reduce latency, improve security, handle poor networks better, and support the demanding needs of modern web and real-time applications. For example, HTTP/3.0’s QUIC protocol is ideal for live sports streaming or multiplayer gaming, where speed and reliability matter most.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/http-10-vs-11-vs-20-vs-30)

# URL vs. URI vs. URN

Here is a detailed summary of the "URL vs. URI vs. URN" page with clear examples:

***

### **URL (Uniform Resource Locator)**
- **Definition:** A URL is a type of URI that not only identifies a resource on the internet but also provides a way to locate it by describing its access mechanism (usually its network location).
- **Key Components:** Protocol (HTTP/HTTPS/FTP), domain, path, optional query parameters or fragment.
- **Example:**  
  - `https://www.example.com/path?query=term#section`  
    This specifies how (HTTPS), where (www.example.com), and what path/query to use.
- **Key Traits:**  
  - Tells both how to access and where to find the resource.

***

### **URI (Uniform Resource Identifier)**
- **Definition:** A URI is a general term for any identifier of a resource—can identify by location (URL), by name (URN), or both.
- **Scope:** Every URL and URN is a URI, but not all URIs are URLs or URNs.
- **Examples:**  
  - URL: `https://www.example.com` (is also a URI)
  - URN: `urn:isbn:0451450523` (is also a URI)
- **Key Traits:**  
  - The most generic term; can identify, locate, or do both.

***

### **URN (Uniform Resource Name)**
- **Definition:** A URN is a URI type that names a resource but does not describe its retrieval or location.
- **Example:**  
  - `urn:isbn:0451450523` uniquely identifies a book using its ISBN, with no info on how/where to access it.
- **Key Traits:**  
  - Provides a persistent, unique name only—not a web or network address.

***

### **Summary Table**

| Term | Focus                   | Example                              | What it Does                  |
|------|-------------------------|--------------------------------------|-------------------------------|
| URL  | Location & access       | `https://www.example.com/image.jpg`  | Where & how to get the file   |
| URI  | Generic (ID/Name/Where) | Any URL/URN is a URI                 | Just identifies something     |
| URN  | Unique naming only      | `urn:isbn:0451450523`                | Unique name, not location     |

***

**Summary:**  
- **URL** specifies both identity and location ("how and where" to find).
- **URI** is the broadest term, covering URLs (locating) and URNs (naming).
- **URN** uniquely identifies a resource *without* saying where it is or how to get it.

**Example in Context:**  
- In web browsing, you mostly use URLs.
- URNs are useful in libraries or digital archives for identifying books or objects regardless of their location.
- URIs are the umbrella term used in web standards, programming, and network specification.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/url-vs-uri-vs-urn)
