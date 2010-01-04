---
layout: post
title: OSGi - Still Waiting for Magnum
---

I got a love and hate relationship with <a href="http://www.osgi.org/">OSGi</a>. On one hand, I think that its a great spec that provides amazing capabilities of modularization within the JVM. On the other hand, its a monstrosity, that in order to use it, you need to heavily lubricant your MANIFEST file, since you know where its going to end up at. Before you jump up and replace that MANIFEST with something else and apply it to me, let me make my point.

I just watched the wonderful <a href="http://www.imdb.com/title/tt0196229/">Zoolander</a> movie, and in the movie, everybody waits for Zoolander to reveal his Magnum face.  At the end, Zoolander manages to find his Magnum face, with OSGi, I am still waiting for it to happen.

We at Javaland somehow always manage to make things much more complex before we realize that and work very hard in order to simplify them (JSF anyone?). The same goes with OSGi. In 95% of the applications, I don't really need OSGi. Most applications can live happily with the current deployment model (each web application in its own class loader, versioning done on a per web app level).

Worst yet, in order to separate my web application into several modules, I need to either work really hard (Import / Export), or rely on tooling. Personally, I hate to work hard, and hate even more to rely on tooling (websfear anyone?). Take for example <a href="http://www.springsource.org/dmserver">Spring dm server</a>, while a novel concept and an amazing technical achievement, in practicality it just makes my life more complex for 99% of my typical applications. Sure, it can deploy "plain" war file, which is great, but then am I not just better off with plain Tomcat? I guess that this exact reasoning were behind the upcoming <a href="http://www.springsource.com/node/897">Spring tc server</a>.

Sure, application servers, or Eclipse for example, can use OSGi to their heart content, but the best thing about it is that they hide almost completely the fact that OSGi is used. Either through tooling for Eclipse (which, in case of Eclipse, that is actually ok, since I develop plugins for Eclipse), or by supporting plain web applications with application server. Another great example is Terracotta TIMs, sure, they use OSGi, but who the frack cares? (personally, I think it was an overkill, but as long as I, as an integration module developer don't know it, I don't really care).

From an architectural standpoint, by the way, I strongly believe that the need for modularity within the same VM is almost never needed. Personally, I will almost never create a DAO module, and Service module, since most times I will roll an upgrade that changes the whole application. Most times when it is needed, you are usually better off with abstracting the module behind a REST AP.

The main case where you do need it, IMO, is when working in a collocated architecture. In such cases, modules do need to reside within the same VM and share another "heavy" collocated module (such as a data grid node/partition). In such cases, a very simple dependency tree (easily achieved with  class loader hierarchy) can be created, with the common collocated module at its base. This is, by the way, why I like the <a href="http://jcp.org/en/jsr/detail?id=277">Java Module System</a> JSR, its much simpler than OSGi and focus on modularity and nothing else.

I am not saying that modularity within the VM is not needed. I just want the following things: When it is not needed, I want things to remain the same. And when it is needed, pretty please, with sugar on top, keep it simple. No tooling and no 300 lines MANIFEST files please.