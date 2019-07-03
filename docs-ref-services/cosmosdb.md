---
title: Bibliotecas de Azure Cosmos DB para Python
description: Documentación de referencia de las bibliotecas de cliente de Python para Azure Cosmos DB
keywords: Azure, Python, SDK, API, SQL, base de datos, PostGres, Cosmos DB, NoSQL
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: bb5e2af6a28d9543cce0c1e80fab1575b78f8cfa
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534312"
---
# <a name="azure-cosmos-db-libraries-for-python"></a><span data-ttu-id="b58d5-104">Bibliotecas de Azure Cosmos DB para Python</span><span class="sxs-lookup"><span data-stu-id="b58d5-104">Azure Cosmos DB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="b58d5-105">Información general</span><span class="sxs-lookup"><span data-stu-id="b58d5-105">Overview</span></span>

<span data-ttu-id="b58d5-106">Use Azure CosmosDB en sus aplicaciones de Python para almacenar y consultar documentos JSON en un almacén de datos NoSQL.</span><span class="sxs-lookup"><span data-stu-id="b58d5-106">Use Azure Cosmos DB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="b58d5-107">Más información acerca de [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="b58d5-107">Learn more about [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="b58d5-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="b58d5-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="b58d5-109">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="b58d5-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="b58d5-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="b58d5-110">Example</span></span>

<span data-ttu-id="b58d5-111">Busque documentos coincidentes en Azure CosmosDB mediante una interfaz de consulta similar a SQL:</span><span class="sxs-lookup"><span data-stu-id="b58d5-111">Find matching documents in Azure CosmosDB using a SQL-like query interface:</span></span>

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python Azure Cosmos DB client
client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
# Create a database
db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })

# Create collection options
options = {
    'offerEnableRUPerMinuteThroughput': True,
    'offerVersion': "V2",
    'offerThroughput': 400
}

# Create a collection
collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)

# Create some documents
document1 = client.CreateDocument(collection['_self'],
    { 
        'id': 'server1',
        'Web Site': 0,
        'Cloud Service': 0,
        'Virtual Machine': 0,
        'name': 'some' 
    })

# Query them in SQL
query = { 'query': 'SELECT * FROM server s' }    

options = {} 
options['enableCrossPartitionQuery'] = True
options['maxItemCount'] = 2

result_iterable = client.QueryDocuments(collection['_self'], query, options)
results = list(result_iterable)

print(results)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="b58d5-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="b58d5-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a><span data-ttu-id="b58d5-113">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="b58d5-113">Samples</span></span>

* [<span data-ttu-id="b58d5-114">Desarrollo de una aplicación de Python para acceder a los datos almacenados en la cuenta de SQL API de Azure Cosmos DB y administrarlos</span><span class="sxs-lookup"><span data-stu-id="b58d5-114">Develop a Python app to access and manage data stored in Azure Cosmos DB SQL API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-python-getting-started.git)

* [<span data-ttu-id="b58d5-115">Desarrollo de una aplicación de Python para acceder a los datos almacenados en la cuenta de MongoDB API de Azure Cosmos DB y administrarlos</span><span class="sxs-lookup"><span data-stu-id="b58d5-115">Develop a Python app to access and manage data stored in Azure Cosmos DB MongoDB API account</span></span>](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git)

* [<span data-ttu-id="b58d5-116">Desarrollo de una aplicación de Python para acceder a los datos almacenados en la cuenta de Gremlin API de Azure Cosmos DB y administrarlos</span><span class="sxs-lookup"><span data-stu-id="b58d5-116">Develop a Python app to access and manage data stored in Azure Cosmos DB Gremlin API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git)

* [<span data-ttu-id="b58d5-117">Desarrollo de una aplicación de Python para acceder a los datos almacenados en la cuenta de Cassandra API de Azure Cosmos DB y administrarlos</span><span class="sxs-lookup"><span data-stu-id="b58d5-117">Develop a Python app to access and manage data stored in Azure Cosmos DB Cassandra API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git)

* [<span data-ttu-id="b58d5-118">Desarrollo de una aplicación de Python para acceder a los datos almacenados en la cuenta de Table API de Azure Cosmos DB y administrarlos</span><span class="sxs-lookup"><span data-stu-id="b58d5-118">Develop a Python app to access and manage data stored in Azure Cosmos DB Table API account</span></span>](https://github.com/Azure-Samples/storage-python-getting-started.git)


