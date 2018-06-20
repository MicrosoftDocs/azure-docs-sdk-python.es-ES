---
title: Bibliotecas de Azure IoT Hub para Python
description: Referencia de las bibliotecas de Azure IoT Hub para Python
keywords: Azure, python, SDK, API, IoT Hub
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 0a1a5efa299f66ff8c31e8224e29dd7bcdc41783
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478778"
---
# <a name="azure-iot-hub-libraries-for-python"></a><span data-ttu-id="9f48f-104">Bibliotecas de Azure IoT Hub para Python</span><span class="sxs-lookup"><span data-stu-id="9f48f-104">Azure IoT Hub libraries for python</span></span>

## <a name="management-apipythonapioverviewazureiotmanagement"></a>[<span data-ttu-id="9f48f-105">API de administración</span><span class="sxs-lookup"><span data-stu-id="9f48f-105">Management API</span></span>](/python/api/overview/azure/iot/management)

```bash
pip install azure-mgmt-iothub
```

## <a name="create-the-management-client"></a><span data-ttu-id="9f48f-106">Creación del cliente de administración</span><span class="sxs-lookup"><span data-stu-id="9f48f-106">Create the management client</span></span>

<span data-ttu-id="9f48f-107">El código siguiente crea una instancia del cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="9f48f-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="9f48f-108">Debe proporcionar el valor de ``subscription_id``, que se puede obtener en [la lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="9f48f-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="9f48f-109">Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="9f48f-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.iothub import IotHubClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

iothub_client = IotHubClient(
    credentials,
    subscription_id
)
```

## <a name="create-an-iothub"></a><span data-ttu-id="9f48f-110">Creación de una instancia de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9f48f-110">Create an IoTHub</span></span>
```python
async_iot_hub = iothub_client.iot_hub_resource.create_or_update(
    'MyResourceGroup',
    'MyIoTHubAccount',
    {
        'location': 'westus',
        'subscriptionid': subscription_id,
        'resourcegroup': 'MyResourceGroup',
        'sku': {
            'name': 'S1',
            'capacity': 2
        },
        'properties': {
            'enable_file_upload_notifications': False,
            'operations_monitoring_properties': {
            'events': {
                "C2DCommands": "Error",
                "DeviceTelemetry": "Error",
                "DeviceIdentityOperations": "Error",
                "Connections": "Information"
            }
            },
            "features": "None",
        }
    }
)
iothub = async_iot_hub.result() # Blocking wait for creation
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9f48f-111">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="9f48f-111">Explore the Management APIs</span></span>](/python/api/overview/azure/iot/management)