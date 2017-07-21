# distributed-tensorflow
Implementation example of distributed TensorFlow

## Implementation

Two implementation examples are available:

* "Distributed Deep MNIST" - [distributed-deep-mnist.py](distributed-deep-mnist.py)
* "Distributed Deep MNIST with Queue" - [distributed-deep-mnist-with-queue.py](distributed-deep-mnist-with-queue.py)

### Distributed Deep MNIST

"Distributed Deep MNIST" is based on Distributed TensorFlow's [skeleton](https://www.tensorflow.org/deploy/distributed#putting_it_all_together_example_trainer_program) and rewrites "[Deep MNIST for Experts](https://www.tensorflow.org/get_started/mnist/pros "Deep MNIST for Experts | TensorFlow")" for distributed processing.

### Distributed Deep MNIST with Queue

"Distributed Deep MNIST" has to manually kill the process of the parameter server because it does not terminate when the task of the worker server is completed.

To solve this problem, "Distributed Deep MNIST with Queue" implements a mechanism to detect the task completion of the worker server and terminate the parameter server normally by introducing the queue. 

Note: 
* They are supposed to run in the TensorFlow 1.2 environment.
* These execution methods and execution options are common.

## Quick Usage

### Try quickly on a single machine

To quickly try distributed TensorFlow, run the following commands on a single machine. 

Example of execution with one parameter server and two worker servers.

```
Terminal1# python <FILENAME> --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=ps --task_index=0
Terminal2# python <FILENAME> --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=worker --task_index=0
Terminal3# python <FILENAME> --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=worker --task_index=1
```

Training starts after three commands are executed. MNIST dataset is downloaded to `/tmp/data_mnist` directory and trained model is saved in  `/tmp/train_logs` directory. These directories can be changed with the `--data_dir` option and `--log_dir` option respectively.

### When trying on multiple machines

Execution method is not much different from that on a single machine, but there are the following changes.

* Change localhost to another Hostname or IP address.
* `--log_dir` must specify a shared directory accessible to all hosts making up the cluster.
