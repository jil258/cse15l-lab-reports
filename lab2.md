# Lab Report 2

## Part1
**Code for StringServer**
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    int num = 1;
    String info = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("String Server Running", num);
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    info += num + ". " +  parameters[1] + "\n";
                    num ++;
                    return String.format(info);
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
![S1](lab2-s1.png)
#### `handleRequest` Method
Method handles incoming HTTP requests based on the path of the URI.

- If the path is `/`, it returns `"String Server Running"`.
- If the path contains `/add-message`, it processes the query parameters to add a message to the `info` field and returns the updated messages.
- For any other path, it returns `"404 Not Found!"`.

### Usage and Field Changes with /add-message

When the `/add-message` endpoint is called with a query parameter like `?s=Hello`:

#### Method Calls:
- `handleRequest(URI url)`: This method is called with a `URI` object representing the new URI("http://localhost:4000/add-message?s=Hello").

#### Arguments and Values:
- `url`: A `URI` object representing the URL `"http://localhost:4000/add-message?s=Hello"`.
- `num`: Initially 1
- `info`: Initially ""

#### Field Changes:
- `info`: This field will concatenate the current value of `num`, the received message, and a newline character. If the initial value was "" and `num` was 1, it becomes `"1. Hello\n"`.
- `num`: This field increments by 1.


![S2](lab2-s2.png)
#### Second Call Method
The second call to `/add-message?s=How%20are%20you`, will have the same method called describe above but different URI object.

#### Initial Values and Parameters
- `url`: A `URI` object representing the URL `"http://localhost:4000/add-message?s=How%20are%20you"`.
- `num`: 2
- `info`: "1. Hello\n"
  
#### Field Changes:
- `info`: Concatenates `"2. How are you\n"` to the existing messages, becoming `"1. Hello\n2. How are you\n"`.
- `num`: Increments to 3.


##  Part2

### Private key
```
> ls ~/.ssh/id_ed25519.pub
/Users/lijianpeng/.ssh/id_ed25519.pub
```

### Public key
```
[cs15lfa23rs@ieng6-203]:~:34$ ls ~/.ssh/authorized_keys 
/home/linux/ieng6/cs15lfa23/cs15lfa23rs/.ssh/authorized_keys
```

### log into ieng6
```
> ssh cs15lfa23rs@ieng6.ucsd.edu
Last login: Wed Oct 11 17:20:41 2023 from tower-us8.prod.edstem.org
============================ NOTICE =================================
Authorized use of this system is limited to password-authenticated
usernames which are issued to individuals and are for the sole use of
the person to whom they are issued.

Privacy notice: be aware that computer files, electronic mail and 
accounts are not private in an absolute sense.  You are responsible
for adhering to the ETS Acceptable Use Policies, which you can review at:
https://blink.ucsd.edu/faculty/instruction/tech-guide/policies/ets-acceptable-use-policies.html
=====================================================================

*** Problems, Suggestions, or Feedback ***
    
    For help requests, please create a ticket at:
    https://support.ucsd.edu/its 

    You may also report issues, suggestions, or feedback by e-mailing root on any system:
    mail -s "Your subject here" root
    Type your message - Ctrl+D to send
    
*** Access our Linux ssh terminals or remote desktops via a web browser at: ***
    https://linuxcloud.ucsd.edu

    All accounts must be enrolled in Duo for access. No VPN required.


-------------------------------------------------------

quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-19_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-10-01_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/hourly.2023-09-29_2001: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-21_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-30_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/hourly.2023-09-29_1601: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/hourly.2023-09-30_0801: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/weekly.2023-09-03_0015: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/hourly.2023-09-29_1201: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-26_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-28_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/hourly.2023-09-30_1201: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-23_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-18_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/hourly.2023-09-30_1601: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/hourly.2023-09-30_2001: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/weekly.2023-09-10_0015: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/hourly.2023-10-01_0801: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-24_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-22_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-20_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-29_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-27_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2023-09-25_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-19_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-10-01_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/hourly.2023-09-29_2001: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-21_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-30_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/hourly.2023-09-29_1601: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/hourly.2023-09-30_0801: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/weekly.2023-09-03_0015: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/hourly.2023-09-29_1201: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-26_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-28_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/hourly.2023-09-30_1201: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-23_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-18_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/hourly.2023-09-30_1601: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/hourly.2023-09-30_2001: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/weekly.2023-09-10_0015: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/hourly.2023-10-01_0801: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-24_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-22_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-20_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-29_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-27_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/staff/.snapshot/daily.2023-09-25_0010: Stale file handle
Hello cs15lfa23rs, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   11:05:01   1  0.01,   0.11,   0.16
ieng6-202   11:05:01   4  0.78,   0.31,   0.23
ieng6-203   11:05:01   4  11.71,  11.89,  12.19

 
Sat Oct 21, 2023 11:09am - Prepping cs15lfa23
```

## Part 3

I didn’t know that we could directly access a remote server via the terminal and interactively make changes on the server in real-time. I also thought that creating a server using a Java file was incredibly cool, as I have only used Node.js for backend tasks.
