# distributed-tensorflow
Implementation example of distributed TensorFlow

This project is a rewrite of the tutorial code for distributed processing based on the skeleton shown in the official TensorFlow document.

Distributed TensorFlow's skeleton is [here](https://www.tensorflow.org/deploy/distributed "Distributed TensorFlow | TensorFlow").

## Distributed Deep MNIST

Note: Distributed Deep MNIST is supposed to run in the TensorFlow 1.2 environment.

### Distributed Deep MNIST

"Distributed Deep MNIST" ([distributed-deep-mnist.py](distributed-deep-mnist.py)) is based on Distributed TensorFlow's skeleton and rewrites "[Deep MNIST for Experts](https://www.tensorflow.org/get_started/mnist/pros "Deep MNIST for Experts | TensorFlow")" for distributed processing.

### Distributed Deep MNIST with Queue

"Distributed Deep MNIST with Queue" ([distributed-deep-mnist-with-queue.py](distributed-deep-mnist-with-queue.py)) implements a mechanism to detect the task completion of the worker server and terminate the parameter server normally by introducing the queue. This script can be executed using the same option as "Distributed Deep MNIST".

### Quick Usage

To quickly try Distributed Deep MNIST, run the following commands on a single machine. If you want to try on multiple machines, change "localhost" to any hosts.

Example of execution with one parameter server and two worker servers.

```
Terminal1# python distributed-deep-mnist.py --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=ps --task_index=0
Terminal2# python distributed-deep-mnist.py --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=worker --task_index=0
Terminal3# python distributed-deep-mnist.py --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=worker --task_index=1
```

### Show all options

`--help` can be used to display all options

```
# python distributed-deep-mnist.py --help
usage: distributed-deep-mnist.py [-h] [--ps_hosts PS_HOSTS]
                                 [--worker_hosts WORKER_HOSTS]
                                 [--job_name JOB_NAME]
                                 [--task_index TASK_INDEX]
                                 [--data_dir DATA_DIR] [--log_dir LOG_DIR]

optional arguments:
  -h, --help            show this help message and exit
  --ps_hosts PS_HOSTS   Comma-separated list of hostname:port pairs
  --worker_hosts WORKER_HOSTS
                        Comma-separated list of hostname:port pairs
  --job_name JOB_NAME   One of 'ps', 'worker'
  --task_index TASK_INDEX
                        Index of task within the job
  --data_dir DATA_DIR   Directory for storing input data
  --log_dir LOG_DIR     Directory for train logs
```
