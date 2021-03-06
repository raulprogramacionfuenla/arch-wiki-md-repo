**Estado de la traducción**
Este artículo es una traducción de [InfluxDB](/index.php/InfluxDB "InfluxDB"), revisada por última vez el **2018-08-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=InfluxDB&diff=0&oldid=533358) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Telegraf](/index.php/Telegraf "Telegraf")
*   [Grafana](/index.php/Grafana "Grafana")

InfluxDB es una base de datos de series de tiempo construida desde cero para manejar altas cargas de escritura y consultas. Es la segunda pieza de la [pila TICK](https://www.influxdata.com/time-series-platform/). InfluxDB está destinado a ser utilizado como una almacenamiento de reserva para cualquier tipo de uso que involucre grandes cantidades de datos con marcas de tiempo, incluyendo la supervisión DevOps, métricas de aplicaciones, datos de sensores IoT y análisis en tiempo real. Para obtener información más detallada, véase la [documentación oficial](https://docs.influxdata.com/influxdb/).

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
*   [3 Utilización](#Utilización)
*   [4 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install "Install") el paquete [influxdb](https://www.archlinux.org/packages/?name=influxdb) y [active](/index.php/Enable "Enable") e [inicie](/index.php/Start "Start") el servicio `influxdb`.

**Advertencia:** La configuración predeterminada escucha en `*:8086` así que asegúrese de cambiar la configuración o habilitar las reglas del cortafuegos relevantes.

## Configuración

Toda la configuración se realiza en `/etc/influxdb/influxdb.conf`.

## Utilización

InfluxDB se puede usar como parte de la **pila TICK**. En esta configuración, los datos se escriben en la base de datos usando [Telegraf](/index.php/Telegraf "Telegraf"). **Kapacitor** y **Chronograf**. Luego usan la base de datos para enviar alertas y mostrar datos respectivamente.

También se puede usar con otros complementos de entrada, como por ejemplo [collectd](/index.php/Collectd "Collectd"). Otra herramienta para la visualización de datos es [Grafana](/index.php/Grafana "Grafana").

La operaciones con la base de datos se pueden hacer mediante su API HTTP, tanto para [escribir](https://docs.influxdata.com/influxdb/latest/guides/writing_data/) como para [consultar](https://docs.influxdata.com/influxdb/latest/guides/querying_data/).

## Véase también

*   [InfluxData](https://www.influxdata.com/)
*   [Github](https://github.com/influxdata/influxdb/)