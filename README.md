Tutorials
===========================
we provide two tutorials for RGSE. We first apply RGSE to analyze a motivation program with respect to the `reader` property, i.e., the inputStreamReader cannot read while closed. 
Then, we present the analyzing for program `Rohino-a` with respect to the `Enumeration` property, i.e., invoking hasMoreElements before nextElement.
  
-------------------------

## **A Motivation Example**
 
The motivation example is shown below. We make the three integer variables m, n, and tag symbolic, and initialize them to 1, 1, and 5, respectively. 
Obviously, when tag equals 0 and n is positive, a violation of the reader property exists. 

![program](https://raw.githubusercontent.com/srv4j/images/master/moti.jpg)
 
------------------------------------------

## **(1). Analysis Driver**

The driver gives the entry point of the analysis, and contains two main modules, i.e., 
property specification and running configuration. 

* `Property Specification`: 
  
We specify the property to be checked as a finite state machine (FSM), where `I`, `R`, and `C` represent the `init`, 
`read`, and `close` event of the `reader` property. We recognize an event through comparing its class type and method 
name with the property specification. 
		
![fsm_spec](https://raw.githubusercontent.com/srv4j/images/master/FSA_moti.jpg)
![fsm](https://raw.githubusercontent.com/srv4j/images/master/FSM.jpg)
			
------------------------------------------

* `Running Configuration`: 

After writing the property specification, we need to configure RGSE. Specifically, the five parameters in args represent call string bound, 
guiding flag, refinement flag, maximum iterations, time threshold, result file name, and slicing flag, respectively. As show below, args ("1", "1"
"0", "-1", "0,0,10,0", "", "0") set the guiding flag true, and the time threshold to be 10 seconds.
		
![args_rgse](https://raw.githubusercontent.com/srv4j/images/master/args_moti.jpg)

----------------------------------------- 

## **(2). Running RGSE**

We can run RGSE in two ways, i.e., running the analysis driver as a Java application or running the docker script. The general command 
for running the script in command line is "./docker_script arg1 arg2 arg3". The three paremeters are used to specify the running mode.
Specifically, "0 0 0" is for DFS mode, "0 1 0" is for path slicing mode, and "1 0 0" is for our guiding mode. 

---------------------------------
## **(3). Analysis Result**
The results include the time and memory consumption, explored iterations, iteration for the accepted path, time for finding 
the first accepted path, and so on. For the toy example and the reader property, the result below show that RGSE can find the 
program path satisfying the FSM in the `2nd` iteration. On the other hand, neither `DFS` nor `slicing` can find the property violation
within the time threshold.  

![results](https://raw.githubusercontent.com/srv4j/images/master/moti_result.jpg)

---------------------------------------------------------

## **Program Rohino-a**

The javascript interpreter program `Rohino-a` is from the `Ashes suite` benchmark. The program can be download 
from [this link](https://github.com/jrgse/demo/tree/master/example-rhino).

-------------------
 
## **(1). Analysis Driver**

The driver gives the entry point of the analysis, and contains two main modules, i.e., 
property specification and running configuration. 

* `Property Specification`: 

We specify the property to be checked as a finite state machine (FSM), where`H` and `N` represent the
`hasMoreElements` and `nextElement` event of the `Enumeration` property. 

![fsm_spec](https://raw.githubusercontent.com/srv4j/images/master/FSM_specRohino.jpg)
![fsm](https://raw.githubusercontent.com/srv4j/images/master/FSM_bloat.jpg)

---------------------------------------

* `Running Configuration`: 

After writing the property specification, we need to configure RGSE. Specifically, the five parameters in args represent call string bound, 
guiding flag, refinement flag, maximum iterations, time threshold, result file name, and slicing flag, respectively. As show below, args ("1", "1"
"0", "-1", "0,10,0,0", "", "0") set the guiding flag true, and the time threshold to be 30 minutes.

![args](https://raw.githubusercontent.com/srv4j/images/master/args_rohino.jpg)

------------------------------

## **(2). Running RGSE**

We can run RGSE in two ways, i.e., running the analysis driver as a Java application or running the docker script. The general command 
for running the script in command line is "./docker_script arg1 arg2 arg3". The three paremeters are used to specify the running mode.
Specifically, "0 0 0" is for DFS mode, "0 1 0" is for path slicing mode, and "1 0 0" is for our guiding mode. 


---------------------------------

## **(3). Analysis Result**
The results include the time and memory consumption, explored iterations, iteration for the accepted path, time for finding 
the first accepted path, and so on. The result below show that RGSE can find the program path satisfying the FSM in 1707841 
seconds (about 28 minutes). On the other hand, neither `DFS` nor `slicing` can find the property violation even within 1 hour. 

![results](https://raw.githubusercontent.com/srv4j/images/master/rohino_result.jpg)

---------------------------------
