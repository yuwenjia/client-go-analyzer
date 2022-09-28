# client-go-analyzer
分析indexer里面的数据结构：

1. 生成索引的函数
type Indexers map[string]IndexFunc
value: IndexFunc：MetaNamespaceIndexFunc
key:   namespace

集群的资源根据namespace进行划分

2. 根据IndexFunc被划分后的结果存入Indices

type Indices map[string]Index

key 被IndexFunc 分后的key 例如： namespace 是default/kube-system等

2.1 type Index map[string]sets.String  存储哪个indexValue 如default/kube-system 下的资源名称索引


完整的流程是IndexFunc 进行index 的分割： 先使用MetaNamespaceIndexFunc将资源根据namespace作为索引的策略，然后将分割的结果装入Indices  [kube-system][kube-system][kubeapi-server等]  然后将资源对象存入  items map[string]interface{}中完成具体资源存储

