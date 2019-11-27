# SAP RESOURCES

https://archive.sap.com/kmuuid2/30d43eb9-487d-2e10-f688-a9dac9378490/SAP%20CRM%20WEB%20UI%207.0%20-%20Performance%20Testing


# SAP GUI NOTES:

## Objects

vugen is able to find the objects. for vugen anything there is in vugen is object. everything is an object. for vugen to do anything in vugen it has to identify objects.for example: btn1
when you highlight the icon/button the name appears.

every object has a name and vugen will identify with the name.

## control Ids
internally this object has control id. every object on the sap will have control id.


like every house has a address.

thousands of objects- if vugen has to identify the particular object it has to know the address of the house/object which is called control ids.

control id- address of the object called "save'

vugen treats every single thing in the screen as objects.everything you see is an object.


vugen assign control id's to each of these objects.


Once it is assigned it will go and identify those objects using the control ids 

Since the control ids can be really big in lr_strings.h is assigned to as a string variables and it is calling it as objects.and it is using the objects in script-shel112

will my script work, if i use control id's directly in the script?

## Enable scripting on the SAP Application Server

1. Open transaction rz11. 

Specify the parameter name sapgui/user_scripting and click Display.

The Display Profile Parameter Attributes window opens.

2. If Profile Val is FALSE, you need to modify its value. 

Click the Change value button in the toolbar. The Change Parameter 

Value window opens. Enter TRUE in the ProfileVal box and click 

the Save button.

3. Restart the application server to apply your changes.

## Enable scripting on SAP GUI client

During installation. While installing the SAP GUI client, enable the SAP GUI Scripting option.

## Replay SAP GUI Scripts

Replace Masked Password
For additional security, you can mask the password within the code. Right-click in the password text (the actual text, not *****) and select Mask String. VuGen inserts an lr_unmask function at the location of the password as follows:

sapgui_logon("user", lr_unmask("3ea037b758"), "800", "EN");

## Save Date Information

lr_save_datetime

```
lr_save_datetime("%d.%m.%Y", DATE_NOW + (2 * ONE_DAY),            

  "paramDateTodayPlus2");
sapgui_set_text("Req. deliv.date", 
        "{paramDateTodayPlus2}",
        "usr/ctxtRV45A-KETDAT", 
        BEGIN_OPTIONAL, 
            "AdditionalInfo=sapgui1025", 
        END_OPTIONAL);
```

## Retrieve Information

```
sapgui_status_bar_get_type

sapgui_status_bar_get_param
  ```

sapgui_status_bar_get_param function saves the order number 

into a user-defined parameter. In this case, the order number is 

the second index of the status bar string.

```
sapgui_press_button("Save (Ctrl+S)", 
    "tbar[0]/btn[11]", 
    BEGIN_OPTIONAL, 
        "AdditionalInfo=sapgui1038", 
    END_OPTIONAL);
sapgui_status_bar_get_type("Status");
if(0==strcmp(lr_eval_string("{Status}"),"Success"))
  sapgui_status_bar_get_param("2", " Order_Number ");
  ```


## Add Verification Functions

```
sapgui_is_object_available

if (!sapgui_is_object_available("wnd[1]"))
        sapgui_call_method("{ButtonID}", 
            "press", 
            LAST, 
            AdditionalInfo=info1011");
sapgui_press_button(.....)
```

# Performance Analysis -Looking into Metrics Using T- Codes 

## Performance Analysis Using SAP Transaction codes.

### ST02 : Memory/Buffer Management 

#### What is Buffer?

SAP stores frequently used information in buffers in memory.

Transaction ST02 monitors the usage of these buffers.

The most critical factors it reports are hit ratio, free spaces and swaps.

#### Hit Ratio: 

The hit ratio is the percentage of request that can be fulfilled by the information in each buffer (preventing expensive database requests), and perhaps is the most important statistic on the screen.

Note: The higher the hit ratio is the better it is.
The Hit Ratio of the single record buffer increases very slowly from system startup: therefore, a hit ratio less than 90% is a concern only if there is no free space left in the buffer.

#### Free Space

Free space measures how full the buffer is.

#### Swap

Swaps show how many times data had to be removed from the buffer to make room for other data.

### Interview Question:

What are the bottleneck that you have seen while doing sapgui?

I have monitored using ST02 and the hit ratio was less than 90% and there was no free space and definitely this was a concern and this is a bottleneck which i reported to the developer.

*Example NFR:*

```
Table:

Parameter      NFR        Desc
Hit Ratio      >95%       Percentage of requests filled by SAP buffer (memory) and not disk.
Free Space     >5%        Unused space percentage in each buffer.
Swaps          >3         No of times an object was swapped from a buffer to make room of another object.
```


## ST06:

Windows OS Level Monitoring - CPU Utilization


# Useful LR Shortcuts

control + T = TRANSACTION NAME


# LoadRunner VuGen Scripting Challenges
https://www.softwaretestinghelp.com/loadrunner/loadrunner-scripting-challenges/


# LoadRunner VuGen

## Steps To Record In VuGen:

- Open the VuGen.

- Select the Protocol.

- Provide a script name , Location , Solution Name, Solution Target 

- Click on Create.

- New Page Opens

- Add as many actions you need for the scenario and Edit the appropriate name for the actions or you can record in 1 action and later on you can create multiple actions and copy and paste/ move actions around.

- There is no hard and fast rule as to whether you have to put all the login in init and logoff in end. It's up to you.

- Cick on record button/click on record and click record  or use shortcut key CTRL + R

- Dialogue box opens 

- Select all the preferences and enter info. 

- Click on Start Recording.

- Recording dialogue box opens and the application where you perform the actions.

- Start performing the actions by commenting each action/ by giving start end transaction name and  by putting into right actions.

- After you are done stop the recording.

- Design studio dialog opens.

- Close the Design studio and you will see the actual recording/codes.

# Resourses of functions

https://knowhowz.weebly.com/performance-engineering/lr-function-lr_paramarr_random-parameter_array_name



# Drodown Correlation

web_reg_save_param_ex using ORD = ALL

In the web reg save param there are various arguments.
As a Performance Tester for the web reg save param ex fiction you have given  LB and RB with Ordinal = ALL to VuGen.

web reg save param ex will go the response grab the dynamic value in-between LB and RB and will put into a LR Parameter. Not only that it will also grab the similar dynamic value which is in-between LB and RB.dynamic value 2 and put it into LR Parameter.

now LR Parameter will store lot of values.

now the LR Parameter is not storing 1 value it it storing multiple values.

This is why we now call this LR Parameter as Array.only one parameter storing multiple values.

agenda:
========
1. Select one random Departure city from the drop down list.
Using ordinal= ALL , pull out all the departure cities     >>> array will be created.
2. From this array list, pick one value randomly and use this as a Departure City.
================================================= 


First you need to correlate the value "Depart."

```
********************************************** 
web_reg_save_param_ex("ParamName=Dept_City",
"LB=<option value=\"",
"RB=\">",
"Ordinal= ALL",
LAST);
*********************************************** 
```
First agenda is done…

now parameter value has to be randomly selected from this array. use this function for this.


lr_paramarr_ramdom("Dept_City");

i will be able to pick up a value randomly from this parameter called  Dept_City.

*****************************************
what is the input for this ? Dept_City

what is the output for this? String is the output for this.

how do you know this? 

go to functions in roadrunner.select hit f1

char *lr_paramarr_random(const char * paramArrayName);

What is the input for this? paramArrayName

what is the output for this? string char *

how the string should be declared ? char * should be declared as a pointer.

***************************************** 

now lr_paramarr_ramdom("Dept_City"); becomes

Random_Dept_City=lr_paramarr_ramdom("Dept_City");

now inside the global.h global variable

declare

``` 
char *Random_Dept_City;
```

now what happens from this array list one value will be picked up randomly from Dept_City which is holding 18 values and will be stored in Random_Dept_City.

lets see what value it has picked up? for this either you have to put lr output message or see in watch 

it has picked up san francisco. try more iterations.

now this Random_Dept_City variable will be holding some values.


no this randomly selected value needs to be passed in here(web request where it is depart)

now instead of denver put {"Random_Dept_City"} with curly braces. 

i am doing this because Random_Dept_City is holding a random value.

now tell me what is Random_Dept_City ? string , integers or float? 

it is a string. 

can i put string as an LR String as an input?

no. this web_submit data LR Functions only accepts LR Parameter. no strings, no inters, no float

now there is a need to convert this string Random_Dept_City into LR Parameter.

for this we can use : lr_save_string

lr_save_string("Random_Dept_City","pRandom_Dept_City");

conversion from string to LR Parameter is done.

now pass this value pRandom_Dept_City to web submit data with curly braces.{pRandom_Dept_City}.

instead of lr_save_string you can also use 

lr_param_sprintf("pRandom_Dept_City ", %s , "Random_Dept_City ");

now we need to pick up random city from arrival city also . since both have same values or are same you do not have to correlation again. or need to build web reg save param.

from the same Dept_City array - web reg save param pick one random city.

now change the parameter name:City

```
web_reg_save_param_ex("ParamName=City",
"LB=<option value=\"",
"RB=\">",
"Ordinal= ALL",
LAST);
```
declare

char *Random_Arrival_City;

Random_Arrival_City=lr_paramarr_ramdom("Arrival_City");

lr_save_string("pRandom_Arrival_City","Random_Arrival_City");

now pass this value pRandom_Arrival_City to web submit data with curly braces.{pRandom_Arrival_City}.

now it will pick random cities for both departure and arrival city.

# Example of extended RB to new line
```
web_reg_save_param_ex(

"ParamName=User_Session",
"LB=<option value=\"",
"RB=\">\n table border",
"Ordinal= ALL",
LAST);
```

# Understanding of What LG means in LoadRunner

1) LG is software which si avaiable with the loadrunner package. You have to identify a machine or server to install this LG software. Once the LG software is installed on a certain machine, we can call it as LG machine

2) We can hav as many LG machines as possible depending on your need. Maximum i have seen is 30 LG's

3) I have seen projects where performance testers created their own LG's and in bigger organizations, HP team (Now Microfocus team) usually do the installations. If you are given responsibility to create these LG's, you can take help of HP team. They are usually good with customer service

4) Once LG is created, you need to connect to these LG's from the controller


# Thread vs Process

Run Vuser As A Thread

Running Vuser as a thread will be more effective on keeping OS resources consumption on the injector's boxes to considerably low as this setting does not  have very heavy footprints.

Run Vuser As Process

Running user as process will be very heavy on OS resources consumption on the injector boxes.

Run Vuser As A Thread

As multiple threads running within a single process share the available resources among themselves, its recommended to use this setting when huge number of users are required to run on the injector boxes.


Run Vuser As Process

As each vsuer has its own process and privately allocated resources, it's not recommended to use this setting when huge number of vusers are are required to run on the injector boxes.

# LoadRunner Interview Questions

https://www.softwaretestinghelp.com/loadrunner-interview-questions-and-best-answers/


# Research about this company for reselling my stuff

https://www.therealreal.com/

# practice REST web services test automation

http://52.202.21.1:8080/swagger-ui.html

he web service is created around a well-known business domain for you, namely a bug tracking service.


# Why Averages Suck and Percentiles are Great

https://www.dynatrace.com/news/blog/why-averages-suck-and-percentiles-are-great/

# An Introduction to the Bell Curve

https://www.thoughtco.com/introduction-to-the-bell-curve-3126337

# The Bell Curve: Theory & Themes

https://study.com/academy/lesson/the-bell-curve-theory-themes-quiz.html


# Use of Bell Curve in Performance Appraisals – Good or Bad?

https://empxtrack.com/blog/bell-curve-for-performance-appraisal/


# Performance roles in client facing projects

https://www.linkedin.com/pulse/performance-roles-client-facing-projects-samson-jaykumar/?trackingId=pEptXcWaJRqcHTOa2B0g8g%3D%3D


# What it takes to build a Career in Performance Engineering?

https://www.linkedin.com/pulse/what-takes-build-career-performance-engineering-samson-jaykumar/

# Fundamentals of Performance Testing

https://www.linkedin.com/pulse/fundamentals-performance-testing-tomi-tiihonen/

# System Performance vs Page Speed

https://www.linkedin.com/pulse/system-performance-vs-page-speed-tomi-tiihonen/


# Need to check out these sites

https://dealsrookie.com/

https://www.nextgenerationautomation.com/

# Scrum Fundamentals Certified

https://www.scrumstudy.com/certification/scrum-fundamentals-certified




# Text Editors

## Brackets

http://brackets.io/

A modern, open source text editor that understands web design.

# Popular Blogs in Perfromance

https://stevesouders.com/


# Load Balancer

## Round Robin Load Balancing Definition

Round robin load balancing is a simple way to distribute client requests across a group of servers. A client request is forwarded to each server in turn. The algorithm instructs the load balancer to go back to the top of the list and repeats again.

## How Does Round Robin Load Balancing Work?

In a nutshell, round robin network load balancing rotates connection requests among web servers in the order that requests are received. For a simplified example, assume that an enterprise has a cluster of three servers: Server A, Server B, and Server C.

• The first request is sent to Server A.
• The second request is sent to Server B.
• The third request is sent to Server C.

The load balancer continues passing requests to servers based on this order. This ensures that the server load is distributed evenly to handle high traffic.

# Which Load Balancing Method Are You Using?

When your server is getting more requests than it can handle, it's a happy day for the marketing department. Lots of users are coming in and using the system. For the IT department, it means making some serious changes. It's time to add one or more servers, but they all have to look like one server to the users.

The server cluster has to allocate requests so that all the machines are doing a roughly equal share of the work. Otherwise, some users will get great performance while others will see a very slow server or even find their sessions dropped. The hardware and software that manages the allocation is a load balancer.

Many different approaches to load balancing are possible. What load balancers are you using? Which ones are better depends on the software being balanced, the hardware which runs them, and the communication among the servers. 

## Sticky or non-sticky?
The most basic distinction is between sticky and non-sticky load balancers. A sticky one keeps a user's session on the server where it started. A non-sticky balancer can put each request in a session on a different server.

The advantage of sticky sessions is that it isn't necessary to move session-related data from one server to another. This can produce more efficient performance. The disadvantage is that it's harder to keep the servers in balance. If sessions requiring a lot of work all accumulate on the same computer, they're going to stay there.

Whether stickiness wins or loses depends on the system architecture and the application that's being balanced. Here are some factors that come into play.

Factors favoring sticky sessions:

Each session uses a lot of server-side data that persists from one request to another.
Sessions are usually short and don't put a large burden on system resources.
Moving data between servers has a high cost.
Factors favoring non-sticky sessions:

Little or no server-side data persists between requests.
Some sessions put a significantly larger burden on the system than others.
A shared drive holds session data where each server can read and write it. If it's fast enough, non-stickiness imposes no cost.


Allocation methods
The next question is which server gets each new session (if sticky) or HTTP request (if non-sticky). The approaches range from simple to complex.

## Round Robin
The simplest is the round robin approach. Each new request goes to the next server in turn. This works best when all the servers have equal capacity. Even so, some servers could get unlucky and get all the more burdensome requests. This is less likely to be a problem with non-sticky sessions, since each server gets an equal number of short-lived requests rather than potentially getting long-lasting sessions.

If some of the servers are more powerful than others, a simple round robin doesn't work so well. The underpowered machines have to do just as much work as the big ones. A more sophisticated approach is necessary.

## Ratio-based Round Robin
The weighted or ratio-based round robin can deal with unequal servers. With this approach, the more powerful servers get additional requests. For instance, if Server A has twice the power of Server B and three times the power of Server C, then on each round A would get six requests, B would get three, and C would get two.

## Least Connections
A more dynamic approach is the least connections approach. In this case, the load balancer has to determine how many active connections each server currently has. It will assign a new request to the server with the fewest connections. If the servers have unequal capacity, then it will divide the number of connections by the server's relative power to decide which one has the lightest load. This provides the best ongoing balance at the cost of extra complexity.

The load balancer is a critical component of a service, since if it fails, all the servers it balances go off line. To guarantee availability, a failover load balancer should be available to take over when needed.

# Check Out: loadrunner-script-structure

https://qainsights.com/loadrunner-script-structure/ 

https://perfmatrix.blogspot.com/


www.coursera.org

www.udemy.com

www.edx.org

www.udacity.com

www.codecademy.com

www.linkedin.com/learning

www.learndigital.withgoogle

https://learndigital.withgoogle.com/digitalunlocked/courses




