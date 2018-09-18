### Big data : 
	Big data refers to large data sets that are challenging to store,search,share,visualize and analyze.
  In distributed environmet, if the size of the file is more then  we split the file into chunks and store in multipule machines.

Hadoop solves how to store the big data, process it.So that it takes less time to complete.

### Bigdata-attributes :
	volume  	    : size of the data
 	Variety(Formats)    : Relational data, Text data, xml, Graph data(Social Network), 
	Velocity 	    : Data is generated fast and handled fast.

### Best Thing about Hadoop :
	Bring code to data rather data to code.
	Reliable : Because same data would replicated in multiple places  

### Hadoop components : 
	Hadoop distrubuted file system 
	Map Reduce

***Hadoop Cluster*** : It is a special type of computational cluster designed for storing and analyzing the huge amounts of unstructered data in a distributed computational environament
HDFS 	       : HDFS is a file system designed for storing very large files with streaming data access pattern, running on clusters of commidity hardware. 

### HDFS Features  :
	Block file system 
	Block size is 64MB or 128 MB. It reduces the disk read time because we directly read the entire 64MB at a time. Normal file system block size is 1KB.
	Hardware failures
	Streaming data access
### Write operation in hadoop

![hadoop_write_operation - copy](https://user-images.githubusercontent.com/40027047/45700848-3b079100-bb8b-11e8-9cfb-28aa41f84c01.png)

i) The HDFS client sends a create request on DistributedFileSystem APIs.

ii) DistributedFileSystem makes an RPC call to the namenode to create a new file in the file system’s namespace. The namenode performs various checks to make sure that the file doesn’t already exist and that the client has the permissions to create the file. When these checks pass, then only the namenode makes a record of the new file; otherwise, file creation fails and the client is thrown an IOException. Also Learn Hadoop HDFS Architecture in Detail.

iii) The DistributedFileSystem returns a FSDataOutputStream for the client to start writing data to. As the client writes data, DFSOutputStream splits it into packets, which it writes to an internal queue, called the data queue. The data queue is consumed by the DataStreamer, whichI is responsible for asking the namenode to allocate new blocks by picking a list of suitable datanodes to store the replicas.

iv) The list of datanodes form a pipeline, and here we’ll assume the replication level is three, so there are three nodes in the pipeline. The DataStreamer streams the packets to the first datanode in the pipeline, which stores the packet and forwards it to the second datanode in the pipeline. Similarly, the second datanode stores the packet and forwards it to the third (and last) datanode in the pipeline. Learn HDFS Data blocks in detail.

v) DFSOutputStream also maintains an internal queue of packets that are waiting to be acknowledged by datanodes, called the ack queue. A packet is removed from the ack queue only when it has been acknowledged by the datanodes in the pipeline. Datanode sends the acknowledgment once required replicas are created (3 by default). Similarly, all the blocks are stored and replicated on the different datanodes, the data blocks are copied in parallel.

vi) When the client has finished writing data, it calls close() on the stream.

vii) This action flushes all the remaining packets to the datanode pipeline and waits for acknowledgments before contacting the namenode to signal that the file is complete. The namenode already knows which blocks the file is made up of, so it only has to wait for blocks to be minimally replicated before returning successfully.

### Hadoop consists
Master Service
- Name node
- Secondary name node
- Job Tracker

slave service
- Data Node
- Task Tracker
	
Each node in the cluster send the heart beat to name node so that it will keep the note of which node is alive or dead. If a node is dead, it will put corresponding data into the another system.

Reason behind the keeping the 64mb as block size is Metadata size will be less in the namenode.

Reason behind the keeping the 64mb as block size is Metadata size will be less in the namenode.

### Data processing:
	Traditional way of processing the data is brought the data to code.But hadoop send the code towards the data.Reason is suppose you have 50GB data, then getting the 50GB into the RAM and processing will take the more time. Instead send the code to datanode that will execute the code and get back to with result.


