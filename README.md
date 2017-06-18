# distributed-tensorflow
Implementation example of distributed TensorFlow

This project is a rewrite of the tutorial code for distributed processing based on the skeleton shown in the official TensorFlow document.

Distributed TensorFlow's skeleton is [here](https://www.tensorflow.org/deploy/distributed "Distributed TensorFlow | TensorFlow").

## Distributed Deep MNIST
Distributed Deep MNIST ( [distributed-deep-mnist.py](distributed-deep-mnist.py) ) is a rewrite of the code shown in the "[Deep MNIST for Experts](https://www.tensorflow.org/get_started/mnist/pros "Deep MNIST for Experts | TensorFlow")" tutorial for distributed processing.

Note: Distributed Deep MNIST is supposed to run in the TensorFlow 1.2 environment.

### Quick Usage
To quickly try Distributed Deep MNIST, run the following commands on a single machine. If you want to try on multiple machines, change "localhost" to any hosts.

Example of execution with one parameter server and two worker servers.

```
Terminal1# python distributed-deep-mnist.py --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=ps --task_index=0
Terminal2# python distributed-deep-mnist.py --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=worker --task_index=0
Terminal3# python distributed-deep-mnist.py --ps_hosts=localhost:2222 --worker_hosts=localhost:2223,localhost:2224 --job_name=worker --task_index=1
```
