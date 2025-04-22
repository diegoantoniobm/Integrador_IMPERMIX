# Proyecto Integrador

## Integrantes

Daniel Aldana López 230110150
Diego Antonio Badillo Morales 230110025
Oswaldo Gabriel Villaverde Mendoza 230110856
Irving Maldonado Olguin 230110716

## ¿Cuál es la problematica?

IMPERMIX trabaja mediante cotizaciones generadas por un Ingeniero de campo de manera física, y notas de venta generadas en el centro de trabajo siendo estas también físicas, el problema radica en la ineficiencia de llevar este proceso de manera física al momento de hacer corte de operaciones al fin de mes, concretar una cotización, pues estos documentos al ser manipulados en campo (física) y por diferentes empleados suelen ser extraviados y por parte de los administradores hacer sus operaciones de contabilidad e inventarios resulta ser una tarea demasiado tediosa e ineficiente tomando en cuenta todos estos factores del día a día.

## ¿Cuál es la propuesta de solución?

El equipo Engineers 0.5 propone la implementación de tecnologías ingenieriles de TICS, para ayudar a la digitalización de las Notas de venta, y las cotizaciones, además en la observación de operaciones, los empleados comentan el uso de un almacén, este esta adecuado a cierta temperatura y humedad, en este se almacenan los productos y se ofrece la implementación de tecnologías Node-RED y uso de Internet de las cosas IOT para el monitoreo de este almacén. 

## ¿Como se implementara el proyecto?

La implementación del proyecto se llevará a cabo en varias fases:

**Fase 1: Análisis y Diseño:** Se definirán los requisitos específicos del software
y se diseñará la estructura de la base de datos. Se identificarán los datos
necesarios para cada aspecto del negocio y se establecerán las relaciones
entre ellos.

**• Fase 2: Desarrollo:** Se procederá con la programación del software, utilizando
tecnologías adecuadas para garantizar la eficiencia y seguridad del sistema.
Se desarrollarán funcionalidades específicas para el monitoreo de inventarios,
costos y precios de venta, así como para la gestión de costos de
mantenimiento y salarios.

**• Fase 3: Pruebas:** Se realizarán pruebas exhaustivas del software para detectar
y corregir errores. Se verificarán todas las funcionalidades y se asegurará que
el sistema cumpla con los requisitos definidos.

**• Fase 4: Implementación y Capacitación:** El software se instalará en los
dispositivos del negocio y se capacitará al personal para su uso. Se garantizará
que solo cuatro usuarios tengan privilegios de administrador para modificar
precios, mientras que los demás solo podrán subir cotizaciones.

## Desarrollo:

![Topología de red](imagen.png)

Segmentación de Red con VLSM (IPv4)
Vamos a partir de la red 192.168.0.0/24, que dispone de 256 direcciones IP posibles. Si necesitamos crear 5 grupos de trabajo sin desperdiciar direcciones, lo ideal es usar VLSM (Máscara de Subred de Longitud Variable).

🔢 Cálculo de direcciones necesarias por subred
Para determinar cuántos bits debemos reservar para los hosts, usamos esta lógica:

Buscamos la menor potencia de 2 que cubra los hosts deseados.

`2^n ≥ número de hosts requeridos`

Por ejemplo:

`2² = 4 es muy justo`

`2³ = 8 es suficiente`

Esto indica que necesitaremos 3 bits para los hosts, lo que nos deja con 8 IPs por subred, de las cuales 6 son útiles (una es la red y otra el broadcast).

### Nueva Máscara
Como usamos 3 bits para hosts, restamos eso a los 32 bits totales:

32 - 3 = 29 bits para red

Pero partimos de /24, así que sumamos esos 3 a la máscara base:

/27 = 255.255.255.224


### Cálculo de direcciones de red y broadcast

Cuando se divide una red en subredes más pequeñas, es fundamental identificar correctamente la dirección de red y la dirección de broadcast. Estas marcan el inicio y el final de cada subred.

La dirección de red se obtiene asignando cero a todos los bits del campo de host.

La dirección de broadcast se obtiene asignando uno a todos los bits del campo de host.

Esto nos permite determinar el rango de direcciones disponibles para los hosts en cada subred.

Dirección de Red

En una máscara /27, los últimos 5 bits corresponden a la parte de host. Si colocamos todos estos bits en 0, obtenemos:

| Posición de bits  |     |     |     | /27 |    |    |    |    |
|-------------------|-----|-----|-----|-----|----|----|----|----|
| Valor del bit     | 128 |  64 |  32 |  16 |  8 |  4 |  2 |  1 |
| Bits utilizados   |  0  |  0  |  0  |  0  |  0 |  0 |  0 |  0 |

Dirección de red resultante: 192.168.0.0
Esta dirección identifica a la subred y no debe asignarse a ningún host.

Dirección de Broadcast
Si colocamos unos en los mismos 5 bits de host:

| Posición de bits  |     |     |     | /27 |    |    |    |    |
|-------------------|-----|-----|-----|-----|----|----|----|----|
| Valor del bit     | 128 |  64 |  32 |  16 |  8 |  4 |  2 |  1 |
| Bits utilizados   |  0  |  0  |  0  |  1  |  1 |  1 |  1 |  1 |

Dirección de broadcast resultante: 192.168.0.31
Esta es la última dirección de la subred, utilizada para enviar mensajes a todos los dispositivos dentro de ella. Tampoco se asigna a un host.

#### Primera Subred:

- Dirección de red: `192.168.0.0`
- Primer host válido: `192.168.0.1`
- Último host válido: `192.168.0.30`
- Dirección de broadcast: `192.168.0.31`

IPs utilizables:  
`192.168.0.1` → `192.168.0.30`
