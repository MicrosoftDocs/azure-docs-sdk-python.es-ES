---
title: Bibliotecas de Azure Cosmos DB para Python
description: Documentación de referencia de las bibliotecas de cliente de Python para Azure Cosmos DB
keywords: Azure, Python, SDK, API, SQL, base de datos, PostGres, Cosmos DB, NoSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: 391b556ece7d818406fa501763814eb7f0d50d22
ms.sourcegitcommit: 41e6e6b5469271f4ec497a322b460e2a2af2c73d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="azure-cosmos-db-libraries-for-python"></a>Bibliotecas de Azure Cosmos DB para Python

## <a name="overview"></a>Información general

Use Azure CosmosDB en sus aplicaciones de Python para almacenar y consultar documentos JSON en un almacén de datos NoSQL.

Más información acerca de [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

## <a name="client-library"></a>Biblioteca de cliente
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>Biblioteca de administración
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>Ejemplo

Busque documentos coincidentes en Azure CosmosDB mediante una interfaz de consulta similar a SQL:

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
> [Explorar las API de administración](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a>Ejemplos

[Desarrollo de una aplicación de Python con Azure Cosmos DB](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


