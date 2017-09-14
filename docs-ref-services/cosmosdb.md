---
title: Bibliotecas de Azure CosmosDB para Python
description: "Documentación de referencia de las bibliotecas de cliente de Python para Cosmos DB"
keywords: Azure, Python, SDK, API, SQL, Database, PostGres, CosmosDB, NoSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/11/2017
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: 5382779d659f7c85e5ecbd304920e00b78a08a49
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmosdb-libraries-for-python"></a><span data-ttu-id="33fdb-104">Bibliotecas de Azure CosmosDB para Python</span><span class="sxs-lookup"><span data-stu-id="33fdb-104">Azure CosmosDB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="33fdb-105">Información general</span><span class="sxs-lookup"><span data-stu-id="33fdb-105">Overview</span></span>

<span data-ttu-id="33fdb-106">Use CosmosDB en sus aplicaciones de Python para almacenar y consultar documentos JSON en un almacén de datos NoSQL.</span><span class="sxs-lookup"><span data-stu-id="33fdb-106">Use CosmosDB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="33fdb-107">Más información sobre [Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="33fdb-107">Learn more about [Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="33fdb-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="33fdb-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="33fdb-109">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="33fdb-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="33fdb-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="33fdb-110">Example</span></span>

<span data-ttu-id="33fdb-111">Busque documentos coincidentes en CosmosDB mediante una interfaz de consulta similar a SQL:</span><span class="sxs-lookup"><span data-stu-id="33fdb-111">Find matching documents in CosmosDB using a SQL-like query interface:</span></span>

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python DocumentDB client
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
> [<span data-ttu-id="33fdb-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="33fdb-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/managementlibrary)

## <a name="samples"></a><span data-ttu-id="33fdb-113">Muestras</span><span class="sxs-lookup"><span data-stu-id="33fdb-113">Samples</span></span>

[<span data-ttu-id="33fdb-114">Desarrollo de una aplicación de Python con la API de DocumentDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="33fdb-114">Develop a Python app using Azure Cosmos DB's DocumentDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


