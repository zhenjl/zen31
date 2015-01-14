+++
Categories = ["cloud"]
date = "2009-05-10T03:25:37+00:00"
title = "Three Cloud Resource Consumption Models"
+++


For the Infrastructure-as-a-Service market, there appears to be three models of consumption today:


1. Allocation-based
2. Usage-based
3. Resource pool-based



First it's allocation-based consumption. Example would be EC2 where you allocate a VM with a certain amount of CPU/memory and you pay for that allocation. No need for a lot of explanations here since this is the model that most people are familiar with.

The second model is a usage-based consumption. This model does not require any allocation or resource pool and the cloud would simply allow you to use resources as needed. For example, your application may only use 300 MHz of CPU and 200MB of memory during normal operations and that's all you pay for. If the application spikes to 1 GHz of CPU and 3 GB of memory for a period of time, you pay for that also. This model is a lot more unpredictable but could potentially be a lot cheaper than the previous two. [Terremark's Enterprise Cloud](http://theenterprisecloud.com/) allows you to burst into this model once you have used up your resource pool. This model is much more of a true utility model since you pay for what you **use**. As far as I know no service provider is offering ONLY this model.

The third model is a resource pool model, which is a combination of the previous two model. In this case, a resource pool, say 5 GHz of CPU and 10GB of memory, is allocated, and you can spin up as many VMs as you like to consume that pool of resource. This model is a combination model because it's still based on allocation but still gives you the advantage of granular metering. The advantage of this model is that you have much better control over the resource pool and if you know your applications well (e.g., the amount of CPU/memory they consume), this will be much more cost effective. [Terremark's Enterprise Cloud](http://theenterprisecloud.com/) is based on this model. 

Both second and third require very granular and accurate resource utilization monitoring. An important factor to consider for all these models is "burst capacity." That is, if your VM needs additional capacity, can you "burst" or do you need to allocate a new VM and move your workload to the new VM? Which model you should choose depends heavily on how well you know your applications' resource utilization pattern. If you know your applications well and can predict the usage pattern, then a resource pool model or true utility model might be better. If you want predictability and fixed pricing, then either the allocation model or the resource pool model will suffice. If you know you will be running many VMs and know your application usage patterns well, then a resource pool model may be best. 

One thing to note here is that all these are consumption models and not cost or billing models. The service provider may charge you per hour or per month based on your allocation or resource pool. There may also be minimum resource level commitment. The service provider may bill you weekly, monthly or quarterly. It's important to understand the differences of consumption, cost and billing models.
