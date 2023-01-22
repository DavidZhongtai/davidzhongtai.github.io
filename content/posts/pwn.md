---
title: "Jenkins? More Like Jeepers!"
---

# How to Pwn a Website (Ethically)

A wonderful story of how an 18 year old was able to infiltrate a multi-million dollar company via basic techniques with a little bit of effort and why **_you shouldn't do the same_**.

So, how does it begin? After getting bored one day and browsing Shodan.io, I found some fun things. Turns out, the answer led to a 2-day bender down different rabbit holes eventually leading to this article here. So let's get started shall we?

Before we do this, I do not endorse attempting to break into company systems. This post is not a tutorial or suggestion, please act ethically. I am not liable for any damage caused by people reading this article. All of the various backdoors found along the way were **_swiftly reported to their corresponding security groups_**. Because of the nature of data accessed, the company will be referenced as `Company X`.

This story is broken into 4 parts, the setup, the exploit, the chase, and the end. Without further ado, lets dive in.

## 1. The Setup

Here, we set up the perfect setting and provide the background necessary to understand how much of this works. To provide context, the main tools used are all freely available to anyone who possesses a little bit of tech-savvy and determination. All you need is a nice web browser and a FTP server. In addition to that, we employ a overuse of the words 'essentially' and 'however' to demonstrate the various conclusions drawn from this.

#### 1.1 Jenkins[^2]

Jenkins is probably the core of how this worked. For any software oriented company, their intellectual property is usually their software and algorithms they have designed over time. Through software, it is a common practice to continue pushing out updates and new features in a timley manner. Basically, developers would test their code on a development build while new updates are pushed onto a production build. However, as time goes on, the Continuous Integration and Continous Development (CI/CD) accrues a signifigant amount of overhead for one to do manually. This is where Jenkins comes in.

Jenkins offers a simple way to set up a continuous integration and continuous delivery environment for almost any combination of languages and source code repositories. In addition to that, it can automate a number of different common developer tasks as well such as updating licenses or **access keys** (more on this later). Essentially, it takes away all of the need to have a significant DevOps team in the form of pipelines, proceesses, and scripts. One other significant feature is allowing the development team to 'run things' (i.e. tests) every time new code is committed into GitHub as well. Every developer can commit to a shared test stack and with that, each commit triggers a build task adn a test task. because of the self contained nature of Jenkins, building and testing fails can swiftly be detected and shutdown without compromising core services and creating different forms of outages.

However, because of this _self-contained nature_ of Jenkins, it needs some way of accessing code and keys for databases to test various data ingestion pipelines. This is done in the form of various AWS and Github Signing and Access keys that need to be stored _on premise_ and _inside the software_. Because of this position, Jenkins is a very attractive target for hackers.

#### 1.2 Shodan.io: The Seeing Eye

Google but for the Internet of Things (IoT). Shodan is a database of billions of publicly available IP addresses that one can scan through. Instead of searching for websites and information, it scans for anything connected to the IoT. This is anything from traffic cameras, exposed servers, smart watches, and even baby monitors. These are household items. As a matter of fact, with enough searching, one can find government systems, energy grid, infrastructure, and other critical systems as well. Essentially, **anything that is connected to the internet can be accessed online**. With it's simple to use and approachable interface, Shodan provides for a valuable tool for IT specialists to observe for publicly facing systems.

Shodan works by creating a system of randomly generated public IP addresses, pinging it, and indexing the response it recieves in return. Anything connected to the internet has a series of ports that can be accessed at certain point which allow it to transmit data through different places. There are a total of 65,535 ports in all, allowing functions from email, browsers, printers, routers; alot of things. When the system sets a port to open, it opens up this access for anyone to be able to go in without some sort of firewall or authentication system layered on top of it. For example, by setting specific ports open on your machine, it may allow a printer or scanner to communicate and send data back to your computer. When these devices transmit data back and forth, they usually send something known as a 'banner' back and forth which establishes the communication information and protocol. That is only one device. Shodan does this on a much larger scale. Essentially, Shodan works by pinging a random IP addresses, 24/7, 365, and listening for these banners. Some of the time, no information is transmitted, however, when they do return a banner, Shodan will index that banner.

```md
HTTP/1.1 200 OK
X-Content-Type-Options: nosniff
X-Hudson-Theme: default
Date: Fri, 23 Dec 2022 21:38:04 GMT
Set-Cookie:[redacted]; Path=/; HttpOnly
X-Hudson: 1.395
Server: Jetty(10.0.12)
Referrer-Policy: same-origin
X-Instance-Identity: [redacted]
Cache-Control: no-cache,no-store,must-revalidate
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Cross-Origin-Opener-Policy: same-origin
X-Jenkins: 2.375.1
X-Jenkins-Session: d936f9ba
X-Frame-Options: sameorigin
Content-Type: text/html;charset=utf-8
```

|                                     |
| :---------------------------------: |
| **An example of a response banner** |

Anything connected can be found and pinged. Everything from nuclear systems and prison payphones can be found indexed on there by previous researchers. Before you, the reader, decides to freak out and hide in a bunker in fear of total meltdown, keep in mind that these are merely _open addresses_ but does not mean they are unsecured. A majority of them contain some sort of authentication layered on top. However, one can safely assume that a majority still could be defaulted to a credential such as `admin` and `password`. What makes it even scarier is that much of the default passwords are usually published online in some form of user manual on company product sites.

#### 1.3 Wrapping Up the Setup

We covered Jenkins and Shodan.io and the basic mechanics of how they worked to scan the internet. What can you takeaway from this? The specific tools we used were Safari 16.2 (18614.3.7.1.5), Filezila 3.59.0, Shodan.io, and a little bit of clever prompting.

## 2. The Exploit

Here, we detail how we were able to find a way into different systems and how the whole process worked. Again, I cannot emphasize that this is merely for informational purposes and open access points were reported to corresponding security groups. I am **not liable for anything that happens with this information I bestow on you**

#### 2.1 Finding a Way In

Jenkins adds a signature on the browser (`X-Jenkins`) to signify that the current platform utilizes Jenkins for CI/CD. What makes this even more significant is that in most cases, it is in most cases cloud based.[^2] Now, when one hear cloud, it is usually a recipe for all of the data to be stored in some centralized location. In that case, what or where could that be stored? Spinning up Shodan, searching "X-Jenkins" will yield a plethora of exposed Jenkins servers anyone can access. However, much of them were redirects to a web-server login or a nginx 403 error in the cases of deactivated or moved servers.

![Example Shodan Interface](/shodan.png "Shodan.io")
| |
| :---------------------------------: |
| **An example of a Shodan query for Jenkins** |

But out of the ~176,000+ servers exposed, how many are without a login? By narrowing down the search query down in a fun way, I was able to narrow it down to ~2,000 servers with exposed and logged in Jenkins servers. In around 30-35 minutes, I was able to find a Jenkins server which had a pretty interesting build tree. In those previous 30-35 minutes, looking around on Jenkins would yield years old build tasks or things with meaningless names (presumably tutorials and standard Maven test builds). Usually I ignored these as they would be meaningless and didn't have much significant contribution. The one I stumbled upon was of signifigance as there was a relatively recent build tasks as both defined ios and android builds for QA. Thinking to myself, "this might actually be a project of significance."

![The Initial Discovery](/intial_censor.jpg "The Find")
| |
| :---------------------------------: |
| **The Initial Discovery** |

What was in front of me was the initial root of how things were built. However, all of it sat right in front of me: the `BUILDS` folder, obviously marked to signify its importance. Clicking on it, was the gold mine that will open up a whole realm of security breaches if not addressed properly

![The Initial Discovery](/build_censor.jpg "The Find")
| |
| :---------------------------------: |
| **The Gold Mine** |

As you can see, so far, we have encountered no resistance at all. I was not prompted for a password or 2FA mechanism, nor was I prompted with any sort of verification from the system. Because of that, this was the path of minimal resistance. At this point, I was still not confident with the results as it may be a college student's one off side project that they made. While as seen above, recent build and run dates were only mere weeks ago, it required a bit more information to confirm. So here we go, digging around again. So now, what is the worst if I actually clicked on a build? Turns out, alot. Like alot.

#### 2.2 How Much Can We Actually Access?

If you want the short answer: **alot**. If you want the long answer, I talk about the findings and implications here.

---

Here, we detail what was the exact information, things that are able to address this, and more. We left off the last section by talking about how someone was able to access builds, but sometimes, that wasn't even useful. In this case, accessing builds became extremely useful. As we mentioned previously, because of the nature of Jenkins, it needed access to the code in order to build things? Where can it find the said code though? There are mainly two ways, providing a SSH token on premise for Jenkins to use and build from automatically with every commit (which is insecure as a malicious actor can gain access to GitHub), or having Jenkins run its own copy of the code inside (which is even more insecure as the source code is stored in a centralized place that can be accessed if not secured properly). Upon clicking on one of the iOS builds and at that moment, I realized no one had enabled the action to **clear the workspace after each run**. This is a huge risk as this means the workspace can persist after subsequent runs meaning **source code remains accessible for anyone with access to Jenkins**. Not only is this an external risk for malicious actors, internal malicious actors are able to access places without authorization too. The only secure part that was worth noting is that it appeared that only the admin was able to run Jenkins actions and clear workspaces and not anyone can run that. However, at this point, it doesn't matter as someone can have unauthorized and almost **full control to a internal system**.

![The File Tree](/file_censor.jpg "The Files")
| |
| :---------------------------------: |
| **The File Tree of `Company X`** |

So at this point, my mind is racing realizing that I had stumbled upon a relatively significant breach of both company and potentially customer data. Even right now, without digging further, I was able to view **the whole company source code for both production and development**. I discuss how I reached out to people and notified them of the risk later on in Section 3. While one may comment "oh that is just some code," it is not simply _some code_, it was a company's IP. That isn't even the largest risk. Knowing that the source code has to connect somewhere to databases that store customer data and other sensitive information (DOB, credit cards, etc), without digging further, one can assume in the source code there had to lie some sort of references to databases and access tokens.

Oh wait, someone mentioned access tokens? How convenient. Usually, we as humans, really don't like memorizing 20+ characters to a password for something. Luckily, Jenkins has this _great_ feature to store all of the credentials you need to use so you never have to remember anything ever. Sounds great right? Turns out this is one of the biggest no-nos you should never make when making a secure store for credentials. Looking around, it seemed like the credential menu for Jenkins was enabled as well. Well what can we find there?

![All these Keys](/keys_censor.jpg "The Keys")
| |
| :---------------------------------: |
| **All of the Example Keys** |

Oh. Turns out we found alot, like alot alot. With this informtion and enough finesse, we can probably discover these keys and potentially breach more information. Knowing that the space was in `global` as well, it means that there are **probably** private keystores out there (giving a malicious actor a mental map of how other keys are stored). This would have not been a problem if not a few employees, by accident, added their private SSH keys inside of the global keystore by accident. At this point, it was not a technical error but more so a human error. Yummy, we have GitHub tokens now, but honestly, we can't do anything without knowing the GitHub repository location. Of course we can guess different GitHub locations, but can there be an easier way?

Good thing that Jenkins **keeps logs of all of the runs if they aren't deleted by a workspace cleanup**. But what can we get from that information? Turns out we can get the GitHub repo locations.
![Github Repo Location](/github_censor.jpg "Github Repo")
| |
| :---------------------------------: |
| **Where is the Github?** |

With this combination, we were able to see that with the SSH keys along with the location of the repo, A malicious actor could be given full access to the Github Repo and able to sign malicious code under the guise of that person as well.

Those were the most significant breaches of information that can be found. You may have noticed that there was no mention of any sort of authentication or passwords and I met no resistance to accessing it. This means I was able to cleanly glide through and access a vast amount of personal data as well. In addition to the things listed above, some of the smaller notable finds are **internal developer lists** as well as **console output from build tasks**.
![People Lists](/person_censor.jpg "People Lists")
| |
| :---------------------------------: |
| **Look at all these people** |

![Console](/console_censor.jpg "Console")
| |
| :---------------------------------: |
| **Example Console Output from Build** |

At this point, without **any verification**, I was able to compromise both production and development builds and access their source code as well as different tooling tokens, SSH keys, GitHub repository locations, internal developer lists, commit history, file paths, console logs, and probably much more. Given enough time, there could be even more information out there. What makes this even more notable is that this was done in the span of 35 minutes from opening up Shodan to finding the server and compromising it.

## 3. The Chase

Stated previously, now, I realized I had stumbled upon something huge. Now the challenge was "how do I reach out to them?" First, I wanted to confirm that this was the actual `Company X.` I dug around different code filed until I realized that all of the `.swift` files were nicely annotated by a developer called M (for privacy) which gave me my first lead.

![A Developer](/dev_censor.jpg "The Developer")
| |
| :---------------------------------: |
| **My First Lead** |

By plugging M into LinkedIn, I was quickly able to get a few matches of his work profile. In addition to that, `Company X`'s codebase had well done naming conventions meaning that it wasn't long before I was able to pinpoint the exact company it was. To do a final check, I took a few names from the developer list and recieved matches as well. That's when I know I have found the right company and started finding the right people to contact and notify, in a scene I call **the chase**.

#### 3.1 Finding the People

Thanks to the advent of the Internet, I was able to find specifically a bunch of people to try and contact. My first try was sending my only free LinkedIn InMail to the CTO of `Company X`. That was a long shot, so I tried contacting other people as well. Since so many people have online blogs and resumes online it wasn't hard to find some phone numbers and emails online and contact them. Soon after, I contacted someone I found, C, and recieved a response telling me to email them on Monday. However, this wasn't a Monday issue. After digging around, I found a person named S who was able to take action right away and put me in touch with all of the right people. Soon after, I got a reply. Bingo! At that point, I had a point of contact and began the process of doing a basic writeup. Here we are with this writeup now.

## 4. The End and Suggestions

My first foray into this area of network security and discovering this was completely unexpected. In a short span of a few hours, one is able to expose a variety of sensitive information. When I checked in the morning, I was able to see that the Jenkins server was still up but now it is behind a password wall and fixed for the time being. Wonderful! Here are some common misconfigurations an organization can look for in the future:

- The Jenkins server is wide open on the internet with all admin rights enabled for anyone who finds it
- Logins may be restricted to a Github login but was not configured for an organization. For example, Jenkins may require a GitHub login but anyone can log in since Jenkins won't check if that GitHub account belongs to the organization.
- Never storing any configuration files or passwords inside of a Jenkins environment where they can be accessed.

Well, that's all folks. Again, I cannot emphasize the importance of ethical hacking and reporting bugs whenever you find them. I am not **liable for what you do with this information**, although I strongly recommend **not doing things like this in your spare time**. Please think about your actions before acting on them.

### Contact

For any questions pertaining to this, please contact me in the contact menu up above or send me an email with a subject line pertaining to the topic.

[^2]: [Jenkins](https://www.devopsschool.com/blog/what-is-jenkins-x-and-how-jenkins-x-works/)
