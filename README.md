# Data Science Process with Embedded Learning Library

This is my work in progress to demonstrate how to use Keras and ELL to recognize custom objects using a Raspberry Pi. The training is done on a powerful VM on Azure, and the model is then compiled to run locally on a Raspberry Pi.

## Workflow

* __Data Acquisition__: We acquire movies of each of 3 objects (in this case bottles of different drinks) using the Raspberry Pi camera.

* __Dataset Preparation__: We extract still frames from each of the movies.

* __Model Training__: We use a Data Science Virtual Machine on Azure, equipped with GPUs, to fine-tune a previously trained deep learning network to recognize our objects.

* __Model "Operationalization"__: We compile the model for the Raspberry Pi. A demo application uses the model to label the content of images.


## Process

* Create a Linux Data Science Virtual Machine on Azure. Select HDD disk type, then select an NC instance (with GPUs).

* SSH to the machine and run the commands in INSTALL.txt. Copy the Notebooks from this project to your ~/notebooks directory.

* Open Jupyter in a web browser, at the URL https://<VM DNS name or IP Address>:8000/

* Run the 3 notebooks

## Issues

At this time I can run the ELL model on the Linux server, but compilation on Raspberry Pi fails with:

```
/usr/bin/ld: BFD (GNU Binutils for Raspbian) 2.25 assertion fail ../../bfd/elf32-arm.c:7827
```
