# Goal
Enable the CosmosDB Provider to support developer defined Partitions. This is needed for 2 reasons:
1. Part of the maturity & credibility story around using CosmosDB. Developers expect access to the Partition keys. 
2. Support (potentially) large bots.

# Compatability
Any solution must have defaults that are back-compatable with v4.0.X bots. This means any new functionality needs to be either additive, a new switch of some time, or fully back-compat. 

# Proposal
Allow developers, on each request, to participate in the data flow and specify a partition key. 

To accomplish this, the following DB related operations in CosmosDBStorage need to be updates:
1. DeleteAsync (C#), Delete (JS)
2. ReadAsync (C#), Read (JS)
3. WriteAsync (C#), Write(JS)

The proposal is to add a new class, PartitionedDocumentStoreItem, alongside DocumentStoreItem. To help insure compatability, this class would NOT be created using inheritence, and would instead simply be a new POCO/POJO. 
```cs
private class DocumentStoreItem
{
    [JsonProperty("partitionKey")]
    public string PartitionKey { get; set; }
    [JsonProperty("id")]
    public string Id { get; set; }
    [JsonProperty("realId")]
    public string ReadlId { get; internal set; }
    [JsonProperty("document")]
    public JObject Document { get; set; }
    [JsonProperty("_etag")]
    public string ETag { get; set; }
}
```
```js
interface DocumentStoreItem {
   partitionKey: string;
   id: string;
   realId: string;
   document: any;
}
```

## DB Initialization
A new "usePartitions" flag is added to the CosmosDbStorageOptions POCO/POJO. If set, the database is initialized as having the partition key in the document collection set to the PartitionKey path. 

```cs
var documentCollection = new DocumentCollection
{
    Id = _collectionId,
};
documentCollection.PartitionKey.Paths.Add("/partitionKey");
```
```js
let docCollection = client.createCollection(
    databaseLink, 
    { id: collectionId }, 
    (err2: any, collectionLink: any) => {
        if (err2) { return reject(err2); }
        resolve(collectionLink._self);
    });
docCollection.PartitionKey.Paths.Add("/partitionKey");
```

# Developer Participation
Developers inherit from CosmosDBStore and override the GetPartitionKey method. This is called on every read/write, and allows the developer to specify an arbitrary string. 
```cs
public overridable string GetPartitionKey(TurnContext context)
{
    return "someKey";
}
```
