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
# <a name="azure-active-directory-libraries-for-python"></a><span data-ttu-id="1bede-104">Bibliotecas de Azure Active Directory para Python</span><span class="sxs-lookup"><span data-stu-id="1bede-104">Azure Active Directory libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="1bede-105">Información general</span><span class="sxs-lookup"><span data-stu-id="1bede-105">Overview</span></span>

<span data-ttu-id="1bede-106">Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span><span class="sxs-lookup"><span data-stu-id="1bede-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

## <a name="client-library"></a><span data-ttu-id="1bede-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="1bede-107">Client library</span></span>

<span data-ttu-id="1bede-108">Configure la autenticación de OAuth2, OpenID Connect o Active Directory Graph y el inicio de sesión único [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) con la [biblioteca de autenticación de Azure Active Directory (ADAL) para Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).</span><span class="sxs-lookup"><span data-stu-id="1bede-108">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).</span></span>

```bash
pip install azure-graphrbac
```

### <a name="example"></a><span data-ttu-id="1bede-109">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1bede-109">Example</span></span>
> [!NOTE]
> <span data-ttu-id="1bede-110">Debe cambiar el parámetro de recurso a https://graph.windows.net al crear la instancia de credenciales.</span><span class="sxs-lookup"><span data-stu-id="1bede-110">You need to change the resource parameter to https://graph.windows.net while creating the credentials instance</span></span>

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
<span data-ttu-id="1bede-111">El siguiente código crea un usuario, lo obtiene directamente y mediante filtrado de la lista y, a continuación, lo elimina.</span><span class="sxs-lookup"><span data-stu-id="1bede-111">The following code creates a user, get it directly and by list filtering, and then delete it.</span></span>
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
> [<span data-ttu-id="1bede-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="1bede-112">Explore the Client APIs</span></span>](/python/api/overview/azure/activedirectory/client)

<span data-ttu-id="1bede-113">Vea más [ejemplos de código de Python para Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1bede-113">Explore more [sample Python code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python) you can use in your apps.</span></span>
