# Lab Report 2

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
![S1](lab2-s1)
![S2](lab2-s2)
