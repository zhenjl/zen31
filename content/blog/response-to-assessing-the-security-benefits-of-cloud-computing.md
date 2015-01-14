+++
Categories = ["cloud", "security"]
date = "2008-08-28T01:58:22+00:00"
title = "Response to \"Assessing the Security Benefits of Cloud Computing\""
+++


Craig Balding from [Cloud Security](http://cloudsecurity.org) wrote an interesting piece on the [security benefits of cloud computing](http://cloudsecurity.org/2008/07/21/assessing-the-security-benefits-of-cloud-computing/) back in July (that I just now got to read.) Craig qualified the post as **potential security benefits** of Cloud Computing.

After reading through it, I felt compelled to respond, even though it's a been over a month since the post is up. Craig mentioned he won't talk about the "flip" side of these benefits in this post, so I figure I will do that. :)
I have only quoted the headers from Craig's article so please refer to the [original article](http://cloudsecurity.org/2008/07/21/assessing-the-security-benefits-of-cloud-computing/) for all the details.

Overall, Craig has made a good list of potential benefits. However, we really need to distinguish the benefits of virtualization vs cloud computing. Many of the benefits listed here are really benefits of virtualization and not cloud computing. When I read the title, I was hoping to read about how the cloud could be more secure than enterprise environments. I think this list has a mix of that, and how enterprise could use the cloud for some security use cases. That's fine but mixing them together can be misleading.



### 1. Centralised Data



**Reduced Data Leakage** 

As Craig said, "this is the benefit I hear most from Cloud providers". Unfortunately I have to disagree with Craig here. In my view, the cloud providers are dead wrong about this one. Many of the cloud providers talk about how laptops or backup tapes being stolen as the biggest threat to data leakage, and they are right about that. However, having enterprise data stored in the cloud doesn't reduce these risks one bit. Travelers will continue to copy data to their laptops as they need to access them while on the road. Old habits die hard. Enterprises will continue to backup data to tapes because they can't simply reply on cloud providers to backup their data. These will still happen no matter where the data is stored. 

In fact, there likely will be an increased chance of data leakage by using cloud computing because now the cloud providers will have to somehow backup their data (maybe on tape!!) 



**Monitoring benefits**

Most enterprises, probably including the one Craig works for, have centralized file servers, content management systems, etc etc. However, we continue to see problems with data leakage. Having data stored in clouds is not all that different than storing on centralized corporate file servers. Centralized storage and monitoring is not an advantage for clouds. Enterprises had centralized storage/archiving solutions for years. 

In my opinion, cloud storage makes it even tougher to monitor data leakage. Think about the tools available to monitor enterprise file servers. Many of them monitors all types of access: read, write, via CIFS/NFS/etc, via local system. How do you do all of that in the cloud? Think S3, the only thing S3 provide you are http access logs. You have no way of knowing who else viewed your files if it's done locally, for example.





### 2. Incident Response / Forensics




**Forensic readiness**

To a certain extent this benefits is real. However, it's not a cloud-only benefit. You get the same benefit by simply doing virtualization on your infrastructure. VMware allows you to easily clone an image so that you can perform whatever analysis is needed on the image instead of the original virtual machine. Same as Xen.

However, think about the cases where forensics require physical hard disk scan in case the attacker has "rm" the "bad stuff" such as audit trails or root kit. You now have NO WAY of getting to that in a virtualized environment. Granted, this is probably an issue with any network/san attached storage.


**Decrease evidence acquisition time**

Same as above, it's not a cloud-exclusive benefit. It's simply a benefit of virtualization. The only real benefit of the cloud, as mentioned by Craig, is not having to "find" storage. Though I would say that's the least of your worries if there's a real attack that happened.


**Eliminate or reduce service downtime**

First, if the server/VM is truly "0wn3d", I am not sure you want to keep that system up and running. You may want to bring a good copy of the VM up and run that instead. (or just go back to a previous good snapshot.)

Second, with the cloud, you don't even have a CHOICE of using physical acquisition toolkit. So I am not so sure that's a benefit. :)


**Decrease evidence transfer time**

Again, not a real benefit of the cloud. First, bit-by-bit copies of the VM in the cloud still takes time just like if you would in the real world. Second, this benefit can also be realized as part of the internal VM infrastructure, not cloud-exclusive.

**Eliminate forensic image verification time**

Ok, so this is a minor benefit, but not a security benefit of the cloud. It's more about the performance and scalability of the cloud.

**Decrease time to access protected documents**

Both this and the next benefit are really about the elasticity and scalability of the clouds and not security. 


### 3. Password assurance testing (aka cracking)



**Decrease password cracking time**

Same as above, this is about the benefits of elasticity and scalability, not security.

**Keep cracking activities to dedicated machines**

Same as above, this is about the benefits of elasticity and scalability, not security.


### 4. Logging



* **‘Unlimited’, pay per drink storage**
* **Improve log indexing and search**
* **Getting compliant with Extended logging**



Ok, this is about the utility and scalability of the cloud. Not a cloud security benefit. It's about using the cloud for security tasks.



### 5. Improve the state of security software (performance)


**Drive vendors to create more efficient security software**

I believe this is true for even software on dedicated machines. Not cloud-exclusive.


### 6. Secure builds


**Pre-hardened, change control builds**

This I agree with. Having pre-built images that are secure from the start is a HUGE benefit. Though it's a benefit of virtualization and virtual machines, not cloud-exclusive.

**Reduce exposure through patching offline**

I don't understand this one. Once the VM is running in production, I can imagine taking that down to do patching. You would have to manage the patching process like any other machine, no? 

Now image templates can be updated with patches so if new machines are started, they are pre-patched.

**Easier to test impact of security changes**

Again I agree. However, it's still the benefit of virtualization, not necessarily cloud-exclusive.


### 7. Security Testing




**Reduce cost of testing security: **

Agreed. It's a side benefit of economies of scale.



