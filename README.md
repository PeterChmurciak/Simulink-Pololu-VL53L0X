# Simulink Pololu VL53L0X

Simulink S-function block that allows Simulink to receive data from the VL53L0X distance sensor through an Arduino board. It is based on [Pololu library](https://github.com/pololu/vl53l0x-arduino). Confirmed to work in Simulink R2019a on Arduino Uno R3.

The block was created to suit the needs of [AutomationShield](https://github.com/gergelytakacs/AutomationShield) project. If you are interested in control engineering and/or you want to learn about educative experiments that can be done using Arduino boards, pay a visit to the project [wiki page](https://github.com/gergelytakacs/AutomationShield/wiki).


## How to install

To be able to work with Arduino in Simulink you have to have [Simulink Support Package for Arduino](https://www.mathworks.com/hardware-support/arduino-simulink.html) installed.

To be able to create and compile the code in Simulink external mode you will need [MinGW-w64 C/C++ Compiler](https://www.mathworks.com/matlabcentral/fileexchange/52848-matlab-support-for-mingw-w64-c-c-compiler) and possibly (this one might not be needed) [Simulink Coder add-on](https://www.mathworks.com/products/simulink-coder.html) installed.

Assuming you have installed it already, to use this block you have to copy the `Pololu_VL53L0X` folder somewhere on your computer and 
add its content to the Matlab search path.

For example if its current location is `C:\Program Files\myProject\myFile\Pololu_VL53L0X` you would use Matlab command `addpath('C:\Program Files\myProject\myFile\Pololu_VL53L0X')`.

Now Matlab should be able to recognize the S-function inside of this file. To check if was detected sucessfully use Matlab command
`which('PololuVL53L0X')`.

You should see the path to the file `PololuVL53L0X.mexw64` located in the `Pololu_VL53L0X` folder.


## How to use

* Firstly, you have to change the execution mode of your Simulink model from `Normal` to `External` and choose your board from the list located in `Model Configuration Parameters` - `Hardware Implementation` - `Hardware board:` - for example `Arduino UNO`
 
* The next thing you need to do, is to add the `S-function block` to the model. Using `Library Browser` it can be found in `Simulink/User-Defined Functions`. When added, change its parameters followingly: 
  ```
  S-function name: PololuVL53L0X
  S-function modules: 'PololuVL53L0X_wrapper'
  ```  
  
* Now connect the output port of `S-function block` to a `Display` or a `Scope` block and press `Run` to see if everything works as it should
    
    
## Note

The block uses continuous reading mode with 20 millisecond measure timing budget. That means you should not use sampling step size smaller than 0.02 seconds to prevent overrun.
