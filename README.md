# CellProfiler
This repository contains CellProfiler Pipelines written for users of the IGC AIR facility. 
Keep reading for some help on using the pipelines.

# How to use a CellProfiler Pipeline
**Loading a pipeline to run**
*	The easiest way to load a CellProfiler pipeline is to drag the .cpipe file over to the white window on left side of the GUI. Once you drag it you will be asked if you want to load the pipeline to which you can say “Yes”.
*	Alternatively, you can go to ‘File’ > ‘Import’ > ‘Pipeline from file’

**Running a pipeline straight from Github**
* Go to the pipeline you want here in this repository (for example - https://github.com/IGC-Advanced-Imaging-Resource/CellProfiler/blob/master/Nuclei_Cytoplasm_Intensity.cppipe)
* If you click the "raw" button near the top right of the top of the code you will go to a new page where the script code is shown in raw form
* Copy the URL of that page
* Open CellProfiler and in the main window go to File > Import > Import from URL...
![Screenshot](https://github.com/IGC-Advanced-Imaging-Resource/CellProfiler/blob/master/images/ImportFromURL.jpg?raw=true)

**Loading images**
*	The first four modules which will be in any pipeline are ‘Images’, ‘Metadata’, ‘NamesAndTypes’ and ‘Groups’. 
  * Images is where you tell CellProfiler which images you want to be analysed. To do this, navigate to this module by double clicking on it and dragging you files into the big area that says “Drop Files and Folders here.” CellProfiler processes any image files found in any folders dragged in so don’t worry about putting all images in the same folder. CellProfiler can read any type of file format so there is no need to convert your files before use.
    * After you’ve added your images, go to the next module ‘Metadata’. If you have loaded multi-channel images then you will need to do the below:
    * First click the “Update Metadata” button in the top half of the module and then click the “Update” button on the table in the bottom half.
    * After doing this, you should see the table populate with your images with a line per channel.
  *	Next, check the NamesAndTypes modules to check what names are being assigned to each channel. You will see that there are “rules” for naming images, for example, that images with “Metadata with C matching 0” will be named DAPI. To know if the channels in your images have the correct names then you will need to know the order of your images. You may remember this from capturing them but you can only also open them in another image analysis program to find out.
  * Most pipelines have assumed that your images are 3 channels and they are in wavelength order (i.e. a DAPI, FITC and TXRD). If you images differ from this you will need to change which channel has which name. The names are important as they are what are used to apply the analysis in the pipeline.
    * N.B. If you have Micro-Manager images, it’s easier to skip metadata and this step completely (even though they are multi-channel). Name all your images thing in the next module and then use a module called “ColorToGrey” to split the channels. An example of this is in our example pipelines folders. You could also change the filter settings to say “Metadata have frame matching” instead of “C matching”. This is due to CellProfiler reading ome-tiffs as multi-frame TIFFs instead of multi-channel. An example of each pipeline like this can be found in the repo called “MicroManagerExamplePipeline_split” and “MicroManagerExamplePipeline” respectively with images to try the pipeline on.

**Test Mode**
*	To test the pipeline on a couple of your images, click the “Start Test Mode” button in the bottom left. Now you are in “Test” mode. By clicking the “Step” button you can see the results of each module. The module you are currently on (the active module) will be in bold and underline. 
*	To see the result the little eye icon to the left of the module needs to open. To change each module between open and closed you can double click the icon there.
*	A new window pops up for each module once it has run. If you can’t find the resultant window you can double click on the module name in the pipeline to bring it to the front. 
*	If you want to how the pipeline performs on a different image click “Next Image Set”, this will bring you back to the top of the pipeline with the next image set.

**Adjustments**
*	One major difference with CellProfiler to other image analysis programs is that analysis is performed using pixels instead of microns or another measurement unit. This means things really change depending on the camera and zoom you are using compared to what was used to set up the pipeline. 
*	For each module, there is a note section at the top. Advice may be written here regarding which parameters to change if the modules aren’t giving you the desired results. 
*	The main module that will need changed for the pipelines written by the facility will be module titled “IdentifyPrimaryObjects” so it’s a good idea to test this module at the very least. 
*	CellProfiler has a question mark icon to the right of each parameter that can be changed. If you click on this, a window with information explaining the parameter and how to change it depending on the result you want.

**Output**
*	All CellProfiler pipelines created in the facility are set to save any output (i.e. images and the spreadsheets) to the “Default Output Folder”
  *	To change the default output folder, click the “View Output Settings” at the bottom left of the GUI. 
* These CellProfiler pipelines will usually create a number of different spreadsheets. One will be called “Image”, this once will contain image level measurements (I.e. number of nuclei per image, mean size of nuclei per image, mean intensity per image. You will also have a spreadsheet for each “Object” created in CellProfiler (i.e. Nuclei, Foci, Cell). This will contain the measurements for the objects (but also lists the image each one came from). If you are doing a large number of images it is likely worth using a data analysis program like R to analyse your images. The facility can help you with setting this up.
*	By default CellProfiler scales all intensity values from 0 – 1. It does this by dividing the intensity values by the maximum possible value your images could have based on the bit-depth (i.e. for 16-bit images all the values are divided by 65535).
*	Remember, the distance results are in pixels (or pixels squared for area), so you may want to convert to microns using the scaling factor of your images. One way to do this is to open an image in FIJI and go to Image > Properties to see your pixel height and width.
  *	Example calculation
    * CellProfiler nuclear area = 12884 pixels squared
    * Square pixel size of image = 0.0515 x 0.0515
    * Area in microns = 12884 x (0.0515 x 0.0515) = 34.1625

**Analyze Images**
*	Once you have adjusted the pipeline as you want, exit “Test Mode”. 
*	Go to ‘Window” > ‘Hide all Windows on Run’ to close all the little eye icons. This will stop windows popping up while you run your full collection of images.
*	Click the “Analyze Images” button. This will run all your images through the pipeline. You will see a loading bar in the bottom right indicating how much is done and a window will pop up to say the analysis is complete once it’s done. 

**Further help if you are a first time user**

If you are opening CellProfiler you should see the Welcome window which has lots of helpful links on it:
*	If you click “Load” of ‘Load an example pipeline’ then a pipeline and a set of images will be loaded in your program. This can be run to get used to what the standard modules are if you’ve never used CellProfiler before.
*	If you click the “Download” link you will be taken to a page with example pipelines made by the CellProfiler team with images that can be run using.
