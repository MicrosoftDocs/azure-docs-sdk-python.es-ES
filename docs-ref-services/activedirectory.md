---
title: Bibliotecas de Azure Active Directory para Python
description: Documentación de referencia de la biblioteca de cliente Azure Active Directory para Python
keywords: Azure, Python, SDK, API, SQL, autenticación, AAD, Active Directory , Graph, OAuth 2.0
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.openlocfilehash: 4cf4149dfbd8209020e3affc0d15ab870f8d9697
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276749"
---
# <a name="azure-active-directory-libraries-for-python"></a>Bibliotecas de Azure Active Directory para Python

## <a name="overview"></a>Información general

Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con [Azure Active Directory](/azure/active-directory/active-directory-whatis).

## <a name="client-library"></a>Biblioteca de cliente

Configure la autenticación de OAuth2, OpenID Connect o Active Directory Graph y el inicio de sesión único [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) con la [biblioteca de autenticación de Azure Active Directory (ADAL) para Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).

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

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/python/api/overview/azure/activedirectory/client)

Vea más [ejemplos de código de Python para Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python) que puede usar en sus aplicaciones.
