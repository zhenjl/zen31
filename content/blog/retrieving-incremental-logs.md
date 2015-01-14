+++
Categories = ["log"]
date = "2006-01-05T09:02:21+00:00"
title = "Retrieving logs incrementally"
+++


Going through one of my sleepless nights again. So I figure I post a question here and see if I get any response.

I've always wondered what is the best way to incrementally upload logs from files that gets updated all the time. For example, application A writes to a log file. It continues to write to that file until the log file gest rotated, either through some external mechanism or the application itself.

There are several options here, obviously. 



### Batch Retrieval



First, the simplest thing to do is wait until the log file is closed and rotated, then upload the file to a central log server. Or the central log server comes and collect the log file using SCP/SFTP/HTTP/HTTPS/FTP. The problem with this approach is that the file may only get rotated every hour, day or week. This is not a feasible solution if there's real-time analysis requirements. For example, you wouldn't want to find some malicious sudo commands were executed a week later.



### Tail + Logger



The second approach is to tail the file and convert it to syslog using something like logger. This approach works somewhat. However, there are also several issues. One is that the tail command may exit for whatever reason. When that happens, you will stop sending logs. The obvious thing to do is to wrap tail in some script that will catch the exit and restart it. However, you may lose some logs during the process (probably unlikely unless lots of logs are being written.) In addition, converting to UDP syslog always has that slight chance of UDP packets being lost on a busy network.

Another problem with converting to syslog is that it won't work with log files that have headers. For example, W3C formatted files have a header that tells the any log parser what fields are included in the file. Without that, it would be pretty difficult to parse the logs. 

Be sure to use the **-F** option with tail in case files get rotated or modified by hand by some user.



### Continuous Curl



The third approach I thought of is to use [curl](http://curl.haxx.se) to upload the files to the central server periodically. However, I don't want to upload the whole file every time, otherwise I will get a ton of duplicate data. So I wrote a small wrapper in perl, [ccurl](http://www.zhen.org/misc/ccurl.txt) (continuous curl), to remember the last position uploaded, and upload only the new logs next time. Basically the script does the following:

1. When supplied a file, it will look for the last uploaded position. If never uploaded before, 0; otherwise the last uploaded position.
2. Run curl to upload the file starting at the last uploaded position. (my curl command uploads to a LogLogic appliance, but you can change it to upload to anything that accepts HTTP uploads.)
3. Update the position file with the latest uploaded position
4. Script exits

The idea is that someone will put this in a cron job and upload every few minutes. However, there are two huge problems with this script as quoted in the script.



```
        # if $size < $pos, that means the file has been rotated
        # however, there are two problems here
        # 1. $size could have increased so fast that the next time 
        #    the file is looked at, that it has increased passed
        #    $pos. this means we will miss all the logs before pos
        # 2. if the file is rotated, that means there's a possibility
        #    that we have lost some logs from the previous file,
        #    like from $pos to the end of the file
```



$size is the size of the actual log file, $pos is the file position of the last upload.

I am relying simply on the file name, which is totaly not fail proof. I added simple logic in there to detect when a file might have been rotated. 

I think I will change the script a bit later to have it use inode numbers to detect whether the file I am looking at is the same as before. This should work if the file is being APPENDED to ONLY. If someone decides to open it for writing, then the inode number will change. And that would totally screw me up.

[Disclaimer: this script is by no means production quality. Use/test at your own risk.]



### Tail + Curl



The last idea I have is to do a combination of #2 and #3. Basically I will write a script to wrap around **tail -F**, read the data for a while, upload the data to the central server using curl, and repeat.

This may turn out to be a better way than the first three. It gives me TCP and the wrapper can be maded to work with log files with headers.

Hum...stay tuned...I'll upload my script here when I get around to it. Or someone else may have done it already and can point me to the right direction. :)



