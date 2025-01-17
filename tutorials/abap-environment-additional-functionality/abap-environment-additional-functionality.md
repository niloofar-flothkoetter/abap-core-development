---
parser: v2
auto_validation: true
primary_tag: software-product>sap-btp--abap-environment
tags: [  tutorial>beginner, programming-tool>abap-development, software-product>sap-business-technology-platform, software-product>sap-s-4hana-cloud ]
time: 30
author_name: Patrick Winkler
author_profile: https://github.com/sepp4me
---

# Explore additional features of the Custom Business Configurations app
<!-- description --> Learn how to copy and paste data from spreadsheet applications. Learn how to use intent navigation.

## Prerequisites  
- You need an SAP BTP, ABAP environment license or a [trial user](abap-environment-trial-onboarding).
- This tutorial also works in an SAP S/4HANA Cloud, public edition system.
- This is the fourth tutorial of group [Create a SAP Fiori based Table Maintenance app](group.abap-env-factory). You must complete the tutorials in the given order.


## You will learn  
- How to copy and paste data from spreadsheet applications
- How to use intent navigation

---
### Copy and paste data from spreadsheet applications


You can add multiple error codes by copying and pasting them from a [spreadsheet application](https://ui5.sap.com/#/topic/f6a8fd2812d9442a9bba2f6fb296c42e).

  1. Start the **Custom Business Configurations** app.

      ![Start Custom Business Configurations app](mc.png)

  2. Select your business configuration.

      ![Select business configuration](m2.png)

  3. Click **Edit**.

  4. Select **Export as**.

      ![Export as](spread2.png)

  5. Export current table content to spreadsheet:
     - File Name: **`ErrorCode###s`**
     - Format: **`Spreadsheet`**
     - Split cells with multiple values: **`true`**

  6. Open the downloaded file and **Enable Editing**.

  7. Add two new lines with the following data:
    - Error Code: **`403`**, Description: **`Forbidden`**
    - Error Code: **`404`**, Description: **`Not Found`**

  8. Select and copy both lines

  9. In the **Custom Business Configurations** app, click **Paste**.

      ![Paste new rows](spread6.png)

10. When prompted, click **Allow**.

11. After the insertion, the new lines are displayed. Select a transport and click **Save**.

      ![Save new rows](spread8.png)


### Make use of intent navigation


You want to navigate from your SAP Fiori app to the maintenance view of a business configuration maintenance object.

For this [intent navigation](https://help.sap.com/docs/BTP/65de2977205c403bbc107264b8eccf4b/76384d8e68e646d6ae5ce8977412cbb4.html#intent-navigation), you can use the parameter `TechnicalIdentifier` for the semantic object `BusinessConfiguration` with the action `maintain`.

- You can test this in the browser:
    - `/ui#BusinessConfiguration-maintain` navigates to the List Report of the **Custom Business Configurations** app.
    - `/ui#BusinessConfiguration-maintain?TechnicalIdentifier=ZERRORCODE###` directly navigates to the maintenance view of the Business Configuration Maintenance Object `ZERRORCODE###`
- In your SAP Fiori app, one option is to use [cross application navigation](https://sapui5.hana.ondemand.com/sdk/#/api/sap.ushell.services.CrossApplicationNavigation):


```JavaScript
sap.ushell.Container.getServiceAsync("CrossApplicationNavigation").then(function (oService) {
    oService.toExternal({
        target: {
            semanticObject: "BusinessConfiguration",
            action: "maintain"
        },
        params: {
            TechnicalIdentifier: "ZERRORCODE###"
        }
    });
});
```


### Test yourself



---
