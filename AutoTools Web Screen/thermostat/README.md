This is the documentation for the Tasker-AutoTools-Web Screen-Termostat preset !
Here is how it looks like :
![](https://raw.githubusercontent.com/AgP42/TaskerProjects/master/AutoTools%20Web%20Screen/thermostat/images/thermostat.jpg)

# Installation

On Tasker :

- create a new task 
- add : "Plugin"/"AutoTools"/"Web Screen"
- "Configuration"
- "Import Preset" and then look for "Thermostat" on the list and click on "Import"
- (If you already import it, click on "Screen Preset" to find it on the list

# Use

You can set variables on all the parameters fields to display the values according to your system. 

On "Modes list", it has to be the exact same name than "Mode actuel" to allow the thermostat to display the correct actual mode. 

# Commands

Here are the possible commands and their effect :

- The arrow < > allows to increase or decrease the target value (unfortunately not yet possible to change it by sliding the slider)
- Clic on the value (the center of the slider or the small value that moves with the bar) to send the command `prefix=:=#mode#=:=#value#`
- a clic on any of the mode button will also trigger a command, it will be `prefix=:=#mode#` if the slider value hasn't been changed, or `prefix=:=#mode#=:=#value#` otherwise

# Issues/support

You can report any issues or proposal here : 
https://github.com/AgP42/TaskerProjects/issues
