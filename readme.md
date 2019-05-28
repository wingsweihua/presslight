# PressLight

PressLight is a reinforcement learning method for multi-intersection traffic signal control. Usage and more information can be found below.

## Usage

How to run the code:

We recommend to run the code through docker. Some brief documentation can be found at https://docs.docker.com/.

1. Please build a docker image using the dockerfile provided. Note that, you need to download Anaconda from web (https://www.anaconda.com/distribution/) to finish the installation. We recommend to use Anaconda3-5.2.0-Linux-x86_64.sh.

docker build -t simulator-test -f simulator.dockerfile .

2. Please run the built docker image to initiate a docker container. Please remember to mount the code directory.

docker run -it -v path/to/the/code/repo/:/work/ simulator-test bash
cd /work/

(Alternatively, you can install the packages (included in the dockerfile) on your linux system)

Start an experiment by:

``python -O runexp.py``

Here, ``-O`` option cannot be omitted unless debug is necessary. In the file ``runexp.py``, the args can be changed. 

* ``runexp.py``

  Run the pipeline under different traffic flows. Specific traffic flow files as well as basic configuration can be assigned in this file. For details about config, please turn to ``config.py``. 


For most cases, you might only modify traffic files and config parameters in ``runexp.py``.
  
## Dataset



* ``data/template_lsr/1_6`` & ``data/template_lsr/16_1``

  The traffic files and roadnet file used in Section 6.4 & Section 6.5
  
  * New York data is in ``data/template_lsr/16_1``. Dataset for Jinan and State College will be included once granted.
  
  
* ``data/template_lsr/1_3_heterogenous`` && ``data/template_lsr/1_3_length``

  The traffic files and roadnet file used in Section 6.6.1
  
  
* ``data/template_lsr/1_10`` && ``data/template_lsr/1_20`` && ``data/template_lsr/3_3``

  The traffic files and roadnet file used in Section 6.6.2
  
* ``data/template_s/1_6``

  The traffic files and roadnet file used in Section 6.7.1
  

## Agent

* ``agent.py``

  An abstract class of different agents.


* ``network_agent.py``

  An abstract class of neural network based agents.  All methods are defined in this file but ``build_network()``, which means only ``build_network()`` is necessary in specific network agents.


* ``simple_dqn_agent.py``

  A DQN agent

## Others

More details about this project are demonstrated in this part.

* ``config.py`` 

  The whole configuration of this project. Note that some parameters will be replaced in ``runexp.py`` while others can only be changed in this file, please be very careful!!!

* ``pipeline.py``

  The whole pipeline is implemented in this module:

  Start a simulation environment, run a simulation for certain time(one round), construct samples from raw log data, update the model and model pooling.

* ``generator.py``

  A generator to load a model, start a simulation enviroment, conduct a simulation and log the results.

* ``anon_env.py``

  Define a simulation environment to interact with the simulator and obtain needed data like features.

* ``construct_sample.py``

* Construct training samples from original data. Select desired state features in the config and compute the corrsponding average/instant reward with specific measure time.

* ``updater.py``

  Define a class of updater for model updating.
  
