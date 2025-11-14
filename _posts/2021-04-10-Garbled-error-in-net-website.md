
Have you ever seen this?

![custom domain](/img/2021-04-10-garbled-error-in-net-website/garbled.png)

Where to start? It happens because modern browsers can handle compression sent from webservers. So what you are seeing is a compressed result of an error. If you use IE11, then you will see the actual error. So what can be done to allow debugging?

Well the fix is simple – it you know what to do. Just locate your Global.ascx file and update the Application_Error method.

void Application_Error(object sender, EventArgs e) {
   if (HttpContext.Current.IsDebuggingEnabled) Response.Filter = null;
}


By setting the Response.Filter to null while debugging, we are removing crompression from the output. This would also be the place where you may want to log any errors in your website too. But this article covers a quick fix to display on screen errors while developing. The garbbled characters then becomes magically legible.


![custom domain](/img/2021-04-10-garbled-error-in-net-website/error.png)


This… I understand!


