+++
Categories = ["rsa", "security", "market"]
date = "2016-02-05T10:57:56-08:00"
title = "2016: Analyzing Security Trends Using RSA Exhibitor Descriptions"
+++

**The data used for this post is available [here](https://github.com/zhenjl/rsaconf). A word of warning, I only have complete data set for 2014-2016. For 2008-2013, I have what I consider to be representative samples. So please take the result set with a big bucket of salt.**

---

Continuing my [analysis from last year](http://zhen.org/blog/analyzing-security-trends-using-rsa-exhibitor-descriptions/), this post analyzes the exhibitors' descriptions from the annual security conference, [RSA 2016](http://www.rsaconference.com/events/us16). Intuitively, the vendor marketing messages should have a high degree of correlation to what customers care about, even if the messages trail the actual pain points slightly. 

Some interesting findings:

* The word _hunt_ has appeared for the first time since 2008. It only appeared 6 times and ranked pretty low, but that's a first nonetheless.
* The word _iot_ jumped 881 spots to 192 in 2016, after showing up for the first time in 2015. This may indicate the strong interest in IoT security. 
* There's no mention of _docker_ in any of the years, and only 5 mentions of container in 2016. This is a bit of a surprise given the noise docker/container is making. This is likely due to most customers care more about management for new technologies than security.
* The word _firewall_ dropped 151 spots in 2016. I want to speculate that it is due to the dissolving of perimeters, but I can't be sure of that.
* As much as noise as _blockchain_ is making, there's no mention of the word.
* The word _behavior_ (as in behavioral analysis) has also gained drastically over the past few years, going from #370 in 2012 to #78 in 2016.
* See other findings below.

### Top Words

The top words that vendors use to describe themselves haven't changed much. The following table shows the top 10 words used in RSA conference exhibitor descriptions since 2008. You can find the complete word list [here](https://github.com/zhenjl/rsaconf).

| # | 2008 | 2009 | 2010 | 2011 | 2012 | 2013 | 2014 | 2015 | 2016 |
| ---: | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 1 | secure | secure | secure | secure | secure | secure | secure | secure | secure |
| 2 | solution | solution | solution | solution | solution | solution | solution | solution | solution |
| 3 | network | manage | manage | network | provide | provide | provide | provide | provide |
| 4 | provide | provide | network | provide | manage | manage | network | data | data | 
| 5 | manage | data | protect | manage | network | service | manage | network | threat |
| 6 | enterprise | network | provide | data | information | more | data | protect | network |
| 7 | data | company | data | information | software | software | protect | threat | protect |
| 8 | product | service | organization | enterprise | enterprise | information | threat | manage | manage |
| 9 | technology | software | information | technology | data | enterprise | service | service | enterprise |
| 10 | application | busy | risk | product | more | customer | enterprise | enterprise | service |

Here's a word cloud that shows the [2016](/images/rsaconf/rsa2016.png) top words. You can also find word clouds for 
[2008](/images/rsaconf/rsa2008.png),
[2009](/images/rsaconf/rsa2009.png),
[2010](/images/rsaconf/rsa2010.png),
[2011](/images/rsaconf/rsa2011.png),
[2012](/images/rsaconf/rsa2012.png),
[2013](/images/rsaconf/rsa2013.png),
[2014](/images/rsaconf/rsa2014.png),
[2015](/images/rsaconf/rsa2015.png).

<img src="/images/rsaconf/rsa2016.png">

### Endpoint vs. Network

While the word _network_ has mostly maintained its top 10 position (except 2013 when it fell to #11), the big gainer is the word _endpoint_, which improved drastically from #266 in 2012 to 2016's #50. This may indicate that enterprises are much more accepting of endpoint technologies. 

I also speculate that there might be a correlation between the increase in _cloud_ and the increase in _endpoint_. As the perimeters get dissolved due to the move to cloud, it's much more difficult to use network security technologies. So enterprises are looking at _endpoint_ technologies to secure their critical assets.

<img src="/images/rsaconf/2016/endpoint-network.png">

### Compliance vs. Threat

Not surprisingly, the use of the word _compliance_ continues to go down, and the word _threat_ continues to go up. 

The number of mentions for _threat intelligence_ remained at 22 for both 2015 and 2016, after jumping from 12 in 2014.

<img src="/images/rsaconf/2016/compliance-threat.png">

### Mobile, Cloud, Virtual and IoT

While the words _mobile_ and _cloud_ maintained their relative positioning in 2016, we can also see _virtual_ continues its slight downward trend.

Interestingly, the word _iot_ made a big jump, going from position #1073 in 2015 to #193 in 2016. This potentially indicates a strong interest in security for internet of things. In general, the IoT space has seen some major activities, including [Cisco's recent acquisition of Jasper](http://techcrunch.com/2016/02/03/cisco-buys-jasper-technologies-for-1-4-billion/).

<img src="/images/rsaconf/2016/mobile-cloud.png">

### Cyber, Malware and Phishing

The word _cyber_ continues to gain popularity in the past 4 years; however, the word _malware_ has fell below the top 100, a position it maintained since 2010.

The word _phishing_ made drastic gains since 2014, jumping from #807 to #193 in 2016. This may indicate that enterprises are seeing more attacks from phishing, and vendors are targeting that specific attack vector.

<img src="/images/rsaconf/2016/cyber-malware.png">

### It's all about Behavior!

The word _behavior_ (as in behavioral analysis) has also gained drastically over the past few years, going from #370 in 2012 to #78 in 2016.

<img src="/images/rsaconf/2016/behavior.png">

### Credits

* The word clouds and word rankings are generated using [Word Cloud](http://timdream.org/wordcloud).
* The actual vendor descriptions are gathered from the RSA web site as well as press releases from Business Wire and others.
* Charts are generated using Excel, which continues to be one of the best friends for data analysts (not that I consider myself one).