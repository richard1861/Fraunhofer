# Fraunhofer 

# Programmed solution and documents the obtained results

The first part about how I did this task, is that I created a new folder called "InspectionTry" which I attached in the mail. This zip file has all the python scripts (which are also in the GitHub page), but also there are some folders with the images and masks. This "InspectionTry" has the following files:

  -Gear (With all files about the Gear) -> Inside it, there are real images,synthetic images, masks and some other folders which I created.
  It is worth mentioning the folder "labels" inside Gear, which was created for the purpose of performing the last part of the task. It contains 78 gear images and it corresponding masks but with annotations on it. that is, I used an annotation tool on "Apeer.com" website in which I manually annotated 2 types of defects: Pitting (round shaped defects) and Scratching (long thin defects with curves). The result of these annotations are masks in .tiff format with annotation, that is, the background has value 0, the pitting defect has value 1 and the scratching defect has value 2.   
  
  -Spring (With all files about the Spring ) -> Inside it, there are real images,synthetic images, masks and some other folders which I created.
  It is worth mentioning the folder Blender_Synthetic_Images ,in both Gear and Spring, which contains some images taken by me in the software Blender.
  -Classification (labels for defect classification) -> Inside it, there are two subfolders, one with all Gear images (synthetic and real) and the other with all Spring images (synthetic and real)
  
  -Input Images -> A selection of 8 test images (2 synthetic gear, 2 real gear, 2 synthetic spring, 2 real spring) used for testing the results of the models in the different types of images.
  
  -Prediction Input Image -> The output of the models that use "Input Images"
  
  -Most of the scripts that are in the GitHub page (except two: DefectSegmentationUnet.py and Defect_classification.ipynb)
  -Some pretrained weights for the models.
 
The scripts in Github are:

- DefectSegmentationUnet.py -> model for defect segmentation using Unet CNN. Good results are obtained in the gear, especially in the synthetic images. On the other hand, poor results are obtained when training the springs because of the greater complexity of the images with respect to the gear. in the final part of this code an image taken in the blender software ("blender_synthetic_images" subfolder) is included to test the model. Good results are obtained for the gear and bad results for the spring, as expected. This script uses other two scripts:
  - simple_unet_model.py -> It defines the architecture of the Unet model.
  - data.augmentation.py -> Code used for increasing the size of the dataset. We only had around 120 images for gear, that might not be enough for a Unet CNN model. Therefore , use this code for increasing Gear and Spring images to 600 (Not more due to memory allocation problems in my GPU)

-Gabor.train.py and Gabor.predict.py -> model for defect segmentation using Random Forest and image filters. Due to the not so satisfactory results with the spring, I decided to try another type of model, in this case using several image filters, mainly gabor filters and creating a model with random forest. Better accuracy results are obtained although equal or worse visualization of the defects in the output image. It is worth mentioning, that the input is only 15 images (subfolders images_15 and masks_15 in both gear and spring) since this is not a Deep learning model that requires large amounts of input data. The output of this code is shown in the folder: Gabor result in both gear and spring.

-classification.py -> Classification model which can recognize if the image contains spring or gear object. After, a image is selected from the folder "Input Images" and this program recognizes which object it is and runs appropriate segmentation model. It does the segmentation in both models described previosly, that is, Unet and RF.

-Defect_classification.py -> A simple model using CNN (extractor) + RF to try to predict what kind of defect an image has. Bad results are obtained.

-Defect_classification.ipynb -> Since I was not able to obtain good results for the defect classification. I tried more complex deep learning models using different BACKBONES (resnet34,inceptionv3 and vgg16). However, the model only predicts well the background and not the defect. even adding different weights in the models to give more value to the defect pixels. 

In summary, the task was acceptably accomplished except for the prediction of springs and classification of defect types.

For this task I used spyder(anaconda tensorflow) and Google colab for one of the scripts (Defect_classification.ipynb)

Anaconda dependencies: 

# Name                    Version                   Build  Channel
absl-py                   1.0.0                    pypi_0    pypi
alabaster                 0.7.12             pyhd3eb1b0_0
appdirs                   1.4.4              pyhd3eb1b0_0
arrow                     0.13.1           py39haa95532_0
astroid                   2.6.6            py39haa95532_0
astunparse                1.6.3                    pypi_0    pypi
async_generator           1.10               pyhd3eb1b0_0
atomicwrites              1.4.0                      py_0
attrs                     21.4.0             pyhd3eb1b0_0
autopep8                  1.6.0              pyhd3eb1b0_0
babel                     2.9.1              pyhd3eb1b0_0
backcall                  0.2.0              pyhd3eb1b0_0
bcrypt                    3.2.0            py39h196d8e1_0
binaryornot               0.4.4              pyhd3eb1b0_1
black                     19.10b0                    py_0
bleach                    4.1.0              pyhd3eb1b0_0
brotlipy                  0.7.0           py39h2bbff1b_1003
ca-certificates           2021.10.26           haa95532_2
cachetools                5.0.0                    pypi_0    pypi
certifi                   2021.10.8        py39haa95532_2
cffi                      1.15.0           py39h2bbff1b_0
chardet                   4.0.0           py39haa95532_1003
charset-normalizer        2.0.4              pyhd3eb1b0_0
click                     8.0.3              pyhd3eb1b0_0
cloudpickle               2.0.0              pyhd3eb1b0_0
colorama                  0.4.4              pyhd3eb1b0_0
cookiecutter              1.7.2              pyhd3eb1b0_0
cryptography              36.0.0           py39h21b164f_0
cycler                    0.11.0                   pypi_0    pypi
debugpy                   1.5.1            py39hd77b12b_0
decorator                 5.1.0              pyhd3eb1b0_0
defusedxml                0.7.1              pyhd3eb1b0_0
diff-match-patch          20200713           pyhd3eb1b0_0
docutils                  0.17.1           py39haa95532_1
efficientnet              1.0.0                    pypi_0    pypi
entrypoints               0.3              py39haa95532_0
flake8                    3.9.2              pyhd3eb1b0_0
flatbuffers               2.0                      pypi_0    pypi
fonttools                 4.29.0                   pypi_0    pypi
gast                      0.4.0                    pypi_0    pypi
google-auth               2.4.1                    pypi_0    pypi
google-auth-oauthlib      0.4.6                    pypi_0    pypi
google-pasta              0.2.0                    pypi_0    pypi
grpcio                    1.43.0                   pypi_0    pypi
h5py                      3.6.0                    pypi_0    pypi
icu                       58.2                 ha925a31_3
idna                      3.3                pyhd3eb1b0_0
image-classifiers         1.0.0                    pypi_0    pypi
imageio                   2.14.1                   pypi_0    pypi
imagesize                 1.3.0              pyhd3eb1b0_0
importlib-metadata        4.8.2            py39haa95532_0
importlib_metadata        4.8.2                hd3eb1b0_0
inflection                0.5.1            py39haa95532_0
intervaltree              3.1.0              pyhd3eb1b0_0
ipykernel                 6.4.1            py39haa95532_1
ipython                   7.29.0           py39hd4e2768_0
ipython_genutils          0.2.0              pyhd3eb1b0_1
isort                     5.9.3              pyhd3eb1b0_0
jedi                      0.18.0           py39haa95532_1
jinja2                    2.11.3             pyhd3eb1b0_0
jinja2-time               0.2.0              pyhd3eb1b0_2
joblib                    1.1.0                    pypi_0    pypi
jpeg                      9d                   h2bbff1b_0
jsonschema                3.2.0              pyhd3eb1b0_2
jupyter_client            6.1.12             pyhd3eb1b0_0
jupyter_core              4.9.1            py39haa95532_0
jupyterlab_pygments       0.1.2                      py_0
keras                     2.7.0                    pypi_0    pypi
keras-applications        1.0.8                    pypi_0    pypi
keras-preprocessing       1.1.2                    pypi_0    pypi
keyring                   23.4.0           py39haa95532_0
kiwisolver                1.3.2                    pypi_0    pypi
lazy-object-proxy         1.6.0            py39h2bbff1b_0
libclang                  12.0.0                   pypi_0    pypi
libpng                    1.6.37               h2a8f88b_0
libspatialindex           1.9.3                h6c2663c_0
markdown                  3.3.6                    pypi_0    pypi
markupsafe                1.1.1            py39h2bbff1b_0
matplotlib                3.5.1                    pypi_0    pypi
matplotlib-inline         0.1.2              pyhd3eb1b0_2
mccabe                    0.6.1            py39haa95532_1
mistune                   0.8.4           py39h2bbff1b_1000
mypy_extensions           0.4.3            py39haa95532_1
nbclient                  0.5.3              pyhd3eb1b0_0
nbconvert                 6.1.0            py39haa95532_0
nbformat                  5.1.3              pyhd3eb1b0_0
nest-asyncio              1.5.1              pyhd3eb1b0_0
networkx                  2.6.3                    pypi_0    pypi
numpy                     1.19.5                   pypi_0    pypi
numpydoc                  1.1.0              pyhd3eb1b0_1
oauthlib                  3.1.1                    pypi_0    pypi
opencv-python             4.5.5.62                 pypi_0    pypi
openssl                   1.1.1m               h2bbff1b_0
opt-einsum                3.3.0                    pypi_0    pypi
packaging                 21.3               pyhd3eb1b0_0
pandas                    1.4.0                    pypi_0    pypi
pandocfilters             1.4.3            py39haa95532_1
paramiko                  2.8.1              pyhd3eb1b0_0
parso                     0.8.3              pyhd3eb1b0_0
pathspec                  0.7.0                      py_0
pexpect                   4.8.0              pyhd3eb1b0_3
pickleshare               0.7.5           pyhd3eb1b0_1003
pillow                    9.0.0                    pypi_0    pypi
pip                       21.2.4           py39haa95532_0
pluggy                    1.0.0            py39haa95532_0
poyo                      0.5.0              pyhd3eb1b0_0
prompt-toolkit            3.0.20             pyhd3eb1b0_0
protobuf                  3.19.3                   pypi_0    pypi
psutil                    5.8.0            py39h2bbff1b_1
ptyprocess                0.7.0              pyhd3eb1b0_2
pyasn1                    0.4.8                    pypi_0    pypi
pyasn1-modules            0.2.8                    pypi_0    pypi
pycodestyle               2.7.0              pyhd3eb1b0_0
pycparser                 2.21               pyhd3eb1b0_0
pydocstyle                6.1.1              pyhd3eb1b0_0
pyflakes                  2.3.1              pyhd3eb1b0_0
pygments                  2.10.0             pyhd3eb1b0_0
pylint                    2.9.6            py39haa95532_1
pyls-spyder               0.4.0              pyhd3eb1b0_0
pynacl                    1.4.0            py39hbd8134f_1
pyopenssl                 21.0.0             pyhd3eb1b0_1
pyparsing                 3.0.4              pyhd3eb1b0_0
pyqt                      5.9.2            py39hd77b12b_6
pyrsistent                0.18.0           py39h196d8e1_0
pysocks                   1.7.1            py39haa95532_0
python                    3.9.7                h6244533_1
python-dateutil           2.8.2              pyhd3eb1b0_0
python-lsp-black          1.0.0              pyhd3eb1b0_0
python-lsp-jsonrpc        1.0.0              pyhd3eb1b0_0
python-lsp-server         1.2.4              pyhd3eb1b0_0
python-slugify            5.0.2              pyhd3eb1b0_0
pytz                      2021.3             pyhd3eb1b0_0
pywavelets                1.2.0                    pypi_0    pypi
pywin32                   302              py39h827c3e9_1
pywin32-ctypes            0.2.0           py39haa95532_1000
pyyaml                    6.0              py39h2bbff1b_1
pyzmq                     22.3.0           py39hd77b12b_2
qdarkstyle                3.0.2              pyhd3eb1b0_0
qstylizer                 0.1.10             pyhd3eb1b0_0
qt                        5.9.7            vc14h73c81de_0
qtawesome                 1.0.3              pyhd3eb1b0_0
qtconsole                 5.1.1              pyhd3eb1b0_0
qtpy                      1.10.0             pyhd3eb1b0_0
regex                     2021.8.3         py39h2bbff1b_0
requests                  2.27.1             pyhd3eb1b0_0
requests-oauthlib         1.3.0                    pypi_0    pypi
rope                      0.21.1             pyhd3eb1b0_0
rsa                       4.8                      pypi_0    pypi
rtree                     0.9.7            py39h2eaa2aa_1
scikit-image              0.19.1                   pypi_0    pypi
scikit-learn              1.0.2                    pypi_0    pypi
scipy                     1.7.3                    pypi_0    pypi
seaborn                   0.11.2                   pypi_0    pypi
segmentation-models       1.0.1                    pypi_0    pypi
setuptools                58.0.4           py39haa95532_0
sip                       4.19.13          py39hd77b12b_0
six                       1.15.0                   pypi_0    pypi
snowballstemmer           2.2.0              pyhd3eb1b0_0
sortedcontainers          2.4.0              pyhd3eb1b0_0
sphinx                    4.2.0              pyhd3eb1b0_1
sphinxcontrib-applehelp   1.0.2              pyhd3eb1b0_0
sphinxcontrib-devhelp     1.0.2              pyhd3eb1b0_0
sphinxcontrib-htmlhelp    2.0.0              pyhd3eb1b0_0
sphinxcontrib-jsmath      1.0.1              pyhd3eb1b0_0
sphinxcontrib-qthelp      1.0.3              pyhd3eb1b0_0
sphinxcontrib-serializinghtml 1.1.5              pyhd3eb1b0_0
spyder                    5.1.5            py39haa95532_1
spyder-kernels            2.1.3            py39haa95532_0
sqlite                    3.37.0               h2bbff1b_0
tensorboard               2.8.0                    pypi_0    pypi
tensorboard-data-server   0.6.1                    pypi_0    pypi
tensorboard-plugin-wit    1.8.1                    pypi_0    pypi
tensorflow                2.7.0                    pypi_0    pypi
tensorflow-estimator      2.7.0                    pypi_0    pypi
tensorflow-gpu            2.7.0                    pypi_0    pypi
tensorflow-io-gcs-filesystem 0.23.1                   pypi_0    pypi
termcolor                 1.1.0                    pypi_0    pypi
testpath                  0.5.0              pyhd3eb1b0_0
text-unidecode            1.3                pyhd3eb1b0_0
textdistance              4.2.1              pyhd3eb1b0_0
threadpoolctl             3.0.0                    pypi_0    pypi
three-merge               0.1.1              pyhd3eb1b0_0
tifffile                  2021.11.2                pypi_0    pypi
tinycss                   0.4             pyhd3eb1b0_1002
toml                      0.10.2             pyhd3eb1b0_0
torch                     1.10.1                   pypi_0    pypi
tornado                   6.1              py39h2bbff1b_0
tqdm                      4.62.3                   pypi_0    pypi
traitlets                 5.1.1              pyhd3eb1b0_0
typed-ast                 1.4.3            py39h2bbff1b_1
typing_extensions         3.10.0.2           pyh06a4308_0
tzdata                    2021e                hda174b7_0
ujson                     4.0.2            py39hd77b12b_0
unet                      0.7.7                    pypi_0    pypi
unidecode                 1.2.0              pyhd3eb1b0_0
urllib3                   1.26.7             pyhd3eb1b0_0
vc                        14.2                 h21ff451_1
vs2015_runtime            14.27.29016          h5e58377_2
watchdog                  2.1.6            py39haa95532_0
wcwidth                   0.2.5              pyhd3eb1b0_0
webencodings              0.5.1            py39haa95532_1
werkzeug                  2.0.2                    pypi_0    pypi
wheel                     0.37.1             pyhd3eb1b0_0
whichcraft                0.6.1              pyhd3eb1b0_0
win_inet_pton             1.1.0            py39haa95532_0
wincertstore              0.2              py39haa95532_2
wrapt                     1.12.1           py39h196d8e1_1
yaml                      0.2.5                he774522_0
yapf                      0.31.0             pyhd3eb1b0_0
zipp                      3.7.0              pyhd3eb1b0_0
zlib                      1.2.11               h8cc25b3_4


  
  
