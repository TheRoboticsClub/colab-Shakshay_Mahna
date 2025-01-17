---
layout: post
title:  "OS Upgrade"
date:   2019-12-02 21:00:00 +0530
categories: ros-melodic
---
Time to update to ROS Melodic Ubuntu 18.04


### Research on Navigation

Being a Computer Science student, and an aspiring engineer; I really like coding and reading about different Algorithms and Data Structures. It was really great when I came to know about this particular algorithm called VFF/Virtual Force Field (Yeah, you won't find it on Wikipedia) from José Sir.  It is a really cool Robotics Navigation Algorithm that allows a robot to navigate an obstacle based path. Too brief! Let's go on to some details:

![Algorithm](https://i.pinimg.com/originals/94/90/e8/9490e82b17e7af5a44d642698d461168.png)

Algorithms are everywhere! Be it [arranging marriages](https://en.wikipedia.org/wiki/Stable_marriage_problem#Algorithmic_solution) or [scheduling your busy day](https://en.wikipedia.org/wiki/Interval_scheduling). So, why leave Robotics? Now the domain of Robotics has algorithms pertaining to vision, naviagation and localisation and many more. The task for this week was to understand a navigation algorithm called Virtual Force Field(VFF).

As I mentioned above, there are no simple links relating to the topic, so I jumped right towards the [research paper](https://drive.google.com/file/d/1jW1im32z8-FG6wiZZ-M5Bzxh1WT_y8N6/view?usp=sharing)! It's on my personal drive, as I started maintaining one for Papers. It's a really cool algorithm, that allows an autonomous robot to navigate through a path consisting of obstacles. It does so by assigning our waypoint and the obstacle a vector. The obstacle behaves as a repulsive vector and the waypoint acts as an attracting vector. Summing both these vectors gives a resultant which our robot can follow. Simple enough let's move to something tougher. This algorithm cannot allow the robot to go through tight passages. Even if it enters one, there is a lot of unstable motion.

![Vector Addition](https://mathinsight.org/media/image/image/vector_2d_add.png)

So, the researchers J. Borenstein and Y. Koren came up with an improved version of the algorithm called [Virtual Field Histogram(VFH)](https://en.wikipedia.org/wiki/Vector_Field_Histogram). Yes, it's available on wikipedia. [Here](https://drive.google.com/file/d/1O-oTjDT-RYcKCSlYITsLGBPIMmCWTz_m/view?usp=sharing) is the research paper(My aim is to create a collection of these research papers on my drive #NerdGoals). It improves over the previous algorithm, by maintaining a histogram of sensor readings and following the direction in which there is a less threshold value, in short; a valley in the sensor readings.

![Virtual Field Histogram](http://www-personal.umich.edu/~johannb/bro114.gif)

But the next [problem](https://jderobot.github.io/RoboticsAcademy/portfolio/obstacle_avoidance/) I am going to solve involves VFF. So, that's what I have to code!

### Problems Ahead!

Let's launch the launch file! And here we are with a problem, we have a folder named obstacle_avoidance, but it contains the launch file to a turtlebot based exercise. Hence of no use! Now, as I can see, there is no launch file related to the problem I need to solve, but the launch file is present in the jderobot-gazebo-assets. So let's launch it from there. To implement the code, JDERobot provides us with an interface, which is executed in python. My next guess; let's run the interface of the turtlebot exercise of obstacle avoidance. We have the next problem! `jderobot` module not found.

After some searching and trying some tweaks on [Adarsh's](https://www.codechef.com/users/akcoder2) (he asked for a special mention) Ubuntu 18.04, I found that the problem was with Ubuntu 16.04, which I was using. Some of the program files for jderobot module refuse to download on 16.04 due to dependency issues. Hence, it was high time I switched to Ubuntu 18.04.

### ROS Melodic here I come!

![ROS Melodic](https://static.packt-cdn.com/products/9781783987443/graphics/c80c549f-8aa3-426a-8f79-81c55be057d7.png)

**SpoilerAlert**: Lots of errors and loads of Google searches ahead.

My best bet was to update the existing Ubuntu version. Simple, just follow random instructions given on a link generated by Google, until you encounter an error and try to fix it. The error was due to some broken packages present on my system. After a lot of brainstorming, and reading a lot about [Package Managers](https://en.wikipedia.org/wiki/Package_manager) and [differences between dpkg and apt](https://wiki.debian.org/DebianPackageManagement) ROS Kinetic was deleted and then the system was updated. A simple solution, but took a lot of time to strike.

What else can go wrong, when the update has completed and we finally have the Ubuntu 18.04 login screen? Nothing, just a login page loop! Again a lot of intersting searches about [gdm and lightdm](https://itsfoss.com/switch-gdm-and-lightdm-in-ubuntu-14-04/) which finally led to the solution. Just activate the terminal at login page, login with your account and type the command `lightdm`. A great temporary solution, will make it permanent soon!

![gdm](https://2.bp.blogspot.com/-_8kJ8k3wFRg/XBOpSdWKqyI/AAAAAAAACD4/BHYm4ZcW0Sk4_ne7klH0hqWwV7rV1PKCgCLcBGAs/w1200-h630-p-k-no-nu/display-manager-gdm3.png)

A simple installation of ROS Melodic, and then `sudo apt install jderobot`, we have our jderobot module ready to be used! This problem has also been referred in this [issue](https://github.com/JdeRobot/RoboticsAcademy/issues/349). 

### Next Week

Running the previously mentioned python file doesn't work. The interface mentioned in the website problem is quite different. So, maybe I was all wrong while finding the problem, or have to do some tweaks again, but that's all for next week! 

### References

[Package Manger](https://wiki.debian.org/DebianPackageManagement)
