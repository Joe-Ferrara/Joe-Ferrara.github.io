---
layout: post
title: "What's a Website"
sub: "none"

---

This post is about what a website<sup>[1](#1)</sup> is from the perspective of how the internet works. For a long time I thought a webpage was an html file, and a website a collection of html files in a directory structure. I had never considered further what's going on when one visits a website. Now I know that when I visits a website, the website is running (aka hosted) on a computer that I'm connecting to through the internet. On the computer that is hosting the website, a program is running which renders that html file for my viewing pleasure. That's a high level description, and I'll get into a little more detail. But first a story about where my thinking that a website is nothing more than a rendered html files came from.

It was my first time meeting the other post docs in the math department at UC San Diego, and I had just set up my personal website at [math.ucsd.edu/~jferrara](https://math.ucsd.edu/~jferrara)<sup>[2](#2)</sup>. When you're associated with a University in a teaching or research role you're given a website, usually at a domain like `department.university.edu/~email_address`. To set up your website, you get a login and password to ssh into a server that's run by the university. When you ssh in, there's some standard directory structure that I forget, where one of the directories corresponds to your webpage. Throw some html into that directory, in particular `index.hrml` in the top level, and that html is rendered at the domain associated with your email address. I had just made my website by typing up this html file

```html
<!DOCTYPE html>
<html>
<head>
  <title>Joe Ferrara's Web Page</title>
<style>
a:link {color:#0000FF;text-decoration:none;}    /* unvisited link */
a:visited {color:#0000FF;text-decoration:none;} /* visited link */
a:hover {color:#0000FF;text-decoration:underline;}
</style>
</head>
<body>


<div id="content" style="font-size:30px; width:800px; margin:0px auto;">Joe Ferrara</div>
<div id="content" style="width:800px; margin:0px auto;"> Postdoctoral Fellow <br/>
	Department of Mathematics <br/>
	UC San Diego <br/>
	<br/>
	<b>email: </b>jferrara (at) ucsd (dot) edu <br/>
	<b>office: </b>AP&M 6321 <br/>
</div>
<br/>

<div id="content" style="font-size:20px; width:800px; margin:0px auto;"><b>Research</b></div>
<br>
<div id="content" style="width:800px; margin:0px auto;">I'm interested in special value formulas for L-functions with an emphasis on Stark's conjectures. I completed my PhD under the supervision of Professor Samit Dasgupta at UC Santa Cruz in Spring 2018. </div>
<br/>

<div id="content" style="font-size:20px; width:800px; margin:0px auto;"><b>Papers</b></div>
<div id="content" style="width:800px; margin:0px auto;">
    <ul>
    <li><i>A p-adic Stark conjecture in the rank one setting</i>, accepted to appear in Acta Arithmetica (<a href="pAdicStarkRankOne.pdf">pdf</a>, <a href=
"https://arxiv.org/abs/1904.10561#">arXiv</a>)
    </li>
    <br>
    <li><i>Stark's Conjectures for p-adic L-functions</i>, PhD Thesis, UC Santa Cruz (<a href="Thesis.pdf">pdf</a>)
    </li>
</div>

<div id="content" style="font-size:20px; width:800px; margin:0px auto;"><b>Code</b></div>
<div id="content" style="width:800px; margin:0px auto;">
    <ul>
    <li>The code used to compute the examples in my thesis and in <i>A p-adic Stark conjecture in the rank one setting</i> can be found on GitHub: <a href="https://github.com/Joe-Ferrara/p-adicStarkExamples">https://github.com/Joe-Ferrara/p-adicStarkExamples</a>.
    </li>
</div>



<div id="content" style="width:800px; margin:0px auto; font-size:20px;"><b>Teaching</b></div>
</div>

<div id="content" style="width:800px; margin:0px auto;">
  Summer 2017 (at UC Santa Cruz): <a href="111ASum17/">Math 111A</a>
</div>

</body>
</html>
```

I was very proud of myself having figured out how to write this html. While I was standing with the other postdocs in the entryway to the math department building waiting for a few other people to go to lunch, I told a few of the postdocs that I'd set up my personal website and asked if they had done the same. When they replied yes, I asked "Did you learn how to code html?"<sup>[3](#3)</sup> I wanted to brag about my new found html skills and that I knew how to ssh into the UCSD server to set  up my website. One of the other postdocs looked at my like I was a fool, and replied "What do you mean, learned how to code in html? I made a couple html files for website, but I wouldn't call that coding in html." Myself, super embarrassed, as people usually are when they want to brag about something they learned and someone else trivializes it, laughed it off and changed the subject.<sup>[4](#4)</sup>

I was obviously naïve, thinking that a website is just a bunch of html files. Of course a website can be just a bunch of html files, which was the case for the website I had made, but there can also be much more going on at a website. I still have the full set up files for my UCSD website, which I've put in this github repo [https://github.com/Joe-Ferrara/my-ucsd-website](https://github.com/Joe-Ferrara/my-ucsd-website). If you download the files in that repository then in the file explorer on your computer, you can click on the `index.html`  file in the top level folder. Usually what will happen if you do that is that your web browser will open up and render the html file. You can then click around and that html file along with others in the folder will make it seem as if you're interacting with a real website.

When you visit a real website though there is more going on - a program is running on the computer that is hosting the website. To host my UCSD website on your computer, you can run the command `python -m http.server` in the top level of the repository. This will work  if Python 3 is installed on your system and the `python` command corresponds to Python 3. Running this command starts a program that hosts the website on port `8000` of your computer.<sup>[5](#5)</sup> To see the website, visit `http://localhost:8000/` in a web browser. The word `localhost` means it's being hosted on your computer. Just like when you clicked the `index.html` file from your file explorer, you can interact with the website. If you interact with the website by clicking around the pages via links, you can see in the logs in the terminal where `python -m http.server` is running that showing that every time you click a link to go to a new page, the program does something to show that page in the web browser.

Even though in this case you are hosting the website on your computer, other people cannot actually visit the website. This has something to do with the fact that you're hosting the website on a personal computer that's accessing the internet through your internet service provider. There are built in guardrails in place that prevent other random people from connecting to your computer and viewing things hosted on your computer. I don't fully understand what the deal is to be honest. It has been a confusing point to me that on the one hand a website is just a program running on a computer that you can access through the internet, while at the same time, it's difficult (or at least non-trivial) for me to host a website on my computer that others could access.

Let's say we wanted to make a website though that everyone could access. We'd need:

1. The html files for the website, which we can use my UCSD html files as a source for.  
2. A computer to run `python -m http.server` on.
3. A domain for people to visit.
4. The proper set up such that people can actually connect to the computer that's running `python -m http.server` and view the website.

As I said before I do not really understand the details of 4., but I can say a bit more about 1., 2., and 3. A standard way to do this is to get an AWS account and turn on a cheap ec2 instance to host the website. An ec2 instance is just a computer - it's a computer you can use to host your website. We'd turn on the ec2 instance, ssh into it, get the files for the website onto the ec2 instance, by cloning the UCSD website repo for instance, and then run `python -m http.server` in the correct folder of the ec2 instance. Then we do some magic to allow any person to connect to the ec2 instance.

The way people connect to the ec2 instance to see the website is by using the ec2 instance's IP address. Every computer connected to the internet has an IP address. An IP address is a string of numbers 4 numbers with dots between them, which looks like `x.x.x.x`. If you do the magic to make the ec2 instance accessible to anyone over the internet, then that means that people can visit a website hosted by the ec2 instance by visiting the instance's public IP address. For example, if you're running `python m http.server`, then people could view the hosted website by visiting `http://x.x.x.x:8000/` where `x.x.x.x` is the IP address of the ec2 instance. People do not want to remember some random IP address for your website though, so you by a domain name like mycoolwebsite.com to host your website and there's a standard process for pointing the domain name mycoolwebsite.com to the IP address and port where you are running your website.

Interestingly, we can almost see what's going on with the UCSD math department websites. The domain that hosted my UCSD website still actually works (as of 8/20/2023). If you go to [https://math.ucsd.edu/~jferrara](https://math.ucsd.edu/~jferrara) then it redirects to the website [https://mathweb.ucsd.edu/~jferrara/](https://mathweb.ucsd.edu/~jferrara/), so you're really viewing the website https://mathweb.ucsd.edu/~jferrara/. If you then go to the website [https://mathweb.ucsd.edu](https://mathweb.ucsd.edu), you get sent to a weird page that people probably are not supposed to visit with the source html:

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<html>
 <head>
  <title>Index of /</title>
 </head>
 <body>
<h1>Index of /</h1>
  <table>
   <tr><th valign="top"><img src="/icons/blank.gif" alt="[ICO]"></th><th><a href="?C=N;O=D">Name</a></th><th><a href="?C=M;O=A">Last modified</a></th><th><a href="?C=S;O=A">Size</a></th><th><a href="?C=D;O=A">Description</a></th></tr>
   <tr><th colspan="5"><hr></th></tr>
   <tr><th colspan="5"><hr></th></tr>
</table>
<address>Apache/2.4.54 (Ubuntu) Server at mathweb.ucsd.edu Port 443</address>
</body></html>
```

The interesting thing about this website is that the website says "Apache/2.4.54 (Ubuntu) Server at mathweb.ucsd.edu Port 443", which seems to indicate that the mathweb.ucsd.edu website is being hosted on port 443 of a server (i.e. a computer) that has the Ubuntu operating system.

<a name="1"><sup>1</sup></a> More accurately this post is about what a *static* website is, but I do not want to get into the difference between a static website and a non-static website, so whenever I say website in this post, you could say that I am technically referring to a static website more than a general website.

<a name="2"><sup>2</sup></a> Surprisingly, at the time of writing this, that url still shows my old website (after a redirect to mathweb.ucsd.edu/~jferrara/) even though I have not been associated with UC San Diego since June 2020. 

<a name="3"><sup>3</sup></a> Cringe.

<a name="4"><sup>4</sup></a> The story also illustrates a point of programming or computer stuff in general - that you can do stuff and have no idea what you're doing. I could ssh into he UCSD server and set up a static website of html files without having any understanding of what it means to ssh into a server or any understanding of how a website actually works.

<a name="5"><sup>5</sup></a> I'd like to, but can't really get into what a port is. I can google it or you can google it to understand what it is better. The extent to which I think about what a port is, is that in the address `http://localhost:8000`, the `localhost` part specifies the computer running the program and the `:8000` part specifies where specifically on the computer the program hosting the website is running. This allows one to isolate exactly what's running the program and illustrates that a computer can do different things at once. While hosting a website on one port it can also be doing other things.
