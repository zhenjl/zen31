+++
Categories = ["log"]
date = "2004-12-28T23:00:54+00:00"
title = "War on Intellectual Property Leakage"
+++


Approximately sixty to eighty percent of your company's asset is defined as Intellectual Properties, or IP.

IP includes everything from patents, trademarks, brands, trade secrets, designs, architectures, copyrights, algorithms, software code, hardware schematics, inventions, business processes, and many other intangible assets. These are properties that may or may not have no physical presence. They exist mostly in the digital world or people's minds. 

A study by PricewaterhouseCoopers, the U.S. Chamber of Commerce, and the American Society for Industrial Security International estimated that American companies lost up to $59 billion in intellectual property and proprietary information between July 2000 and June 2001. The largest average dollar value of loss per incident occurred in research and development ($404,000), followed by financial data ($356,000). 

Probably not surprising to information security professionals, most of the IP leakage incidents involve insiders. Insiders are generally considered "trusted" users who have access to the internal network, whether they are connected on the internal LAN or through VPNs. The insiders can be current and former employees, contractors or business partners.

Any one of these employees, contractors or business partners could be dissatisfied for whatever reason and decide to send a few design specs to the competitors. Once the secret is out, it is extremely difficult to contain it. The cost of IP litigation, if you choose to go that route, can cost from several hundred thousand dollars to several million dollars. This amount doesn't even include the cost due to loss of reputation, brand, speed to market and other factors.

So how does a company go about securing their intellectual properties and make sure access to the IPs are tracked?



### Enterprise Content Management



The first class of companies who attacked this problem is the Enterprise Content Management (ECM) vendors such as FileNet, Documentum, Interwoven, Open Text, Stellent and Vignette. These vendors generally provide centralized document management capabilities that allow users to 




  * Organize and classify electronic documents


  * Search documents using keywords


  * Share documents with other users


  * Check-in and check-out documents for edit


  * Version control for all documents


  * Audit all access to documents



The main solution to the IP leakage problem by these vendors is all access to electronic documents are recorded and reported. These products will help manage and track documents when it's stored centrally on the server. They can track who has accessed which file at what time. How many times files are accessed and how often people access these files. 

Some of the more sophisticated products can also tell you the access behavior by individual users. For example, if a user who doesn't normally access a certain section of the repository all the sudden starts to download all the files in that section, something suspicious may be going on and should be alerted.

But what happens when the file has been downloaded to the user's desktop? Once that happens, these products can no longer protect or track the documents. What happens if the user emails the file via Yahoo Mail or Gmail? What happens if the user uploads the file to another server using FTP or HTTP? What happens if the user copies it to an USB drive or prints it out? 



### IP Leakage Detection



A whole new class of companies, including Vericept, Vidius, and Vontu, has been founded to detect IP leakage on the network. These companies' products are designed to detected IP leakage by monitoring all the exit points in which information can leave the corporate network. 

In general, when users intentionally or unintentionally leak intellectual properties, they will probably




  * E-mail the documents as attachments


  * Upload the documents to another server via FTP or HTTP


  * IM another user



All unencrypted traffic on the network can be sniffed out by package sniffers and have the content be examined. This is essentially what some of the products are doing. Most of the products in this category are basically re-purposing technologies from the IDS and content filtering world. These products will captures the contents from either the network or email stream; examine the content by either performing a keyword or regular expression search; and alert the administrators if any matches occur.

The detection mechanisms in these products are not unlike signature-based IDS. They also suffer the same high false positive rate problems as the IDS products. You will also need to spend quite a bit of time tuning and maintaining the products in order for it to accurately detect IP leakage.

However, some vendors, such as Vericept, claims to have additional technology that performs statistical or linguistic analysis on the content and are able to detect leakage much more accurately and efficiently.



### IP Leakage Control



One major problem that the network-based detection products cannot solve is sneakerware leakage. Sneakerware leakage includes scenarios where the user copies the file onto removable media such as CDs, USB drives and floppies, or the user prints the documents out. The user can then carry these removable medias or printouts with them and no one will notice.

Another class of companies, including Verdasys, Liquid Machine, Authentica, and AegisDRM, are attacking the IP leakage problem a different perspective. They have designed agents that run on users' desktops and track all user actions including opening and printing files, copying files to removable media, and sending files across the network. These products allow users to define Acceptable Use Policies, monitors all actions performed, and prevent or alert when a violation occurs. This class of companies is generally categorized as Digital Rights Management vendors.

In general, however, these products cannot detect whether a document contains confidential information. Administrators or users must explicitly mark documents as either confidential and should be protected, or not confidential. Administrators can also set up policies to globally disallow copying to removable medias, or file sharing via P2P networks.



### The Future



What's in the future in fighting against IP leakage? 

As storage and security solutions are merging, as evidenced by the Symantec and Veritas marriage, we can expect comprehensive solutions that will integrate all of the above components. We can expect products that 




  * Have centralized enterprise contents management capabilities


  * Have components that can monitor network exit points and match the outbound content with the central repository


  * Have agents that can monitor user activities



These three components will talk to each other to more accurately detect and prevent intellectual property leakage.

We will also probably see many of the pure play vendors in these three areas (ECM, DRM, IP Leakage Detection) be bought up by some of the bigger vendors such as Symantec and EMC/Documentum.
