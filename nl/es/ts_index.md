---

copyright:
  years: 2015, 2019
lastupdated: "2019-2-11"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:faq: data-hd-content-type='faq'}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Preguntas más frecuentes
{: #ts_cd}

Aquí encontrará respuestas a las preguntas más frecuentes sobre el uso de {{site.data.keyword.contdelivery_full}}.
{:shortdesc}


## He intentado añadir la integración de herramientas de GitHub a la cadena de herramientas. ¿Por qué no se añade la integración de herramientas?
{: #cannot_authorize_github}
{: faq}

Si {{site.data.keyword.Bluemix_notm}} no está autorizado para acceder a la cuenta de GitHub, la integración de herramientas no se añade a la cadena de herramientas.

Si configura la integración de herramientas de GitHub mientras crea la cadena de herramientas, siga estos pasos para autorizar a GitHub:

  1. En la sección Integraciones configurables, pulse **GitHub**.
  1. Si está creando la cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y {{site.data.keyword.Bluemix_notm}} no está autorizado para acceder a GitHub, pulse **Autorizar** para ir al sitio web de GitHub.
  1. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Autorizar aplicación** para permitir que {{site.data.keyword.Bluemix_notm}} acceda a su cuenta de GitHub.

Si ya tiene una cadena de herramientas, actualice la configuración de la integración de herramientas de GitHub:

 1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse sobre la cadena de herramientas para abrir la página Visión general correspondiente. Si lo prefiere, en la página Visión general de la app, tarjeta Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Visión general**.
 1. En la tarjeta GitHub, pulse el menú y pulse **Configurar**.
 1. Actualice los valores de configuración para autorizar a {{site.data.keyword.Bluemix_notm}} para acceder a GitHub. Pulse **Autorizar** para ir al sitio web de GitHub. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Autorizar aplicación** para permitir que {{site.data.keyword.Bluemix_notm}} acceda a su cuenta de GitHub.
 1. Cuando haya terminado de configurar los ajustes, pulse **Guardar integración**.


## He intentado crear una cadena de herramientas. ¿Por qué aparece un error?
{: #cannot_create_toolchain}
{: faq}

Al intentar crear una cadena de herramientas en una organización, si aparece el siguiente mensaje de error, elimine una o varias cadenas de su organización y, a continuación, cree la cadena de herramientas de nuevo.

`Esta organización contiene 200 cadenas de herramientas, que es el límite máximo. Antes de que pueda añadir otra cadena de herramientas, elimine una o varias cadenas de herramientas de la organización.`


## ¿Por qué la página Cadenas de herramientas muestra que se ha excedido el plan Lite del servicio de {{site.data.keyword.contdelivery_short}}?
{: #plan_exceeded}
{: faq}

{{site.data.keyword.contdelivery_short}} ofrece dos planes: Lite y Professional. Si tiene el plan Lite de {{site.data.keyword.contdelivery_short}}, puede utilizar cadenas de herramientas de forma gratuita, hasta los límites del plan. El mensaje de error indica que ha sobrepasado uno o más límites del plan Lite. Por ejemplo, puede superar el plan si tiene demasiados usuarios autorizados que están asociados a la instancia de servicio de {{site.data.keyword.contdelivery_short}}, o si ha ejecutado el número máximo de trabajos de {{site.data.keyword.deliverypipeline}}. Para obtener más información sobre los términos del plan, consulte [Limitaciones y uso del plan](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-limitations_usage){: new_window}.


## He creado una cadena de herramientas, ¿por qué la página Cadenas de herramientas muestra que se necesita un servicio de Continuous Delivery?
{: #service_required_resource_group}
{: faq}

Los términos del plan para la instancia de servicio de {{site.data.keyword.contdelivery_short}} que se encuentra en el mismo grupo de recursos u organización que la cadena de herramientas gestiona el uso de algunas de las integraciones de herramientas ({{site.data.keyword.deliverypipeline}}, Eclipse Orion {{site.data.keyword.webide}} y {{site.data.keyword.gitrepos}}) contenidas en el servicio. El mensaje de error indica que el grupo de recursos o la organización no contiene la instancia necesaria del servicio de {{site.data.keyword.contdelivery_short}}. Para obtener más información sobre los términos del plan, consulte [Limitaciones y uso del plan](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-limitations_usage){: new_window}.


## He creado una cadena de herramientas en una organización de Cloud Foundry, ¿por qué la página Cadenas de herramientas muestra que se necesita un servicio de Continuous Delivery?
{: #service_required_cloud_foundry}
{: faq}

Cuando se crea una cadena de herramientas en un grupo de recursos u organización que no tiene una instancia del servicio de {{site.data.keyword.contdelivery_short}}, la plataforma de la cadena de herramientas intenta crear automáticamente una instancia del servicio utilizando el plan Lite. El mensaje de error indica que la plataforma de la cadena de herramientas no ha podido crear la instancia de servicio.

Este error se puede producir al crear una cadena de herramientas en la región EE.UU. sur y en una organización de Cloud Foundry que no tenga todavía una instancia de {{site.data.keyword.contdelivery_short}}. En la región EE.UU. sur, debe crear todas las instancias nuevas del servicio {{site.data.keyword.contdelivery_short}} en grupos de recursos. 

Puede crear la cadena de herramientas en un grupo de recursos o crear la cadena de herramientas en una organización que ya tenga una instancia de {{site.data.keyword.contdelivery_short}}.
  

## He intentado desplegar una app en {{site.data.keyword.Bluemix_notm}}. ¿Por qué aparece un error?
{: #org_outofmemory}
{: faq}

Al intentar desplegar una app en {{site.data.keyword.Bluemix_notm}}, si obtiene el siguiente mensaje de error, la cantidad de memoria que queda en la organización es menor que la cantidad de memoria que necesita la app que quiere desplegar.

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

Puede aumentar la cuota de memoria de su cuenta o reducir la memoria que utilizan las apps. El máximo de cuota de memoria para una cuenta de prueba es de 2 GB. Para aumentar la cuota de memoria de su cuenta, convierta su cuenta de prueba en una cuenta de pago. Para obtener más información sobre cómo convertir su cuenta de prueba en una cuenta de pago, consulte [¿Cómo actualizo o cambio mi cuenta?](/docs/account?topic=account-accountfaqs#changeacct). Para reducir la memoria que utilizan las apps, utilice la consola de {{site.data.keyword.Bluemix_notm}} o la interfaz de línea de mandatos cf.

Si utiliza la consola de {{site.data.keyword.Bluemix_notm}}, siga estos pasos:

1. En el panel de control Apps, seleccione su app. Se abre la página de detalles de la app.
1. En el panel tiempo de ejecución, puede reducir el límite máximo de memoria o el número de instancias de la app, o ambos, para la app que desee.

Si utiliza la interfaz de la línea de mandatos cf, efectúe los pasos siguientes:

1. Compruebe cuánta memoria están utilizando las apps. El mandato cf apps lista todas las apps desplegadas en el espacio actual. También se visualiza el estado de cada app.

	  ```
	  cf apps
	  ```

1. Para reducir la cantidad de memoria que utiliza la app, puede reducir el número de instancias de la app, el límite máximo de memoria o ambos:

	  ```
	  cf push appname -p vía_acceso_app -i número_instancia -m límite_memoria
      ```
    
1. Reinicie la app para que se apliquen los cambios.


## He creado una app. ¿Por qué no se muestran los iconos de {{site.data.keyword.Bluemix_notm}} Live Sync en la barra de ejecución de Eclipse Orion Web IDE?
{: #ts_llz_lkb_3r}
{: faq}

![Barra de ejecución](images/webide_runbar_light.png)   

Al editar una app de Node.js en Web IDE, los iconos de {{site.data.keyword.Bluemix_notm}} de edición en directo, reinicio rápido y depuración no están disponibles en la barra de ejecución en estas circunstancias:


* El archivo `manifest.yml` no está almacenado en el nivel superior del proyecto.
* La app está almacenada en un subdirectorio en lugar de en la raíz, pero la vía de acceso al subdirectorio no está especificada en el archivo `manifest.yml`.
* La app no contiene un archivo `package.json`.


Si el archivo `manifest.yml` no está almacenado en la raíz, almacénelo allí. Si la app está almacenada en un subdirectorio, especifique la vía de acceso al subdirectorio en el archivo `manifest.yml`. Si la app no contiene un archivo `package.json`, cree uno que esté en el mismo directorio que la app.


## He pulsado una cadena de herramientas para ver su página Visión general. ¿Por qué no se carga la cadena de herramientas?
{: #toolchains_load}
{: faq}

Consulte la página Estado de {{site.data.keyword.Bluemix_notm}} para determinar si hay problemas conocidos que afecten a la plataforma {{site.data.keyword.Bluemix_notm}} y a los principales servicios en {{site.data.keyword.Bluemix_notm}}.

Para ver la página Estado, seleccione una de las dos opciones siguientes:

  * Inicie la sesión en la consola de {{site.data.keyword.Bluemix_notm}}. En la barra de menús, pulse **Soporte** y seleccione **Estado**. Compruebe la lista de recursos en busca del icono ![algunos problemas](../../get-support/images/some_issues.svg). Este icono podría indicar una parada.
  * Acceda directamente a [{{site.data.keyword.Bluemix_notm}} - Estado del sistema ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://cloud.ibm.com/status){: new_window}.

Para obtener más información sobre la página Estado de {{site.data.keyword.Bluemix_notm}}, consulte [Visualización del estado de {{site.data.keyword.Bluemix_notm}}](/docs/get-support?topic=get-support-viewing-cloud-status#viewing-cloud-status){: new_window}.


## He configurado una integración de herramientas para mi cadena de herramientas. ¿Por qué no se ha configurado?
{: #tool_integration_error}
{: faq}

Cuando añade una integración de herramientas, la cadena de herramientas se comunica con la herramienta representada mediante la integración de herramientas para suministrar los recursos necesarios y asociarlos con la cadena de herramientas. Si se produce un error durante el proceso de configuración o si la comunicación entre la cadena de herramientas y la herramienta no se establece correctamente, la integración de herramientas se coloca en un estado de error.

 ![Error de configuración](images/tool_setup_failed.png)

Puede intentar configurar de nuevo la integración de herramientas:

1. En su tarjeta de herramienta, mueva el cursor sobre el mensaje `Error de configuración` y pulse **Volver a configurar**.

 ![Botón Volver a configurar](images/tool_reconfigure.png)

1. Asegúrese de utilizar parámetros de configuración válidos. Si el error está causado por una configuración no válida, se muestra un mensaje de error; por ejemplo, `La integración se ha podido configurar. Compruebe la configuración y vuelva a intentarlo. Razón: api_key:fakeKey no válido`. Actualice los valores de la integración de herramientas y pulse **Guardar integración**.
1. Si el error está causado por un problema de comunicación, pulse **Guardar integración** para intentarlo de nuevo.
