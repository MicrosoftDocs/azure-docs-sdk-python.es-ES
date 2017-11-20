---
title: Bibliotecas de Azure Monitor para Python
description: Referencia de las bibliotecas de Azure Monitor para Python
keywords: Azure, python, SDK, API, Monitor
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 04aeb24f5ed294f5862e2e1f1bc6319c317bb157
ms.sourcegitcommit: cd2d097f5e91aae1eb1cd5a238d3b49ac427fd64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="azure-monitoring-libraries-for-python"></a><span data-ttu-id="700e8-104">Bibliotecas de Azure Monitor para Python</span><span class="sxs-lookup"><span data-stu-id="700e8-104">Azure Monitoring libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="700e8-105">Información general</span><span class="sxs-lookup"><span data-stu-id="700e8-105">Overview</span></span> 
<span data-ttu-id="700e8-106">La supervisión proporciona datos para garantizar que la aplicación permanece en funcionamiento en un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="700e8-106">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="700e8-107">También ayuda a evitar posibles problemas o a solucionar los existentes.</span><span class="sxs-lookup"><span data-stu-id="700e8-107">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="700e8-108">Además, puede usar datos de supervisión para obtener un conocimiento más profundo sobre su aplicación.</span><span class="sxs-lookup"><span data-stu-id="700e8-108">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="700e8-109">Este conocimiento puede ayudarle a mejorar el rendimiento o mantenimiento de la aplicación, o a automatizar acciones que de lo contrario requerirían intervención manual.</span><span class="sxs-lookup"><span data-stu-id="700e8-109">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>

<span data-ttu-id="700e8-110">Más información sobre [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span><span class="sxs-lookup"><span data-stu-id="700e8-110">Learn more about Azure Monitor [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span></span> 

## <a name="installation"></a><span data-ttu-id="700e8-111">Instalación</span><span class="sxs-lookup"><span data-stu-id="700e8-111">Installation</span></span>
```bash
pip install azure-mgmt-monitor
```

## <a name="example---metrics"></a><span data-ttu-id="700e8-112">Ejemplo: métricas</span><span class="sxs-lookup"><span data-stu-id="700e8-112">Example - Metrics</span></span>
<span data-ttu-id="700e8-113">Este ejemplo obtiene las métricas de un recurso en Azure (máquinas virtuales, etc.).</span><span class="sxs-lookup"><span data-stu-id="700e8-113">This sample obtains the metrics of a resource on Azure (VMs, etc.).</span></span> <span data-ttu-id="700e8-114">Este ejemplo requiere al menos la versión 0.4.0 del paquete de Python.</span><span class="sxs-lookup"><span data-stu-id="700e8-114">This sample requires version 0.4.0 of the Python package at least.</span></span>

<span data-ttu-id="700e8-115">[Esta es la lista completa](https://msdn.microsoft.com/library/azure/mt743622.aspx) de las palabras clave disponibles para los filtros.</span><span class="sxs-lookup"><span data-stu-id="700e8-115">A complete list of available keywords for filters is available [here](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span></span>

<span data-ttu-id="700e8-116">[Estas son las métricas](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics) admitidas por tipo de recurso que hay disponibles.</span><span class="sxs-lookup"><span data-stu-id="700e8-116">Supported metrics per resource type is available [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span></span>

```python
import datetime
from azure.mgmt.monitor import MonitorManagementClient

# Get the ARM id of your resource. You might chose to do a "get"
# using the according management or to build the URL directly
# Example for a ARM VM
resource_id = (
    "subscriptions/{}/"
    "resourceGroups/{}/"
    "providers/Microsoft.Compute/virtualMachines/{}"
).format(subscription_id, resource_group_name, vm_name)

# create client
client = MonitorManagementClient(
    credentials,
    subscription_id
)

# You can get the available metrics of this specific resource
for metric in client.metric_definitions.list(resource_id):
    # azure.monitor.models.MetricDefinition
    print("{}: id={}, unit={}".format(
        metric.name.localized_value,
        metric.name.value,
        metric.unit
    ))

# Example of result for a VM:
# Percentage CPU: id=Percentage CPU, unit=Unit.percent
# Network In: id=Network In, unit=Unit.bytes
# Network Out: id=Network Out, unit=Unit.bytes
# Disk Read Bytes: id=Disk Read Bytes, unit=Unit.bytes
# Disk Write Bytes: id=Disk Write Bytes, unit=Unit.bytes
# Disk Read Operations/Sec: id=Disk Read Operations/Sec, unit=Unit.count_per_second
# Disk Write Operations/Sec: id=Disk Write Operations/Sec, unit=Unit.count_per_second

# Get CPU total of yesterday for this VM, by hour

today = datetime.datetime.now().date()
yesterday = today - datetime.timedelta(days=1)

metrics_data = client.metrics.list(
    resource_id,
    timespan="{}/{}".format(yesterday, today),
    interval='PT1H',
    metric='Percentage CPU',
    aggregation='Total'
)

for item in metrics_data.value:
    # azure.mgmt.monitor.models.Metric
    print("{} ({})".format(item.name.localized_value, item.unit.name))
    for timeserie in item.timeseries:
        for data in timeserie.data:
            # azure.mgmt.monitor.models.MetricData
            print("{}: {}".format(data.time_stamp, data.total))

# Example of result:
# Percentage CPU (percent)
# 2016-11-16 00:00:00+00:00: 72.0
# 2016-11-16 01:00:00+00:00: 90.59
# 2016-11-16 02:00:00+00:00: 60.58
# 2016-11-16 03:00:00+00:00: 65.78
# 2016-11-16 04:00:00+00:00: 43.96
# 2016-11-16 05:00:00+00:00: 43.96
# 2016-11-16 06:00:00+00:00: 114.9
# 2016-11-16 07:00:00+00:00: 45.4
```

## <a name="example---alerts"></a><span data-ttu-id="700e8-117">Ejemplo: alertas</span><span class="sxs-lookup"><span data-stu-id="700e8-117">Example - Alerts</span></span>
<span data-ttu-id="700e8-118">Este ejemplo muestra cómo configurar automáticamente las alertas en los recursos cuando se crean para asegurarse de que todos los recursos se supervisan correctamente.</span><span class="sxs-lookup"><span data-stu-id="700e8-118">This example shows how to automatically set up alerts on your resources when they are created to ensure that all resources are monitored correctly.</span></span>

<span data-ttu-id="700e8-119">Cree un origen de datos en una máquina virtual para que le alerte sobre el uso de la CPU:</span><span class="sxs-lookup"><span data-stu-id="700e8-119">Create a data source on a VM to alert on CPU usage:</span></span>
```python
from azure.mgmt.monitor import MonitorMgmtClient
from azure.mgmt.monitor.models import RuleMetricDataSource

resource_id = (
    "subscriptions/{}/"
    "resourceGroups/MonitorTestsDoNotDelete/"
    "providers/Microsoft.Compute/virtualMachines/MonitorTest"
).format(self.settings.SUBSCRIPTION_ID)

# create client
client = MonitorMgmtClient(
    credentials,
    subscription_id
)

# I need a subclass of "RuleDataSource"
data_source = RuleMetricDataSource(
    resource_uri = resource_id,
    metric_name = 'Percentage CPU'
)
```
<span data-ttu-id="700e8-120">Cree una condición de umbral que se desencadenará cuando el uso medio de la CPU de una máquina virtual durante los últimos 5 minutos sea superior al 90 % (con el origen de datos anterior):</span><span class="sxs-lookup"><span data-stu-id="700e8-120">Create a threshold condition that triggers when the average CPU usage of a VM for the last 5 minutes is above 90% (using the preceding data source):</span></span>
```python
from azure.mgmt.monitor.models import ThresholdRuleCondition

# I need a subclasses of "RuleCondition"
rule_condition = ThresholdRuleCondition(
    data_source = data_source,
    operator = 'GreaterThanOrEqual',
    threshold = 90,
    window_size = 'PT5M',
    time_aggregation = 'Average'
)
```

<span data-ttu-id="700e8-121">Cree una acción de correo electrónico:</span><span class="sxs-lookup"><span data-stu-id="700e8-121">Create an email action:</span></span>
```python
from azure.mgmt.monitor.models import RuleEmailAction

# I need a subclass of "RuleAction"
rule_action = RuleEmailAction(
    send_to_service_owners = True,
    custom_emails = [
        'monitoringemail@microsoft.com'
    ]
)
```

<span data-ttu-id="700e8-122">Cree la regla:</span><span class="sxs-lookup"><span data-stu-id="700e8-122">Create the alert:</span></span>
```python
rule_name = 'MyPyTestAlertRule'
my_alert = client.alert_rules.create_or_update(
    group_name,
    rule_name,
    {
        'location': 'westus',
        'alert_rule_resource_name': rule_name,
        'description': 'Testing Alert rule creation',
        'is_enabled': True,
        'condition': rule_condition,
        'actions': [
            rule_action
        ]
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="700e8-123">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="700e8-123">Explore the Management APIs</span></span>](/python/api/overview/azure/monitoring/managementlibrary)
