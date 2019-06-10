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
ms.openlocfilehash: 27238e00463ae30ec0e47e8c18497ffb9edac62c
ms.sourcegitcommit: 253c8d4b3dbc2bb76d1a273a757ab96ba37617a1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65731541"
---
# <a name="azure-active-directory-graph-libraries-for-python"></a>Bibliotecas de Azure Active Directory Graph para Python

> [!IMPORTANT]
>
> A partir de febrero de 2019, comenzamos el proceso para dejar de utilizar algunas versiones anteriores de Azure Active Directory Graph API en favor de Microsoft Graph API. 
>
> Para más información, actualizaciones y plazos de tiempo, consulte [Microsoft Graph o Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) del centro de desarrollo de Office.
>
> De ahora en adelante, las aplicaciones deben usar Microsoft Graph API. 

## <a name="overview"></a>Información general 

Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-apis).   

## <a name="client-library"></a>Biblioteca de cliente   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a>Ejemplo 
> [!NOTE]   
> Debe cambiar el parámetro de recurso a https://graph.windows.net al crear la instancia de credenciales.    
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
El siguiente código crea un usuario, lo obtiene directamente y mediante filtrado de la lista y, a continuación, lo elimina.   
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