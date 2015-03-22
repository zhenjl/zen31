+++
Categories = ["rsa", "security", "market"]
date = "2015-03-22T09:57:56-08:00"
title = "Analyzing Security Trends Using RSA Exhibitor Descriptions"
+++

**The data used for this post is available [here](https://github.com/topclouds/rsaconf). A word of warning, I only have complete data set for 2014 and 2015. For 2008-2013, I have what I consider to be representative samples. So please take the result set with a big bucket of salt.**

---

After going through this analysis, the big question I wonder out loud is: 

> _How can vendors differentiate from each other and stand above the crowd when everyone is using the same words to describe themselves?_

---

The annual security conference, [RSA 2015](http://www.rsaconference.com/events/us15), is right around the corner. Close to 30,000 attendees will descend into [San Francisco Moscone Center](http://moscone.com) to attend 400+ sessions, listen to 600+ speakers and talk to close to 600 vendors and exhibitors.

For me, the most interesting aspect of RSA is walking the expo floor, and listening to how vendors describe their products. Intuitively, the vendor marketing messages should have a high degree of correlation to what customers care about, even if the messages trail the actual pain points slightly. 

This post highlights some of the unsurprising findings from analyzing 8 years worth of RSA Conference exihibitor descriptions. 

It is interesting how almost all vendor descriptions use the same set of words to describe themselves, and these words mostly haven't changed over the past 8 years. For example, the following table shows the top 10 words used in RSA conference exhibitor descriptions for the past 8 years. You can find the complete word list at ...

| # | 2008 | 2009 | 2010 | 2011 | 2012 | 2013 | 2014 | 2015 |
| ---: | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 1 | secure | secure | secure | secure | secure | secure | secure | secure |
| 2 | solution | solution | solution | solution | solution | solution | solution | solution |
| 3 | network | manage | manage | network | provide | provide | provide | provide |
| 4 | provide | provide | network | provide | manage | manage | network | data |
| 5 | manage | data | protect | manage | network | service | manage | network |
| 6 | enterprise | network | provide | data | information | more | data | protect |
| 7 | data | company | data | information | software | software | protect | threat |
| 8 | product | service | organization | enterprise | enterprise | information | threat | manage |
| 9 | technology | software | information | technology | data | enterprise | service | service |
| 10 | application | busy | risk | product | more | customer | enterprise | enterprise |

Here's a word cloud that shows the [2015](https://github.com/topclouds/rsaconf/blob/master/rsa2015.png) top words. You can also find word clouds for 
[2008](https://github.com/topclouds/rsaconf/blob/master/rsa2008.png), 
[2009](https://github.com/topclouds/rsaconf/blob/master/rsa2009.png), 
[2010](https://github.com/topclouds/rsaconf/blob/master/rsa2010.png), 
[2011](https://github.com/topclouds/rsaconf/blob/master/rsa2011.png), 
[2012](https://github.com/topclouds/rsaconf/blob/master/rsa2012.png), 
[2013](https://github.com/topclouds/rsaconf/blob/master/rsa2013.png), 
[2014](https://github.com/topclouds/rsaconf/blob/master/rsa2014.png).

<img src="/images/rsaconf/rsa2015.png">


### Compliance Down, Threats Up

While the macro trend has not changed dramatically for the exhibitor descriptions, there have been some micro trends. Here are a couple of examples. 

First, the use of the word _compliance_ has gone down over the years, while the word _threat_ has gone up. After 2013, they changed places with each other. 

This finding is probably not surprising. At the end of 2013, one of the biggest breaches, Target, happened. And over the next two years we've seen major breaches of Sony, Anthem, Home Depot, Premera and many others. Threats to both the corporate infrastructure as well as top executive jobs (just ask [Target’s CEO Gregg Steinhafel](http://www.forbes.com/sites/ericbasu/2014/06/15/target-ceo-fired-can-you-be-fired-if-your-company-is-hacked/), or [Sony's Co-Chairwoman Amy Pascal](http://abcnews.go.com/Entertainment/wireStory/sony-chief-amy-pascal-acknowledges-fired-28918607)) are becoming real. So it seems natural for the marketers to start using the word _threat_ to highlight their solutions.

_Compliance_ was a big use case in security for many years, and many vendors have leveraged the need for compliance to build their company and revenue pipeline since the mid-2000s. However, use cases can only remain in fashion for so long before customers get sick of hearing about them, and vendors need new ways of selling their wares to customers. So it looks like _compliance_ is finally out of fashion around 2011 and started declining in exhibitor descriptions.

<img src="/images/rsaconf/compliance-threat.png">

### Mobile and Cloud Up

The words _mobile_ and _cloud_ has gained dramatically in rankings over past 8 years. In fact, it's been consistently one of the top words used in the last 4. For anyone who hasn't been hiding under a rock in the past few years, this is completely unsurprising. 

The _cloud_ war started to heat up back in 2009 when most major service providers have felt the Amazon Web Services threat and all wanted to build their own clouds. In fact, I joined VMware in 2009 to build out their emerging cloud infrastructure group to specifically help service providers build their cloud infrastructures. Eventually, in 2011, VMware decided to get into the game and I built the initial product and engineering team that developed what it's now known as vCloud Air (still have no idea why this name is chosen). 

As more and more workloads move to the cloud, requirements for protecting cloud workloads quickly appeared, and vendors natually started to position their products for the cloud. So the rise in _cloud_ rankings matches what I've experiened.

About the same time (2010, 2011 or so), more and more corporations are providing their employees smartphones, and workers are becoming more and more mobile. The need for mobile security became a major requirement, and a whole slueth of mobile security startup came into the scene. So natually the _mobile_ word rose in rankings.

<img src="/images/rsaconf/mobile-cloud.png">


### Virtual and Real-Time Regaining Ground

The words _virtual_ and _real-time_ dropped dramatically in rankings for a couple of years (2010, 2011) but have since regained all the lost ground and more. I have no precise reasons on why that's the case but I have some theories. These theories are probably completely wrong, and if you have better explanations I would love to hear from you.

* _Virtual_ lost to _cloud_ during that timeframe as every vendor is trying to position their products for the cloud era. However, _virtual_ infrastructures haven't gone away and in fact continue to experience strong growth. So in the past couple of years, marketers are covering their basis and starting to message both _virtual_ and _cloud_.
* The drop in rankings for _real-time_ is potentially due to the peak of _compliance_ use case, which is usually report-based and does not have _real-time_ requirements. Also, I suspect another reason is that SIEM, which _real-time_ is critical, is going out of fashion somewhat due to the high cost of ownership and lack of trust in the tools. However, given the recent rise of _threats_, natually _real-time_ becomes critical again.

<img src="/images/rsaconf/virtual-real-time.png">

### Other Findings

The word _cyber_ gained huge popularity in the past 3 years, likely due to the U.S. government's focus on _cyber_ security. The word _malware_ has been fairly consistently at the top 100 words since 2010.

<img src="/images/rsaconf/cyber-malware.png">

The words _product_ and _service_ switched places in 2013, likely due to the increase in number of security software-as-a-service plays.

<img src="/images/rsaconf/product-service.png">

### Credits

* The word clouds and word rankings are generated using [Word Cloud](http://timdream.org/wordcloud).
* The actual vendor descriptions are gathered from the RSA web site as well as press releases from Business Wire and others.
* Charts are generated using Excel, which continues to be one of the best friends for data analysts (not that I consider myself one).