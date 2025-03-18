In this tutorial we are going to learn about Internet Address, URLs and URIs which are core components in network programming. We are going to teach you how you may implement these concepts using a high level programming language. We will use Java to demonastrate these concepts. This is the part of the course where you really dive into the mesmerizing world of network programming. Up until now we have discussed the topics that you will need to know to go further.

Internet Address:

Let us first explain why we need to know about Internet Address in the first place.

First let us get used to some terms. The first term we are going to learn is called Node. A node is simply a device that is connected to the Internet. The second term we are going to learn is called Host. A host is a node which is a general purpose computer. In summary:

Node (Any device connected to the Internet):

1. A smartphone connected to Wi-Fi
2. A smart TV streaming Netflix
3. A Wi-Fi-enabled printer

Host (A node that is a general-purpose computer):

1. A laptop browsing the web
2. A desktop running a web server
3. A cloud server hosting a website

All hosts are nodes, but not all nodes are hosts (since some nodes, like printers and IoT devices, aren't general-purpose computers).

In this course when we talk about networking we are primarily going to mean "Internet" as most of the networking we do today happens on the Internet. But do not worry. You can easily use and implement these concepts that we learn in this course to your other networking needs i.e. on premises networking.

Now that we have defined these two terms let us go forward. 

If these devices (nodes and hosts) are all connected to the Internet and you want to send data from one device to another you need some way to uniquely identify them. Otherwise these devices won't know where to send data. 

Think of the internet like a courier service delivering parcels. When you send a parcel, you must include both your home address and the recipient’s address so the courier knows where to deliver it and where to return a response. If you do not mention the delivery address then the parcel company won't know where to deliver the parcel. And if you do not mention where to reach you to give the status of the parcel the delivery company can not give you the status update.

In the Internet, the device that are connected to the Internet, we assign unique number to each node or host to uniquely identify it. This is called Internet Address or IP Address in short. The sole purpose of assiging IP Address to a node or host is to uniquely identify it in the Internet amongst the billions of other nodes and hosts so that our data can reach its intended node or host.

There are two flavors of IP Address that we mainly use in the Internet to uniquely identify a host or node in the Internet. They are:

IPv4 (Internet Protocol Version 4)
Format: Four groups of numbers separated by dots (e.g., 192.168.1.1).
Range: Each number ranges from 0 to 255 (uses 32 bits).

IPv6 (Internet Protocol Version 6)
Format: Eight groups of four hexadecimal numbers separated by colons (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334).
Bit Length: Uses 128 bits, providing a vastly larger address space.

Both IPv4 and IPv6 addresses are structured as an ordered sequence of bytes, much like an array. They are not "real numbers" in the mathematical sense but rather a representation of data used for identification and communication in computer networks. Below is a list of reasons as to why IP Addresses are not real numbers: 

They Do Not Represent Quantities: Unlike real numbers (like 3.14 or 100), IP addresses do not have a numerical meaning for calculations. They simply act as labels for identifying devices.

They Are Not Used in Arithmetic: You cannot meaningfully add, subtract, or divide IP addresses. They are used for routing and communication, not mathematical operations.

They Are Stored and Processed as Byte Sequences: Computers handle IP addresses as binary data rather than decimal or hexadecimal numbers.

In short, An IP address is more like a string of structured bytes than a real number. It follows a defined format for network identification rather than representing a quantity or being used in mathematical computations. 

The dot(.) in the case of IPv4 Address, an the colon(:) is used for the convenience of human eyes. Each of the four bytes in the IPv4 Address ranges from 0 to 255. An IPv4 Address of the format 257.255.0.1 is not valid because the first byte range is greater than 255. This format of four bytes ranging from 0 to 255 separated each byte by a period is called dotted quad format.

Though IP Addresses are great from computers, they are not so convenient for the humans. Human tends to have a hard time remembering long numbers (we again referred IP Address as numbers. This is because the IP Addresses are normally referred as numbers in the real world. It is one of those human nuances where the definition somehow contrasts the real use.). 

The pioneer of the Internet invented a system called Domain Name System (DNS) to address this issue. DNS (Domain Name System) essentially assigns human-readable names(called host names) to IP addresses, making it easier for users to access websites and services on the internet.

Think of DNS like a phonebook for the internet. Instead of remembering long, complicated IP addresses (like 142.250.190.46 for Google), we can simply type www.google.com, and DNS translates it into the correct IP address.

You enter a domain name (e.g., www.example.com) in your browser.
The DNS system looks up the IP address associated with that domain.
Your device connects to the correct server using the IP address.
The website loads on your screen as if you typed the IP address directly.

People often use "Internet Address" to mean a host-name. But as a network programmer you should mind the distinction. You should be precise about Address and Host name. An address is always a numeric IP Address which is great for computers. A hostname is a human-readable format.

A DNS server (Domain Name System server) is a system that translates human-readable domain names (like www.example.com) into IP addresses (like 192.168.1.1) so that computers can communicate with each other over the internet.

What Does a DNS Server Do?
When you enter a website address (URL) in your browser, your device needs to find out the IP address associated with that domain to connect to the website. This is where the DNS server comes in. It acts as a translator between human-friendly domain names and machine-friendly IP addresses.

We will not dive into more details in this course regarding Addresses and host names. What we have discussed so far is enough to get started with network programming.

The InetAddress Class

In java, the InetAddress class is used to represent an IP address, both IPv4 and IPv6. Most of the other netwokring classes in java, including Socket, ServerSocket, URL and more use this class. Do not mind about the other classes. We will discuss them later in this course. What you need to remember now is the InetAddress class is used to represent the Internet Address and it included both a hostname and an IP address.

How to create a new InetAddress Object?

The InetAddress class in Java follows a design pattern call Factory Design Pattern. The Factory Design Pattern is used when object creation logic is abstracted away from the client. You can not directly use new keyword to instantiate an object of a class that is designed using the Factory Design Pattern. Instead of directly using a constructor, the class provides static factory methods to create instances.

Instead of having any public constructor in the class definition, the InetAddress has static factory methods that connect to a DNS server to resolve a hostname. The most common and the one you will primarily use is the following:


InetAddress.getByName();

For example, if you want to look up www.google.com you will do something like this:

```java
import java.net.InetAddress;

import java.net.InetAddress;
import java.net.UnknownHostException;

public class InetAddressExample {
    public static void main(String[] args) {
        try {
            InetAddress address = InetAddress.getByName("google.com");
            System.out.println("Google IP Address: " + address.getHostAddress());
        } catch (UnknownHostException e) {
            System.out.println("Unable to resolve host: google.com");
        }
    }
}
```

This method does not merely set a private String in the InetAddress class but it actually makes a connection to the local DNS server to look up the name and the numeric address. The method throws an UnknownHostExceptio which is a subclass of IOException, if the DNS server can't find the address.

If you want to get the hostname for a IP Address, a reverse lookup, you can do this using the InetAddress class. To do this you have to pass the dotted quad address to the InetAddress.getByName() as paramters.

```java
InetAddress address = InetAddress.getByName("208.201.239.100");
System.out.println(address.getHostName());
```

In this scenario, if your look up does not have a hostname, getHostName() simply returns the dotted quad address that you gave as parameter.

In the case of a hostname referring to more than one IP Addresses you should use the following and if for some reason you need all the addresses of the host, use getAllByName(). This method returns an array:

```java
try {
    InetAddress[] addresses = InetAddress.getAllByName("www.google.com");
    for (InetAddress address : addresses) {
        System.out.println(address);
    }
} catch (UnknownHostException ex) {
    System.out.println("Could not find www.google.com");
}
```

Last but not least, if you want to get an InetAddress object for the host on which your code is running use getLocalHost():

```java
InetAddress localHost = InetAddress.getLocalHost();
```

This method tries to connect to DNS to get a real hostname and IP address such as
"www.google.com" and "192.1.254.68"; but if that fails it may return the loopback
address instead. This is the hostname "localhost" and the dotted quad address
"127.0.0.1".

There is another factory method in the InetAddress class which lets you create a InetAddress object from a numeric address and hostname(optional). This methods are helpful when a domain name server is not available to you or might have inaccurate information.

```java
public static InetAddress getByAddress(String host,byte[] addr)
    
public static InetAddress getByAddress(byte[] addr)
```

These methods can create addresses for hosts that do not exist or can not be resolved. The following examples demonastrates this:

```java
byte[] address = {107, 23, (byte) 216, (byte) 196};
InetAddress inetAddress = InetAddress.getByAddress(address);
InetAddress inetAddress = InetAddress.getByAddress(
"www.google.nosite", address);
```

You have to cast the large values to bytes as these two methods take bytes as its parameters. The methods throws an UnknownHostException if the byte array size is neither 4 nor 16 bytes long. These methods are helpful when the hosts are not registered any DNS server but they are assigned IP Addresses.

What to use IP Address or hostname?

The getByName() method can be called the host's name.
The host name can either be a machine name, such as "www. google.com", or a textual representation of its IP address. When the IP address string is used as an argument, the InetAddress object returned is created for the requested IP address without checking with DNS. So you may run into situations where the host does not exists and you can not connect to using the InetAddress object. The hostname of an InetAddress object created from a string containing an IP address is initially set to that string. A DNS lookup for the actual hostname is only performed when the hostname is requested, either explicitly via a getHostName(). That’s how www.google.com was determined from the dotted quad address
208.201.239.37. If, at the time the hostname is requested and a DNS lookup is finally performed, the host with the specified IP address can’t be found, the hostname
remains the original dotted quad string. However, no UnknownHostException is thrown.

We would suggest you to choose hostname to create an InetAddress object orver IP Address. Hostnames are more stable than IP Addresses. Some services on the Internet has retained the same hostname for years, but changed the IP Addresses quite a few times. Try to use IP Address only when a hostname is not available. Some may argue that as creating a new InetAddress object from a hostname is requires a DNS lookup it may be considered insecured. Java provides several mechanisms to handle this issue.

Getter & Setter Methods

There are four getter methods in the InetAddress class that return the hostname as a string and the IP Address as both a string and byte array. 

```java
public String getHostName()
public String getCanonicalHostName()
public byte[] getAddress()
public String getHostAddress()
```

There are no setHostName() and setAddress() methods in the InetAddress class which makes thevInetAddress immutable. This ensures thread safety.

Please refere to the documentation for further details about the getter methods. If we try to explain everything in detail in this course the course will be very long and boring. The purpose of this course is to introduce you to the concepts that will get you started with the network programming and build a solid foundation. For further study always refer to the official documentation of Java which is a rich source of information.

The concepts you have learnt up until now can be used to write some useful and interesting programs.