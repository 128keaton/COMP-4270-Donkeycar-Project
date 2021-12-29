
# COMP-4270-Donkeycar-Project

[Source Documentation](https://docs.donkeycar.com/)

## mycar

Project folder for the physical car


### Notes

* An image crop transformation is applied on the dataset to eliminate unneeded/distracting data on the horizon
	```
	# config.py
	TRANSFORMATIONS = ['CROP']
	ROI_CROP_TOP = 45               # the number of rows of pixels to ignore on the top of the image
	ROI_CROP_BOTTOM = 0             # the number of rows of pixels to ignore on the bottom of the image
	ROI_CROP_RIGHT = 0              # the number of rows of pixels to ignore on the right of the image
	ROI_CROP_LEFT = 0               # the number of rows of pixels to ignore on the left of the image
	```

* Additionally, we applied a 'MULTIPLY' transformation to ensure that the model would work well with different lightning conditions
	```
	# config.py
	AUGMENTATIONS = ['MULTIPLY']
	```

* Lastly, as we are using Donkeycar v4.2.1, the default model was the "fat" Tensorflow model. We had issues with
the car reacting too late, so we switched to the `tflite_linear` model
	```
	# config.py
	DEFAULT_MODEL_TYPE = 'tflite_linear'
	CREATE_TF_LITE = True
	```

	`$ donkey train --tub ./data/* --type tflite_linear --comment "model #2 tflite" `


## mysim

Project folder for the simulated car

