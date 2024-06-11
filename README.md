# analyzing_networl_layer_communication
Analyzing ICMP and DNS traffic using tcpdump

You are a cybersecurity analyst working at a company that specializes in providing IT services for clients. Several customers of clients reported that they were not able to access the client company website www.yummyrecipesforme.com, and saw the error “destination port unreachable” after waiting for the page to load. 

You are tasked with analyzing the situation and determining which network protocol was affected during this incident. To start, you attempt to visit the website and you also receive the error “destination port unreachable.” To troubleshoot the issue, you load your network analyzer tool, tcpdump, and attempt to load the webpage again. To load the webpage, your browser sends a query to a DNS server via the UDP protocol to retrieve the IP address for the website's domain name; this is part of the DNS protocol. Your browser then uses this IP address as the destination IP for sending an HTTPS request to the web server to display the webpage  The analyzer shows that when you send UDP packets to the DNS server, you receive ICMP packets containing the error message: “udp port 53 unreachable.” 

![Image](https://github.com/AxelVx1/analyzing_network_layer_communication/blob/main/Screenshot%202024-06-11%20at%202.03.39%20PM.png?raw=true)

My goals are to:
- Provide a summary of the problem found in the tcpdump log
- Explain your analysis of the data and provide one possible cause of the incident

Response:
| Part 1: Provide a summary of the problem found in the DNS and ICMP traffic log. |
| ------------------------------------------------------------------------------- |
| In this case, the UDP protocol was used to contact the DNS server to correctly retrieve the IP address for the domain name of “yummyrecipesforme.com.” Then the ICMP protocol responded with an error message indicating a problem with contacting the DNS server. The first two lines illustrate the communication between the source computer and the DNS server destination. The next lines display the error that is occurring in the communication, in this case, “udp port 53 unreachable.” We know that port 53 is associated with DNS protocol traffic meaning there is a problem with the DNS server. After reading more of the message we see more evidence of this because of the plus sign after the query identification number 35084 which indicates flags with the UDP message and the “A?” symbol which indicates flags with performing DNS protocol operations. With the ICMP response error message about port 53, it is more than likely that the DNS server isn’t responding. We can confirm this by looking at the rest of the messages containing the flags commonly associated with the outgoing UDP message and domain name retrieval.|

| Part 2: Explain your analysis of the data and provide at least one cause of the incident. |
| ----------------------------------------------------------------------------------------- |
| The incident happened today at 1:24 pm. The organization was notified about a message stating “destination port unreachable” when customers tried to access “yummrecipsforme.com.” The security team associated with the organization is actively investigating the situation so customers can continue to access the site. We conducted a quick investigation using packet analyzing tests using tcpdump. In the log file, we noticed that DNS port 53 was unreachable, so the next step is to identify why that is. It could be caused by the DNS being down or maybe the port is being blocked by a firewall. One reason the DNS server could be down is it could be experiencing a successful DoS/DDos.|
