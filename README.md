# Chiplet Interconnect SI Dataset
This is the chiplet interconnect SI dataset described in the paper:  
GNN-SP: Fast S-Parameter Estimation of Chiplet Interconnect via Graph Neural Network  
Description of each folder is shown below:  
1. example_ads_project  
   This folder includes an example project to simulate chiplet UCIe interconnects in `layout` folder using the Agilent Advanced Design System (ADS) Momentum simulator based on the Method of Moments (MoM). The simulating frequency ranges from 0GHz to 60GHz with 1GHz step size. 
2. layouts  
   This folder includes the gds file of each chiplet interconnect data.  
   - Name of each subfolder is formated as `x_y`, where `x` and `y` are coordinates of the second macro with different positions. Note that to generate the routing data, we fix the postion of the first macro and move that of the second macro, then we generate the routing result by the chiplet routing tool.  
   - In each subfolder, interconnect data with different module map and pitch are included. Layout files has the suffix of `.gds`. The coordinates of wires in each net coorsponding to each `.gds` file are recorded in files with suffix `.txt`  
3. s_parameter_files  
   This folder includes the s-parameters of each chiplet interconnect data with suffix of `.txt` (Needs to unzip the `.7z` files first). Note that for a net, s-parameters of its 2-hop neighbors are recorded in the `.txt` file in this folder.  
   - The port id of each net with id `i` is `i*2` (port on the right of the net) and `i*2+1` (port on the left of the net). 
   - The first line of each file is `Numtype 3 port id start from 0` means S-parameters have 3 types:
     - S-parameters between ports on the same net, e.g. the inserssion loss and return loss of each port. 
     - S-parameters of near crosstalk. 
     - S-parameters of far crosstalk.   
   - Each type of S-parameters will start with line `Nump1 x`, e.g. `Nump1 74` means this type have 74 set of S-parameters. 
     - Each set of S-parameters will start with line `px y`, e.g. `p16 2` means this set of S-parameters are considered from port 16 to two other ports. 
       - In each other port will start with line `px 122`, e.g. `p17 122` means the other port id is `17` and have `122/2=61` frequency points.
       - The following line of each other port will be magnitude(dB) and phase(degree) of S-parameters of each frequency. The first 61 elements are magnitude(dB) and the last 61 elements are phase(degree).  

The document of this dataset will keep updating to offer more details, if you have any questions, please contact: <21112020054@m.fudan.edu.cn>