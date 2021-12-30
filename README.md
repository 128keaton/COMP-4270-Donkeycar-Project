
# COMP-4270-Donkeycar-Project

[Source Documentation](https://docs.donkeycar.com/)

All models were trained on an M1 Max MacBook Pro using Python 3.9. Average training time was 5-8 minutes. 

### Python 3.9

Donkeycar is built for Python 3.7, but in order to utilize the native processing speed of the M1 Max, I "fixed" the Python 3.9-specific issues in [my Donkeycar branch](https://github.com/128keaton/donkeycar/tree/m1-py3.9). At the time of writing, it is based off the latest `master` version (4.2.1) of Donkeycar. 

You should be able to roughly follow the Mac guide on the Donkeycar documentation site above.

Some dependencies were not available though `conda` or `conda-forge` for the M1/arm64-macOS arch, which is why they were removed from the `mac.yml` [Conda environment file](https://github.com/autorope/donkeycar/compare/master...128keaton:m1-py3.9?expand=1#diff-e6da1d196d2d58206198e24cd26781d530c2180888afa5e484e184314bce494f).

Instead, install these with `pip`:

`$ pip3 install kivy torch torchaudio`

Lastly, to install Tensorflow (with Metal acceleration) follow the instructions [Apple themselves](https://developer.apple.com/metal/tensorflow-plugin/) has provided.

These instructions may be completely wrong when you're attempting this yourself, but it'll at least get you pointed in the right direction.


## mycar

Project folder for the physical car


### Notes

* An image crop transformation is applied on the dataset to eliminate unneeded/distracting data on the horizon
	```python
	# config.py
	TRANSFORMATIONS = ['CROP']
	ROI_CROP_TOP = 45               # the number of rows of pixels to ignore on the top of the image
	ROI_CROP_BOTTOM = 0             # the number of rows of pixels to ignore on the bottom of the image
	ROI_CROP_RIGHT = 0              # the number of rows of pixels to ignore on the right of the image
	ROI_CROP_LEFT = 0               # the number of rows of pixels to ignore on the left of the image
	```

* Additionally, we applied a 'MULTIPLY' transformation to ensure that the model would work well with different lightning conditions
	```python
	# config.py
	AUGMENTATIONS = ['MULTIPLY']
	```

* Lastly, as we are using Donkeycar v4.2.1, the default model was the "fat" Tensorflow model. We had issues with
the car reacting too late, so we switched to the `tflite_linear` model
	```python
	# config.py
	DEFAULT_MODEL_TYPE = 'tflite_linear'
	CREATE_TF_LITE = True
	```

	Training:
	
	`$ donkey train --tub ./data/* --type tflite_linear --comment "model #2 tflite" `


## mysim

Project folder for the simulated car

## Credits

Special thanks to the Donkeycar Discord community members listed below, they were invaluable in getting the car operating properly:
	* Ezward
	* Maxime Ellerbach
	* DGarbanzo

