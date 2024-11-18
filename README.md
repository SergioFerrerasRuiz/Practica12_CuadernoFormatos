# Formatos de datos
Los archivos que manejamos dia a dia tienen diferentes extensiones o formatos, pero ¿Alguna vez te has preguntado porque esos archivos tienen ese formato?.
En este documento se explicaran formatos como CSV, XMl, JSON, AVRO, PARQUET entre otros.
## CSV (Comma Separated Values)
Es un tipo de formato de datos que requiere que cada elemento de nuestro cojunto se presente en una línea. Dentro de esa línea cada uno de los atributos del elemento deben estar separados por un único separador (normalmente se usa una coma), además, el formato deberá seguir siempre el mismo orden. La primera línea del fichero, a la que llamaremos ``cabecera``, no contiene datos de ningún elemento, sino información de los atributos. Si el campo contiene alguna coma, utilizaremos un delimitador como por ejemplo " ". Es por eso por lo que el formato sigue un orden, porque tiene que hacer referencia a la cabezera y cuadrar con ella.

Ejemplo de CSV:
```bash
ID,Nombre,Precio,Cantidad,En_Stock
1,Camiseta,19.99,50,Sí
2,Pantalones,29.99,30,Sí
3,Zapatos,49.99,20,No
4,Gorra,9.99,100,Sí
5,Sudadera,39.99,15,No
```

## XML (Extensive Markup Languaje)
Es un lenguaje de etiquetas utilizado para almacenar datos de forma estructurada y visual. Los objetos están organizados en ``etiquetas``. Estas etiquetas funcionan como contenedores de información y son personalizables. Ademas ``XML`` permite anidar etiquetas, creando una estructura jerárquica. Esto es útil para representar relaciones entre los datos. Es fácil de entender porque las etiquetas describen su contenido y se permite el uso de atributos en las etiquetas para agregar más contexto.

Ejemplo de XML:
```bash
<agenda>
    <contacto id="1" tipo="personal">
        <nombre>Ana García</nombre>
        <telefono>+34 612 345 678</telefono>
        <email>ana.garcia@email.com</email>
    </contacto>
    <contacto id="2" tipo="trabajo">
        <nombre>Juan Pérez</nombre>
        <telefono>+34 689 876 543</telefono>
        <email>juan.perez@empresa.com</email>
    </contacto>
</agenda>
```

## JSON (JavaScript Object Notation)
Formato muy utilizado hoy en día, tiene el mismo propósito que el ``XML``,  el intercambio de datos aunque este formato, no utiliza las etiquetas
abiertas y cerradas, sino que pretende que ocupe menos espacio, para ello:
Los objetos se representan mediante llaves ``{}`` y contienen pares de ``clave-valor``, donde la clave es una cadena de texto que va entre commillas ``""`` y el valor puede ser un booleano, int, String.... 
Por otra parte, los Arrays, se representan con corchetes ``[]`` y contienen una lista ordenada de valores.

Ejemplo de JSON:
```bash
{
  "nombre": "Juan Pérez",
  "edad": 30,
  "correo": "juan.perez@example.com",
  "esActivo": true,
  "hobbies": ["leer", "viajar", "programar"],
  "direccion":  {
                    "calle": "123 Calle Principal",
                    "ciudad": "Ciudad Ejemplo",
                    "codigoPostal": "12345"
                }
}

```

## AVRO 
Formato de almacenamiento basado en filas para Hadoop. ``Avro`` se basa
en esquemas. Cuando los datos .avro son leídos siempre está presente el esquema con el que han sido escritos. Avro utiliza ``JSON`` para definir tipos de datos y protocolos. Es el formato utilizado para la serialización de datos ya que es más rápido y ocupa menos espacio que los ``JSON``, la serialización de los datos la hace en un formato ``binario compacto``.

## PARQUET
Formato de almacenamiento basado en columnas para ``Hadoop`` creado para disponer de un formato de compresión y codificación eficiente. El formato
Parquet está compuesto por tres piezas:
- ``Row group``: es un conjunto de filas en formato columnar.

- ``Column chunk``: son los datos de una columna en grupo. Se puede leer de
manera independiente para mejorar las lecturas.

- ``Page``: es donde finalmente se almacenan los datos, debe ser lo
suficientemente grade para que la compresión sea eficiente.



---
# PARENTESIS PARA PREGUNTA EN CLASE
Esto es copia y pega de los apuntes del teacher
---
## Formatos de datos a detalle
Conforme los datos viajan a través de los diferentes pipelines, los ingenieros de datos deben gestionar la serialización en diferentes formatos y ser capaces de convertir unos en otros.

Las propiedades que ha de tener un formato de datos son:
- independiente del lenguaje
- expresivo, con soporte para estructuras complejas y anidadas
- eficiente, rápido y reducido
- dinámico, de manera que los programas puedan procesar y definir nuevos tipos de datos.
- formato de fichero standalone y que permita dividirlo y comprimirlo.

Para que Hadoop/Spark o cualquier herramienta de analítica de datos pueda procesar documentos, es imprescindible que el formato del fichero permita su división en fragmentos (splittable in chunks).

Si los clasificamos respecto al formato de almacenamiento tenemos formatos de tipo:
- texto (más lentos, ocupan más pero son más expresivos y permiten su
interoperabilidad): CSV, XML, JSON, etc...
- binario (mejor rendimiento, ocupan menos, menos expresivos): Avro,
Parquet, ORC, etc...

Si comparamos los formatos más empleados a partir de las propiedades descritas tenemos:

Las ventajas de elegir el formato correcto son:
- Mayor rendimiento en la lectura y/o escritura
- Ficheros troceables (splittables)
- Soporte para esquemas que evolucionan
- Soporte para compresión de los datos (por ejemplo, mediante Snappy).

## Filas vs Columnas
Los formatos con los que estamos más familiarizados, como son CSV, XML o JSON, son formatos basados en filas, donde cada registro se almacena en una fila o documento. Estos formatos son más lentos en ciertas consultas y su almacenamiento no es óptimo.
### JSON vs JSONL
Un documento JSON contiene diferentes pares de clave-valor con los elementos que lo componen ocupando varias líneas.

Un tipo específico de JSON es JSON (JSON Lines), el cual almacena una secuencia de objetos JSON delimitando cada objeto por un saldo de línea.

