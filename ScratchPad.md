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








# Useful LR Shortcuts

control + T = TRANSACTION NAME


# LoadRunner VuGen Scripting Challenges
https://www.softwaretestinghelp.com/loadrunner/loadrunner-scripting-challenges/








