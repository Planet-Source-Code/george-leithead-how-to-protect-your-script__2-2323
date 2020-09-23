<div align="center">

## How to protect your script\.\!\!


</div>

### Description

It's quite common, and I do it my self! I find a site that has some interesting script, and I 'borrow it'. I wouldn't say steal, as I usually re-write it, but the net effect is the same. Someone else has done the work, and since it's on a web site, almost anyone with some know how can 'borrow it'.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[George Leithead](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/george-leithead.md)
**Level**          |Beginner
**User Rating**    |2.7 (27 globes from 10 users)
**Compatibility**  |
**Category**       |[Security](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/security__2-74.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/george-leithead-how-to-protect-your-script__2-2323/archive/master.zip)





### Source Code

It's quite common, and I do it my self! I find a site that has some interesting script, and I 'borrow it'. I wouldn't say steal, as I usually re-write it, but the net effect is the same. Someone else has done the work, and since it's on a web site, almost anyone with some know how can 'borrow it'.<br >
<br >
Nowadays, like so many other developers, when it comes to developing a front end (GUI) I use a lot of JavaScript. As soon as this script is available to the general public, it's almost certain that someone will come along and take a copy. Well, I have thought of a simply way of stopping people from getting at my code. It's by no mean's perfect, but it goes a heck of a way to stop the casual surfer.<br >
<br >
My solution is based on using IIS and ASP (Active Server Pages). I'm sure that there is a similar solution for other web servers, and I'd be equally interested in hearing about them. My solution is simple, short, and easily implemented!<br >
<br >
As you know, script on the client side (in the browser), defines code that is executed when a page is loaded, or an action is performed, something like a 'MouseOver' (You have probably seen it a hundred times, when you move your mouse over an icon, the icon changes). This script can be either contained within the web page (In-Line), or contained in an externally referenced file, by means of a source parameter. All code can be downloaded from <a href="http://forums.internetwideworld.com/CodeSamples/How_To_Protect_Your_Script.zip">here</a><br >
<br >
In-Line code example:<br >
<font color="darkgreen">
&lt;html&gt;<br >
&lt;head&gt;<br >
&lt;title&gt;How to protect your script!&lt;/title&gt;<br >
&lt;script language="JavaScript"&gt;<br >
alert('In-Line Code');<br >
&lt;/script&gt;<br >
&lt;/head&gt;<br >
&lt;body&gt;<br >
This is the document body!<br >
&lt;/body&gt;<br >
&lt;/html&gt;<br >
</font>
<br >
Externally referenced file example:<br >
<font color="darkgreen">
&lt;html&gt;<br >
&lt;head&gt;<br >
&lt;title&gt;How to protect your script!&lt;/title&gt;<br >
&lt;script language="JavaScript" src="MyJavaScript.js"&gt;&lt;/script&gt;<br >
&lt;/head&gt;<br >
&lt;body&gt;<br >
This is the document body!<br >
&lt;/body&gt;<br >
&lt;/html&gt;<br >
</font>
<br >
The thing to look for here is the 'src' parameter. This indicates that the JavaScript is contained in another file, namely MyJavaScript.js (the js extension, signifies that it's a JavaScript file). The contents of the MyJavaScript.js file is as follows:<br >
<br >
<font color="darkgreen">alert('In-Line Code');</font><br >
<br >
Now, to the end user, there IS no difference. Both of the web pages look and act exactly the same!<br >
<br >
So, now we get to the clever part and actually protect our scripts. What if, instead of using a .js file, but instead we use an ASP file? So, instead of MyJavaScript.js, we reference the file MyJavaScript.asp Sure, an ASP file that simply contains the same code as the .js file achieves nothing. It still does exactly the same thing! So, HOW do I protect my script?<br >
<br >
Firstly, we need to know how people get a hold of your script. Obviously, if it's simply in-line, they simply view the source, and copy from there. However, if it's an external file, they have to enter the URL to the file. E.g. http://www.internetwideworld.com/MyJavaScript.asp<br >
<br >
If they go to the URL, they'll simply get the contents of the file displayed! So, we have to prevent the file from being viewed if accessed via a URL.<br >
<br >
In ASP, you'll find that there is a collection of server environment variables, also known as ServerVariables. These server variables contain lots of useful information about the server that your code is on, and more. The server variable we're interested in is the HTTP_REFERER. If the page is referred to by another page, then the HTTP_REFERER variable holds the URL to the referring page. So, if the JavaScript file is linked via a SRC, the HTTP_REFERER is populated. However, if it's accessed through a URL it's empty! Thus a simple check of this server variable would suffice to determine if it's a linked file or direct URL access.<br >
<br >
<font color="darkgreen">
&lt;%<br >
  If Len(Request.ServerVariables("HTTP_REFERER")) &lt;&gt;0 then<br >
alert('This is an alert');&lt;%<br >
else%&gt;<br >
&nbsp;&nbsp;&nbsp;&nbsp;&lt;script type="text/javascript" xml:space="preserve" language="JavaScript"&gt;<br >
&nbsp;&nbsp;&nbsp;&nbsp;document.location = " GiveMe.htm";<br >
&nbsp;&nbsp;&nbsp;&nbsp;&lt;/script&gt;&lt;%<br >
End if%&gt;<br >
</font>
<br >
As you can see, in this example, if a URL has accessed the file, we direct the web page to a file called GiveMe.htm This file simply contains some details telling the user that the script is not available for copying!<br >
<br >
You can take this even further! By performing a simple check of contents of the http_referrer variable, to ensure that it's from your domain!<br >
<br >
So simple, I can't believe it hasn't been done before!<br >
<br >
Want to discuss the code, add comments, and even make it better? Do it <a href="http://forums.internetwideworld.com/default.asp?DefaultPage=ViewCompleteThread.asp%3FCategoryID%3D60%26ThreadID%3D20">here</a>.
<img src="http://forums.internetwideworld.com/Images/Blank.gif" width="1" height="1" alt="Weaval" />

