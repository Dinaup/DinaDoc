 # Testeando sistema de Ventas

El sistema de Ventas de Dinaup, tiene estos sistemas críticos.




## Funcionalidades

### Precios e importes

1. Descuentos
2. IVA y Recargo de equivalencia.
3. Retenciones.
   1. Capital mobiliario
   2. Arrendamiento
4. Suplidos.
5. Arrendamientos
6. Emisión de Saldo y Descuento de saldo
7. En compras; % Deducción IVA, % Deducción IRPF.
8. Catálogo de precios
9. Moneda extranjera (Solo afecta en la impresión)
10. Venta/Compra de Recursos de la empresa
11. Venta/Compra de productos

### Cobros y pagos

1. Cobros de Venta
2. Pago de devoluciones de Venta
3. Pagos de Compras
4. Cobros de devoluciones de compra

### Stock e inventario

1. Productos sin Stock
2. Stock por lotes 
3. Stock sin lotes (Se crea un lote por defecto y se usa siempre ese)
4. Reservas
5. Salidas y entradas manuales
6. Salidas y entradas automáticas






## Cantidad de decimales

Los precios unitarios deben soportar 6 decimales y en caso de terminar en 5 se redondea hacia arriba.

| Precio unidad | Suma |      |
| ------------- | ---- | ---- |
| 0.995         | 1    |      |
| 0.994         | 0.99 |      |
| 0.999994      | 1    |      |

> El `precio unidad`,  `dto fijo unidad`, `saldo extra unidad`,   siempre debe soportar 6 decimales.  Se redondea en la suma que es cuando se multiplica por la cantidad de unidades.



## Bases imponibles e IVA 

Se puede configurar el IVA en el catálogo de precios, en cualquier caso, se pueden agregar hasta 3 tipos de IVA distintos + Exento por cada factura.

![image-20221007171513978](https://dinaup.dinaupfs.com/cdn/link/articulos/image-20221007171513978.png)

 En la pestaña `Detalles` debería verse así.![image-20221007171749679](https://dinaup.dinaupfs.com/cdn/link/articulos/image-20221007171749679.png)

> Los impuestos se asignan de manera descendente. 21%,10%,4% y exento.   Y nunca puede estar rellenada la Base imponible 2 si no está rellenada la Base imponible 1.





## Recargo de equivalencia

Para activar el recargo de equivalencia debe haber un checkbox en la pestaña `Parámetros`. Al activarlo se aplicará del mismo modo que se aplica el IVA, pero se almacenan en campos separados (Los terminados en `- Cuota R.E`)

![image-20221007172739072](https://dinaup.dinaupfs.com/cdn/link/articulos/image-20221007172739072.png)

| Concepto                            | Importe    |
| ----------------------------------- | ---------- |
| **Subtotal**                        | **400,00** |
| IVA 21% de 100,00                   | 21         |
| IVA 10% de 100,00                   | 10         |
| IVA 4% de 100,00                    | 4          |
| IVA 0% de 100,00                    | 0          |
| Recargo Equivalencia 5.2% de 100,00 | 5.2        |
| Recargo Equivalencia 1.4% de 100,00 | 1.4        |
| Recargo Equivalencia 0.5% de 100,00 | 0.5        |
| Recargo Equivalencia 0% de 100,00   | 0          |
| **TOTAL**                           | **442,10** |

## Retenciones

En la pestaña `Parámetros` está el campo de `Retención`.  Al seleccionarlo se aplicará en la factura. La retención se calcula basándose en el `Subtotal`.  Por lo que, siguiendo el ejemplo de la factura anterior, al seleccionar una retención de un  `19%`  *(19% de 400 = 76)*

![Dinaup, valor retención en factura](https://dinaup.dinaupfs.com/cdn/link/articulos/image-20221007173611378.png)

![Dinaup barra de totales con retención](https://dinaup.dinaupfs.com/cdn/link/articulos/image-20221007173636104.png)





## Descuentos 

Existen 3 formas de aplicar descuentos.

1. **Desde la factura.** 
   Tanto en compras como en ventas, pestaña `Parámetros`. 
   Únicamente acepta valores porcentuales. Este tipo de descuento realmente se aplica después individualmente por cada producto.
   - Venta: `Dto VIP %`,  `Dto Entidad %`, `Dto Tipo Entidad %`, `Dto General %`
   - Compras:    `Dto Entidad %`, `Dto General %`
2. **Desde los productos**. 
   En la ventana central del producto se puede indicar `Descuento fijo por unidad` y `Descuento %`
   Después en la pestaña de `Detalles` puedes ver un resumen de como han afectado los descuentos.
3. **Agregando fila en negativo.** 
   Si se desea agregar un descuento fijo general, por ejemplo ¡10€ de descuento en tu primera factura!.
   Una opción es agregar una fila en negativo. Para que compute como descuento la fila debe ser de tipo `Descuento`.
4. **Usando saldo promocional.**
   En la pestaña parámetros, hay un botón `Agregar saldo promocional` si se pulsa se agregará una fila en negativo. (El descuento por saldo, IVA, categoría... se configura desde empresas administradas) para que  compute como saldo promociona la fila debe ser de tipo `Saldo`

> Realmente los descuentos de factura se aplican por producto, están puestos en la factura para facilitar al usuario aplicar descuentos a todos los productos.





## Precios con impuestos incluidos

En la pestaña parámetros hay un campo que indica los precios son con o sin impuestos incluidos.

### La problemática de los decimales.

Si dejas `Impuestos incluidos` **DESMARCADO** verás que **no puedes vender un producto** por `100€` si a este le aplicas `21% de IVA`, ya que se redondea a 99.99€ o a 100.01€. *(Esto pasa en todos los sistemas,es algo matemático.)*



### Recargo de equivalencia e impuestos incluidos

Cuando se vende con recargo de equivalencia y se marca  `Impuestos incluidos` se entiende que el recargo de equivalencia no está incluido. Así que el cliente terminará pagando, el precio + Recargo de equivalencia.

## Suplidos 

Un gasto suplido básicamente es cuando en una factura te cobran el importe de otra factura. Por ejemplo, el asesor te cobra la factura del notario.
Para configurar un suplido, simplemente en tipo de fila puedes seleccionar una fila como  `Suplido` esto incrementará el `Total de la factura` por el importe indicado como suplido, pero:

- Los suplidos no pueden tener descuentos
- A los suplidos no se les aplica IVA ni Retenciones.
- El gasto suplido no afecta al campo `Total Operación`
- El total por gasto suplido se resume en un campo `Total suplido`

## Saldo promocional 

El % de emisión de saldo se configura en tipo de cliente.  

1. En ventas con impuestos **NO** incluidos: *El saldo se calcula sobre el subtotal*
2. En ventas con impuestos **SI** incluidos: *El saldo se calcula sobre el  ` Subtotal + IVA`    (No incluye: R.E, Suplidos, retenciones)*
3. No obtiene el saldo hasta que no se pague la venta.
4. El descuento por saldo APLICADO, aparece separado en BI
5. No puede aplicar tanto saldo, que deje la venta en negativo.
6. En ventas ordinarias, el saldo no puede estar en positivo
7. Cuando se agrega el saldo se debe bloquear TODO excepto Impuestos y precio unidad
8. Cuando se selecciona saldo, se debe asignar automáticamente con los valores indicados en empresas administradas: 
   1. Concepto
   2. Categoría
   3. Impuesto 



## Otras funcionalidades 

1. Al seleccionar el cliente se copia `Descuento de cliente %`, `Tipo de cliente`,  `Retención`,  `Datos fiscales`, `Moneda extranjera`, `Tipo de factura`, `Condiciones de pago`
2. Al seleccionar el Tipo de cliente se copia: `Dto Tipo entidad %`, `Dto VIP %`, `Dto General %` , `Saldo %`
3. Al agregar un producto a la lista:  
   1. Cantidad = 1
   2. Concepto = Sin concepto
4. Al seleccionar un producto:
   1. Se copia el nombre al concepto
   2. Se copia la categoría de venta
   3. Se copia peso
5. Al seleccionar un recurso
   1. Se copia el nombre al concepto
   2. Se copian los precios de venta
   3. Se copia el peso
