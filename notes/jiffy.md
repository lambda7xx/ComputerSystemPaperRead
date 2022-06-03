## Introduce

This works foucs on the memory elastic for stateful serverless .To achieve the memory elastic ,jiffy design and implement three mechanism 1)Hierarchical Addressing 2)3.2 Data Lifetime Management 3)3.3 Flexible Data Repartitioning.Also ,it support some data structure like file,kv store and others. The architecture of jiffy is similar to Pocket(OSDI18).

## Question
- how to achieve the memory eleasic
- what's the experiment result of jiffy
- what's the disadvantage of jiffy

## Design 

The analytics job can represent  as a directed acyclic graph (DAG) where nodes correspond to computation
tasks (implemented as serverless functions), while edges denote intermediate data exchange between them ,as we can see in the Fig 3.

### Hierarchical Addressing
Jiffy use the idea from Internet hierarchical IP addressing mechanism that captures network structure,which is called Hierarchical Addressing , it organizes the analytic job as a tree.Each task has its own address. (Note:some task may have multiple address if it has mutliple parent node,like the T7/T5/T6 in Fig 4)

By use this mechanism ,Jiffy can provide isolation at task granularity because different task has different name address.


### Data Lifetime Management

Previous work foucs on the job level resource allocation, which means only the  job is done, the system can reclaim the storage that the job use, which is coarse-grained.But Jiffy can provide fine-grained  data management .


#### Jiffy achieves this by integrating well-known lease management mechanisms  with hierarchical addressing to enable lifetime management of intermediate data. 
- Update the lease:when one task is running ,it will send message to its' parent and its' children node and the node receive the message,the node will update its lease respectively.


- when the lease of one task is expired,Jiffy reclaims all memory allocated to the node after fulshing the data to persistent storage


## Evaluation 
As we can  see the Fig.9,when the memory capacity decrease, Jiffy can ensure the  good job performance and high resource utilization 




