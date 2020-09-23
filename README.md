<div align="center">

## WebTest


</div>

### Description

So you have built a cool web site with code you wrote or downloaded from great sites like planet-source-code, the next thing you might want to do is testing it: Can your code handle more than, say 10 concurrent users? Does it have a memory leak that will eventually lead to crash if you don't reboot?

Here is a java program I wrote that can query a web site continuously. If you want to simulate more than one user, just start as many instances of this program as you need. The command line to run it is:

java WebTest "http://www.yahoo.com/" 20000

This will query the www.yahoo.com site continuously, sleeping a random amount of time from 0 up to 20000 milliseconds between consecutive requests. If you omit the second parameter, the default number 10000 will be used.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[nfs](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/nfs.md)
**Level**          |Advanced
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |Java \(JDK 1\.1\), Java \(JDK 1\.2\)
**Category**       |[Complete Applications](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/complete-applications__2-64.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/nfs-webtest__2-2560/archive/master.zip)





### Source Code

```
import java.net.*;
import java.io.*;
import java.util.*;
public class WebTest
{
  public static void main (String[] args)
  {
    // initialize random seed
    Random randomGen = new Random(new Date().getTime());
    while(true)
    {
      try
      {
        // sleep for a random interval
        Thread.currentThread().sleep(randomGen.nextInt(args.length>1?(new Integer(args[1]).intValue()):10000));
        if(args.length>0)
        {
          // print the user supplied URL to the console window
          System.out.println(args[0]);
          // open URL connection
          URLConnection urlConn = new URL(args[0]).openConnection();
          urlConn.setUseCaches(false);
          // read and print the content to the console window
          InputStream in = urlConn.getInputStream();
          byte buf[] = new byte[4096];
          int nSize = in.read(buf);
          while(nSize>=0)
          {
            System.out.print(new String(buf,0,nSize));
            nSize = in.read(buf);
          }
          System.out.print("\r\n");
        }
        else return;
      }
      catch(Exception e)
      {
        // print error message
        System.out.println("Exception: "+e.getMessage());
      }
    }
  }
}
```

