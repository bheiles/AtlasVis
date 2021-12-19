
# AtlasVis
*Visualization toolbox for "Volumetric ultrasound localization microscopy of the whole brain microvasculature"*

Baptiste Heiles<sup>1,2,3</sup>, Arthur Chavignon<sup>1</sup>, Antoine Bergel<sup>2</sup>, Vincent Hingot<sup>1,2</sup>, Hicham Serroune<sup>2</sup>, David Maresca<sup>3</sup>,Sophie Pezet<sup>2</sup>, Mathieu Pernot<sup>2</sup>, Mickael Tanter<sup>2</sup>, Olivier Couture<sup>1</sup>
  
<sup>1</sup>Sorbonne Université, CNRS, INSERM, Laboratoire d’Imagerie Biomédicale 
<sup>2</sup>Institute Physics for Medicine, CNRS, INSERM, ESPCI Paris, PSL Research University, 
<sup>3</sup> Department of Imaging Physics, TU Delft, Netherlands
Corresponding author: baptiste.heiles@gmail.com


## Installation

1. Download the executable file from the github repository
2. Double-click the executable file and follow the installation instructions
3. Run the app named AtlasVis from the Windows startup panel

## Associated dataset
The associated dataset are available at this [link](https://surfdrive.surf.nl/files/index.php/s/l5hS19lQxbqA5vf) during the whole review process and will be made available to the public using a Zenodo repository upon publication.
1. "Density.mat" : a matrix file containing density of microbubbles
3. "NormedVelocity.mat" : a matrix file containing normed-velocity of microbubbles tracked
4. "SignedVelocity.mat" : a matrix file containing normed-velocity <b>with</b> encoded sign. The velocities towards the top of the image are assigned the negative sign.

## Usage
All the different panels are explained in the <b>Interface</b> section.

At the execution, simply start by loading the dataset you want to explore using the "Load Vol 1" button and selecting either "Density.mat", "NormedVelocity.mat", "SignedVelocity.mat". Wait until the busy lamp turns green again (can take up to 15 minutes) and the load the atlas files using the "Load atlas" button and selecting the matrix file "AtlasMoved.mat". When all the data has been loaded, you should be able to explore the dataset by using the different controls explained in the next section.


## Interface
After opening the app, you will be faced with a blank graphical interface allowing you to load and explore 3 different types of data obtained from 3D Ultrasound Localization Microscopy of the whole rat brain.
  
<a href="https://github.com/bheiles/AtlasVis/blob/main/Images/initialization.png"><img src="https://github.com/bheiles/AtlasVis/blob/main/Images/initialization.png" width="478" height="300"/></a>

It is composed of 4 panels:

<b>1. Panel "Load and parameters"</b>

  a) "Load Vol 1" : this is the load button. Click on it to load the 3D ULM data (either  Density, Normed velocity or Signed velocity). This step takes a while when the volumes are big
  
  b) "Load atlas" : this will load the atlas registered to the volume. Everytime you change slice, a partial section of the atlas will be loaded to prevent overflowing the memory
  
  c) "Voxel size" : this is the voxel size in micrometers. For the dataset available, it is pre-entered as 10x10x10 and should not be changed
  
  d) "Velocity unit (m/s)" : this is the unit of the velocity measured in the matrix loaded (so only useful when you load velocities, not densities). It is pre-entered as 1 micrometers/s
  
<b>2. Panel "Display parameters"</b>

  a) "Slab thickness" : this is the thickness of the slab you want to display in voxel size. Initial value is 100, which means the interface will display a slab of thickness 1 mm
  
  b) "Caxis" : this controls the color axis and is scaled according to min and max values of the matrix loaded. Please note that to increase the dynamic range of small vessels, square root compression is computed for density based renderings, and 3rd order root is computed for velocity based renderings.
  
  c) "Type" : this dropdown menu allows to select which kind of data you have loaded, and will change the colormap accordingly.
  
<b>3. Panel "Explore and measure"</b>

  This panel will display coronal/sagittal/transverse cuts according to the display parameters entered. The title of the axes indicates the anatomical zone where the mouse pointer is. Moving the mouse outside of the axes will display "unknown anatomical area"
  
  a) "Direction" : this dropdown menu allows to select the direction of the cut you want to display. Direction 1 corresponds to transverse cuts, direction 2, to sagittal cuts, direction 3, to coronal cuts.
  
  b) "Velocity filter" : this button activates a 3rd order median filter which is useful when displaying signed velocity matrices (V3) as the superposition of vessels in the cut can make it arduous to visualize correct velocities.
  
  c) "Slice #" : this spinner allows to navigate along the direction chosen with voxel size step.
  
  d) "Select center" : this button will draw a cross-hair on the display. Simply press-down the left button of your mouse to fix the cross-hair and record the position. The algorithm will then take that position as an input. It will calculate the center position of the vessel according to this position, compute the surface orthogonal to the direction of the vessel and draw the 3D velocity profile on the 1st axes as a surface. The velocity profiles in each direction are represented in the background of the 3D plot. The two profiles along the two directions are also represented in the two axes below.
  <a href="https://github.com/bheiles/AtlasVis/blob/main/Images/crosshair.PNG"><img src="https://github.com/bheiles/AtlasVis/blob/main/Images/crosshair.PNG" width="202" height="150"/></a>
  
<b>4. Panel "Result"</b>

  This displays the results of the algorithm used to get the velocity profiles and diameters based on the cross-hair position selected. The algorithm will then take that position as an input. It will calculate the center position of the vessel according to this position, compute the surface orthogonal to the direction of the vessel and draw the 3D velocity profile on the 1st axes as a surface. The velocity profiles in each direction are represented in the background of the 3D plot. The two profiles along the two directions are also represented in the two axes below.
   <a href="https://github.com/bheiles/AtlasVis/blob/main/Images/result.PNG"><img src="https://github.com/bheiles/AtlasVis/blob/main/Images/result.PNG" width="107" height="187"/></a>
  a) The two offset spinners can be modified if the user thinks the mid-line taken by the algorithm as the center of the vessel is slightly off (i.e the maximum of the velocity is not centered around 0 in the two plots below)
  
  b) D1, D2 and Speed measure the diameters in the two direction of the vessel and the maximum speed.

  c) The save button will save the position, diameters estimate (micrometers) and velocity (mm/s) in a file called "SavedPos_datetag" (datetag indicates a timestamp). The first time you press this button it will ask you for a folder to save in.
  
The green/red button indicates whether the interface is busy or not. When loading or calculating speed, it is not uncommon that the toolbox will take a long time to execupte/compute and the button will stay red for a while. It has not necessarily crashed. Loading a matrix can take up to 15 minutes on slower machines.

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
CC BY-NC-SA 4.0


## Disclaimer

THIS SOFTWARE IS PROVIDED BY THE AUTHORS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE AUTHORS AND CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
