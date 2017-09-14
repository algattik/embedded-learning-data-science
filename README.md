# Data Science Process with Embedded Learning Library

This is my work in progress to demonstrate how to use Keras and ELL to recognize custom objects using a Raspberry Pi. The training is done on a powerful VM on Azure, and the model is then compiled to run locally on a Raspberry Pi.

## Workflow

* __Data Acquisition__: We acquire movies of each of 3 objects (in this case bottles of different drinks) using the Raspberry Pi camera.

* __Dataset Preparation__: We extract still frames from each of the movies.

* __Model Training__: We use a Data Science Virtual Machine on Azure, equipped with GPUs, to fine-tune a previously trained deep learning network to recognize our objects.

* __Model "Operationalization"__: We compile the model for the Raspberry Pi. A demo application uses the model to label the content of images.

## Issues

At this time I get an error when trying to use the resulting model in ELL:

```
Constructing equivalent ELL layers from CNTK...
Converting layer  Convolution(ParameterTensor[64,3,3,3], Tensor[3,224,224]) -> Tensor[64,224,224]
Error occurred attempting to convert cntk layers to ELL layers
Traceback (most recent call last):
  File "./../../../../build/tools/importers/CNTK\cntk_to_ell.py", line 867, in predictor_from_cntk_model
    ellLayers = convert_cntk_layers_to_ell_layers(layersToConvert)
  File "./../../../../build/tools/importers/CNTK\cntk_to_ell.py", line 635, in convert_cntk_layers_to_ell_layers
    process_binary_convolutional_layer(cntkLayer, ellLayers)
  File "./../../../../build/tools/importers/CNTK\cntk_to_ell.py", line 337, in process_binary_convolutional_layer
    raise NotImplementedError("Error: Not yet implemented")
NotImplementedError: Error: Not yet implemented
Error occurrred attempting to wrap ELL predictor in ELL model
Traceback (most recent call last):
  File "./../../../../build/interfaces/python/utilities\ell_utilities.py", line 22, in ell_map_from_float_predictor
    shape = predictor.GetInputShape()
AttributeError: 'NoneType' object has no attribute 'GetInputShape'
Traceback (most recent call last):
  File "drinks.py", line 68, in <module>
    main()
  File "drinks.py", line 29, in main
    helper.save_ell_predictor_to_file(model, "vgg16ImageNet.map")
  File "modelHelper.py", line 95, in save_ell_predictor_to_file
    ell_map.Save(filePath)
AttributeError: 'NoneType' object has no attribute 'Save'
```
