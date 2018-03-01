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
ms.openlocfilehash: d56dd69f4fc4513034046f9f721608ad94ff5cfe
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="azure-cosmosdb-libraries-for-python"></a><span data-ttu-id="84899-104">Bibliotecas de Azure CosmosDB para Python</span><span class="sxs-lookup"><span data-stu-id="84899-104">Azure CosmosDB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="84899-105">Información general</span><span class="sxs-lookup"><span data-stu-id="84899-105">Overview</span></span>

<span data-ttu-id="84899-106">Use CosmosDB en sus aplicaciones de Python para almacenar y consultar documentos JSON en un almacén de datos NoSQL.</span><span class="sxs-lookup"><span data-stu-id="84899-106">Use CosmosDB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="84899-107">Más información sobre [Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="84899-107">Learn more about [Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="84899-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="84899-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="84899-109">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="84899-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="84899-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="84899-110">Example</span></span>

<span data-ttu-id="84899-111">Busque documentos coincidentes en CosmosDB mediante una interfaz de consulta similar a SQL:</span><span class="sxs-lookup"><span data-stu-id="84899-111">Find matching documents in CosmosDB using a SQL-like query interface:</span></span>

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
> [<span data-ttu-id="84899-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="84899-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a><span data-ttu-id="84899-113">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="84899-113">Samples</span></span>

[<span data-ttu-id="84899-114">Desarrollo de una aplicación de Python con la API de DocumentDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="84899-114">Develop a Python app using Azure Cosmos DB's DocumentDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


