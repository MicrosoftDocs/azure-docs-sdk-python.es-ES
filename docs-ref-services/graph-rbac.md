---
title: Bibliotecas Graph RBAC para Python
description: Referencia de las bibliotecas Graph RBAC para Python
keywords: Azure, Python, SDK, API, Graph RBAC
author: rloutlaw
ms.author: routlaw
manager: jfriend
ms.date: 05/10/2019
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: e9b0aba7998565284ae18e0036da96d033b2b05f
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534275"
---
# <a name="azure-active-directory-graph-libraries-for-python"></a><span data-ttu-id="926fd-104">Bibliotecas de Azure Active Directory Graph para Python</span><span class="sxs-lookup"><span data-stu-id="926fd-104">Azure Active Directory Graph libraries for Python</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="926fd-105">A partir de febrero de 2019, comenzamos el proceso para dejar de utilizar algunas versiones anteriores de Azure Active Directory Graph API en favor de Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="926fd-105">As of February 2019, we started the process to deprecate some earlier versions of Azure Active Directory Graph API in favor of the Microsoft Graph API.</span></span> 
>
> <span data-ttu-id="926fd-106">Para más información, actualizaciones y plazos de tiempo, consulte [Microsoft Graph o Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) del centro de desarrollo de Office.</span><span class="sxs-lookup"><span data-stu-id="926fd-106">For details, updates, and time frames, see [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) in the Office Dev Center.</span></span>
>
> <span data-ttu-id="926fd-107">De ahora en adelante, las aplicaciones deben usar Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="926fd-107">Moving forward, applications should use the Microsoft Graph API.</span></span> 

## <a name="overview"></a><span data-ttu-id="926fd-108">Información general</span><span class="sxs-lookup"><span data-stu-id="926fd-108">Overview</span></span> 

<span data-ttu-id="926fd-109">Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-api).</span><span class="sxs-lookup"><span data-stu-id="926fd-109">Sign-on users and control access to applications and APIs with [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-api).</span></span>    

## <a name="client-library"></a><span data-ttu-id="926fd-110">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="926fd-110">Client library</span></span>   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a><span data-ttu-id="926fd-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="926fd-111">Example</span></span> 
> [!NOTE]   
> <span data-ttu-id="926fd-112">Debe cambiar el parámetro de recurso a https://graph.windows.net al crear la instancia de credenciales.</span><span class="sxs-lookup"><span data-stu-id="926fd-112">You need to change the resource parameter to https://graph.windows.net while creating the credentials instance</span></span>    
 ```python  
from azure.graphrbac import GraphRbacManagementClient   
from azure.common.credentials import UserPassCredentials    
 credentials = UserPassCredentials( 
            'user@domain.com',      # Your user 
            'my_password',          # Your password 
            resource="https://graph.windows.net"    
    )   
 tenant_id = "myad.onmicrosoft.com" 
 graphrbac_client = GraphRbacManagementClient(  
    credentials,    
    tenant_id   
)   
``` 
<span data-ttu-id="926fd-113">El siguiente código crea un usuario, lo obtiene directamente y mediante filtrado de la lista y, a continuación, lo elimina.</span><span class="sxs-lookup"><span data-stu-id="926fd-113">The following code creates a user, get it directly and by list filtering, and then delete it.</span></span>   
```python   
from azure.graphrbac.models import UserCreateParameters, PasswordProfile    
 user = graphrbac_client.users.create(  
    UserCreateParameters(   
        user_principal_name="testbuddy@{}".format(MY_AD_DOMAIN),    
        account_enabled=False,  
        display_name='Test Buddy',  
        mail_nickname='testbuddy',  
        password_profile=PasswordProfile(   
            password='MyStr0ngP4ssword',    
            force_change_password_next_login=True   
        )   
    )   
)   
# user is a User instance   
self.assertEqual(user.display_name, 'Test Buddy')   
 user = graphrbac_client.users.get(user.object_id)  
self.assertEqual(user.display_name, 'Test Buddy')   
 for user in graphrbac_client.users.list(filter="displayName eq 'Test Buddy'"): 
    self.assertEqual(user.display_name, 'Test Buddy')   
 graphrbac_client.users.delete(user.object_id)  
```