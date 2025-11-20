# vlnce-python3.8-install
This installation guide successfully resolves the common issues encountered when setting up the VLN-CE environment on Python 3.8. The resulting environment has been verified to run on both [ETPNav](https://github.com/MarSaKi/ETPNav) and [NaVid](https://github.com/jzhzhang/NaVid-VLN-CE) in a headless GPU servers with A6000 and L40S GPUs.


1. Create a virtual environment with Python 3.8.
```bash
conda create -n vlnce3.8 python==3.8 -y
conda activate vlnce3.8
```
2. Clone and install a navigation policy (we use [ETPNav](https://github.com/MarSaKi/ETPNav) as example)
```bash
git clone git@github.com:MarSaKi/ETPNav.git
cd ETPNav
```
3. Clone and install ```habitat-sim-v0.1.7```
```bash
git clone https://github.com/facebookresearch/habitat-sim.git
cd habitat-sim/
git checkout tags/v0.1.7
pip install -r requirements.txt
python setup.py install --headless
```
4. Clone and install ```habitat-lab-v0.1.7```. Remove or comment out ```moviepy>=1.0.1``` and ```tensorflow==1.13.1``` from ```./habitat_baselines/rl/requirements.txt``` before running ```python setup.py develop --all```
```bash
git clone https://github.com/facebookresearch/habitat-lab.git
cd ../habitat-lab
git checkout tags/v0.1.7
pip install torch==1.10.0+cu111 torchvision==0.11.0+cu111 torchaudio==0.10.0 -f https://download.pytorch.org/whl/torch_stable.html
pip install -r requirements.txt
pip install msgpack cffi markupsafe # additional depencies
# Remove or comment out moviepy>=1.0.1 and tensorflow==1.13.1 from "./habitat_baselines/rl/requirements.txt" before proceeding
python setup.py develop --all
```
5. Downgrade ```setuptools``` and reinstall ```lmdb```
```bash
pip install setuptools==58.0.0
pip uninstall lmdb -y
rm -rf /home/sungjki/anaconda3/envs/vlnce3.8/lib/python3.8/site-packages/lmdb*
conda install -c conda-forge python-lmdb -y
```
6. Install remaining packages
```bash
pip install dtw fastdtw boto3 jsonlines networkx msgpack_numpy requests pytorch_transformers transformers
pip install git+https://github.com/openai/CLIP.git
pip install "numpy<1.24"
python -m pip install "pip<23.1"
pip install gym==0.21.0
