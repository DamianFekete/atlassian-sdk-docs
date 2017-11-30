---
aliases:
- /server/framework/atlassian-sdk/adding-websudo-support-to-your-plugin-5242916.html
- /server/framework/atlassian-sdk/adding-websudo-support-to-your-plugin-5242916.md
category: devguide
confluence_id: 5242916
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5242916
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5242916
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/adding-websudo-support-to-your-plugin
new_url: /server/framework/atlassian-sdk/adding-websudo-support-to-your-plugin
platform: server
product: atlassian-sdk
subcategory: learning
title: Adding WebSudo support to your plugin
---
# Adding WebSudo support to your plugin

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p><a href="https://developer.atlassian.com/pages/viewpage.action?pageId=5242917">SAL 2.2</a> and later; <a href="/server/framework/atlassian-sdk/rest-plugin-2-2-release-notes">REST 2.2</a> and later.</p></td>
</tr>
</tbody>
</table>

 

Support for Secure Administrator Sessions (also called websudo) was added in Confluence 3.3 and JIRA 4.3. When an administrator who is logged into Confluence or JIRA attempts to access an administration function, they are prompted to log in again.  By default, Atlassian applications run with secure sessions enabled. Administrators can disable this feature. For information on how to do this, refer to the <a href="http://confluence.atlassian.com" class="external-link">administrative documentation</a> for your product and version.  

All the Atlassian applications will support WebSudo sessions at some point. As of SAL version 2.2 and REST 2.2 it is possible to enforce websudo from within a plugin if the host application supports it.

SAL 2.2 supports programmatic access to a `WebSudoManager` that you can use from within your [servlet](/server/framework/atlassian-sdk/servlet-plugin-module) or [servlet filter](/server/framework/atlassian-sdk/servlet-filter-plugin-module). As of version 2.2 of the Atlassian [REST plugin module](https://developer.atlassian.com/display/REST), you can add annotations to REST resources.

## Servlet Example

You can use the `com.atlassian.sal.api.websudo.WebSudoManager` to check for secure administrator sessions and to enforce the websudo protection for the current request.

The call to `WebSudoManager#enforceWebSudoProtection(javax.servlet.http.HttpServletRequest, javax.servlet.http.HttpServletResponse)` will cause the host application to  
redirect the user to an authentication form if, and only if, the current request is not WebSudo protected.

``` java
package com.example.myplugin.servlet;

import static com.google.common.base.Preconditions.checkNotNull;
// import [...]

public final class MyManagerServlet extends HttpServlet
{
    private final UserManager userManager;
    private final WebSudoManager webSudoManager;

    public MyManagerServlet(final UserManager userManager,
                            final WebSudoManager webSudoManager)
    {
        this.userManager = checkNotNull(userManager, "userManager");
        this.webSudoManager = checkNotNull(webSudoManager, "webSudoManager");
    }

    @Override
    public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException
    {
        // WebSudo
        try {
            webSudoManager.willExecuteWebSudoRequest(request);


            // This request will be WebSudo protected
            // Add your custom code here

        } catch(WebSudoSessionException wes) {
            webSudoManager.enforceWebSudoProtection(request, response);
        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException
    {
        // WebSudo

        try {
            webSudoManager.willExecuteWebSudoRequest(request);
            // This request will be WebSudo protected            // Add your custom code here

        } catch(WebSudoSessionException wes) {            // Send an error or redirect the user to the initial form.
            response.sendError(HttpServletResponse.SC_FORBIDDEN);
        }    }

}
```

## REST Example

SAL provides two annotations that you can use to control secure administrator sessions. You can apply the annotations on a package, type or method level.

The `com.atlassian.sal.api.websudo.WebSudoRequired` annotation will require websudo protection. On the other hand, `com.atlassian.sal.api.websudo.WebSudoNotRequired` allows REST resources to bypass websudo protection if this annotation is applied to a more specific element.

The following example adds a package level annotation that enforces websudo protection but allows the REST resource `ATestResource` to bypass it.

Enforce websudo protection for all the resources in the `com.example.myplugin.rest.resources.admin` package:

`com/example/myplugin/rest/resources/admin/package-info.java`:

``` java
@WebSudoRequired
package com.example.myplugin.rest.resources.admin;
import com.atlassian.sal.api.websudo.WebSudoRequired;
```

To exclude a resource, you can add the annotation `com.atlassian.sal.api.websudo.WebSudoNotRequired`:

``` java
@Path("/test/{key}")
@WebSudoNotRequired
public class ATestResource
{
    // [...]
    @GET
    public Response get(@PathParam("key") String key)
    {
        // ....
        return ...
    }
}
```

This prevents websudo protection from being enforced for the `ATestResource` REST resource.





















































































































































