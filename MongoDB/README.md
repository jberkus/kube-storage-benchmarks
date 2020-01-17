These scripts will simplfy running YCSB on many MongoDb pods in a kubernetes cluster.


Make sure to change KUBE_CMD to the binary you use to control k8s (basically either "kubectl" for k8s or "oc" for an OpenShift cluster).

1. create_mongodbs
This script will create many pods of MongoDBs in your cluster. Make sure to provide the list of worker nodes via the WORKERS_LIST_FILE variable.
The rest of the variables are pretty self explanatory, you can play with how many pods of MongoDB will be created in every worker node, the requirements of CPU/RAM for each pod, size of PVC each MongoDB will use.
The script does not count on k8s to equally distribute the pods and uses a set of coron/uncordon commands to make sure all pods are equally spread.

2. run_ycsb_job-parallel
can be used by itself or via the "run_loops" wrapper scripts.
to load YCSB data on the previouslly x number of pods that were created, you can run "run_ycsb_job-parallel load load1".
to actually run YCSB benchmark, use "run_ycsb_job-parallel run some_directory"

3. run_loops
a wrapper script for run_ycsb_job-parallel so you can run many loops of the same test on all MongoDB pods.
The script also print the results via print_ycsb_results

4. print_ycsb_results
print results of a single run. You can either create a line ready for CSV file with the averages, or pretty print the averages in a nice and readable format.
