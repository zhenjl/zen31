+++
Categories = ["log"]
date = "2004-11-04T03:06:54+00:00"
title = "Five Business Mistakes of Log Analysis"
+++

Aside from the technical or operational mistakes mentioned in this [article](http://www.computerworld.com/securitytopics/security/story/0,10801,96587,00.html?SKC=security-96587), there are also business mistakes that organizations can make in their implementation of the log analysis infrastructure/product.

Below are five common mistakes that are commonly seen in organizations.



### 1. Lack of clear understanding of the values



Return on Investment (ROI) is usually a metric organizations use to justify any capital investments. Most SIM vendors have one, and they usually use it to help the buyers in the organizations to justify the investment to the upper management. Most ROI are centered around four different areas: revenue, cost, asset and risk.

Unfortunately, most of the metrics around SIM products are "fuzzy" metrics, i.e., was the increase in revenue or reduction in cost really caused by the implementation of the SIM products? There might be many factors, but the implementation of the SIM product most likely helped. Was the risk really reduced due to the implementation? Maybe, maybe not. 

**Revenue ROI** is probably the easiest to understand. How much more money did we make after the implementation?

**Cost ROI** can have many factors, including labor, productivity, COGS, depreciation, training cost, waste and many others.

**Asset ROI** can include inventory, DPO, DSO, property plant and equipment, and others.

**Risk ROI** can include lawsuits, regulations and fines, and other catastrophic events.

Calculating the exact value of a SIM product is almost impossible. This makes measuring and evaluating the success of a SIM solution very difficult. 

When calculating the ROI, be sure to have a clear understanding of the TCO (Total Cost of Ownership, and how many TLAs can we throw out?). Some solutions will require professional services while others don't. Some solutions will require you to get the hardware while others come as an appliance. Without a concrete TCO, the ROI figures are meaningless.

Understanding the various ROI metrics, knowing that these are fuzzy metrics, and clearly defining what the organization expects from a successful implementation will help shape the clear understanding of the values.



### 2. Lack of clear understanding of the users



Who are the main users of the solution you are implementing? Are they business users or technical users? Are they power users or casual users?

**Business users** are usually users from marketing, finance, and other non-technical groups in the organization. They are usually managers, directors and upper management. These users want to see summaries, dash boards, charts, graphs, and other reports that gives them a high level view and the ability to spot trends.

**Technical users** are usually users from IT, security and other operations groups. These are the users who want to see all the nitty-gritty details. They want to drill down and diagnose/troubleshoot problems. They perform the root cause analysis when the **** hits the fan. Some of the operational users will also want to see dash boards so that they can see things at a glance.

**Power users** are the people who wants to create their own reports. They are used to sophisticated interfaces and want the flexbility over (over-)simplicity. There users generally use the system 3 or 4 times a week or even every day and they can be anywhere in the organization, including marketing and finance.

**Casual users** generally use the system once a week or every other week. They may not even log into the system and prefer to receive the reports via email. These users wants to run pre-built reports and they have a specific set of reports they want to see. They don't have the knowledge or time to build their own reports. 

Knowing who your users are directly affect the solution you choose. If your users are mostly business users, you may want to choose a solution that's easy to use and provide the necessary views for these users. If most of your users are technical users, you will want a solution that provides the users the flexibilities that they need. Giving a technical users' interface to the business users will intimidate them and turn them off.



### 3. Lack of clear understanding of the requirements



Simply stating that "we need to analyze our firewall and web server logs" is not a requirement.  Having a SIM vendor come in to pitch, then draft the requirements based on the conversations is also the wrong way to go. These are just lazy ways of trying to get out of identifying the real requirements. There's no other way to detail out the requirements other than talking to the potential users.

Are your requirements based on regulations? security attacks? operational problems? If so, which regulation? What type of security attacks? internal or external? DoS attacks? What are the operational problems? Performance or capacity optimization? Trend analysis?

Are your requirements centered around log retention? real-time alerts? long term analysis? If so, how long is the retention requirement? How "real time" do the alerts need to be? How far back do you need to perform analysis? 

Do you have requirements on which logs need to be kept? OS logs? Network logs? Application logs? What type of reports the users need to see? High level or detailed reports?

Does your organization have requirements on the platforms? Windows? Linux? Java? No Java? Integration with corporate (authentication/authorization/web/database/storage) infrastructure? 

What's your requirement on performance? scalability? extensibility? manageability? usability? security? How much logs are you receiving (per second, retention period)? What's your network architecture (VERY distributed or centralized)? How many people are going to maintain this solution (1 admin with MANY OTHER responsibilities or you have spare resources)?

What are the criticality and/or priority of your requirements? 

Before evaluating any solutions, all these questions should be answered in details. Knowing your requirements will help you find the best product to fit your needs. Try not to choose a product or create unreasonable requirements because of brand loyalty (we only work with vendor X) or FOE (Friends of Executives).



### 4. Lack of clear understanding of the options



With all the talks these days about security information or event management and log analysis, it's easy for organizations to jump on the bandwagon and decide that they must have a SIM product in order to meet the requirements. 

There are at least 3 options out there: **commercial, open source and home-grown solutions**.

Before you jump to a commercial solution, you should evaluate your resources and skills within your own organization and see if you can/should go open source.

There are many factors when considering the commercial, open source or home-grown options. They include 





  * **Resource**. Do you have the head count that can support the option you choose? Commercial solutions may relieve your engineers from having to write and maintain code. When there's a problem, you can throw it over to the vendor and demand a resolution. Open source solutions is a middle ground between commercial and home-grown solutions. But when there's a problem, you have to either wait for a patch from the maintainers of the software or roll your own patch. Home-grown solutions will probably require the most from your engineers. You will have to write and maintain and enhance your solution.


  * **Skill set**. Do your engineers have the necessary skills to maintain an open source solution or develop a home-grown solution? This really goes back to your requirements. If your requirement is mainly retention and not analysis, you may be able to do that in house or get a open source solution. But if you are looking for deep correlation analysis, sophisticated graphing and charting, and pre-built log parsers and reports, you may want to check out a commercial solution.


  * **Time**. Even if you have the resources and skills within your organization, can you spare the time? Building a solution that meets your requirements is not a small undertaking. It will require dedicated resources and A LOT of time, time your organization probably can't spare. Can you spend hours or days in diagnosing your home-grown solution?


  * **Budget**. What is your budget for implementing this solution? Commercial solutions are not cheap. They can range anywhere from $25k to $750k, depending on your requirements. Your budget may vary based on the executive sponsor, the scale (departmental or corporate-wide), the urgency (SOX compliant by 2005), the risk (your organization lost 200k credit card #'s to a hacker last month), and other factors. If you have a small or no budget, you may need to go the open source or home-grown route (but know that these routes will have high costs as well).



Knowing your requirements will allow you to find the right option to meet your requirements.



### 5. Lack of clear understanding of the products



Many of the log analysis solutions out there are strong in some areas and weak in others. For example, some of the solutions provide better real-time analysis, whereas others are better at historical analysis. Some solutions are better at integrating the MANY log sources (network, system, application) whereas others provide better reports. Some solutions come in an appliance form factor, others are packaged software. Some solutions are targeted towards business users whereas others are targeted towards power users. Some solutions have much better visualizations while others have none.

Many vendors will tell you that they are strong in all areas. That's a **LIE**! If they tell you that, run away as fast as you can (or kick them out as fast as you can).

As the vendors about your requirements. Ask them to rate how well their solution meets your requirement. Ask to see a demo. Ask for an evaluation (on site or hosted by the vendor). Ask them how their solution compare to their competitors. Ask them to share their product roadmap (when you are seriously considering the product.) Ask about the support structure. 

Do **not** ever buy a solution without actually using it. There's no way to tell how usable the product is or whether it meets your requirements by looking at power point slides.

Try to be open minded. Most of the solutions you will see are still fairly new to the market. They will have holes and problems. They will not meet all your requirements 100%. This is why it is necessary to prioritize your requirements. It maybe that you need both real-time and historical analysis, but one of those may not be as critical as the other. In that case, if a vendor doesn't meet the less critical requirement but has a strong roadmap, it might be fine.

-----

These are common mistakes organizations make when they are considering a log analysis solution. Spending some time up front will help you avoid these and allow you to implement a solution that meets your **real** requirements.
