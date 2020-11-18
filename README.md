# README #

### What is this repository for? ###

* oxnnet_core is a light weight python program designed to be extended to create more complex neural networks for patch based image analysis
* Version 0.01

### How do I get set up? ###

**Create a working directory for the test** 
`set OXNNET_TEST_DIR=C:\oxnnet_test_dir`
`mkdir %OXNNET_TEST_DIR%

**Create a set of test cases** 

`python -m tests.utils %OXNNET_TEST_DIR%\TestVolumes`

**Write out the TensorFlowRecords**

`python main.py --model oxnnet.model.simplenet write --save_dir %OXNNET_TEST_DIR%\TestRect-tfr --data_dir %OXNNET_TEST_DIR%\TestVolumes\`

**Train the model**

`python main.py --model oxnnet.model.simplenet train --tfr_dir %OXNNET_TEST_DIR%\TestRect-tfr --save_dir %OXNNET_TEST_DIR%\TestRect-out --num_epochs 10 --batch_size 100`

**Test the model (replace <iteration_no> in this command)**

`python main.py --model oxnnet.model.simplenet test --save_dir %OXNNET_TEST_DIR%\TestRect-out\test --test_data_file %OXNNET_TEST_DIR%\TestRect-tfr/meta_data.txt --model_file %OXNNET_TEST_DIR%\TestRect-out\epoch_model.ckpt-<iteration_no> --batch_size 100`

**Inspect results**
Download an NII viewer from https://www.nitrc.org/projects/mricron.  Inspect the model outputs in `%OXNNET_TEST_DIR%\TestRect-out\val_preds_###` and compare them to coresponding test volume.

**Dependencies**

`tflearn (v0.3), tensorflow (v2.3), pandas, nibabel`

Python 3.8 recommended.

** How to run tests **

`python3 -m unittest`
