# Base - Recursos de la empresa





## Introducción

Los recursos de la empresa son una sección similar a la de produ





## Información estándar

- Se pueden crear derivadas: `Sí`
- Derivada principal: `Recursos de la empresa`
- Autor de  la sección: `Ángel albaladejo`
- Descripción: 
- Casos de uso:
- Alternativa: 



## Comportamiento esperado de sus derivadas

-----

> Aunque no se vayan a utilizar, estas opciones deben ser implementadas en todas sus derivadas

1. Debe tener campo `Detalles` 
   Sirve para definir el tipo, por ejemplo, un Recurso puede ser un coche, aquí seria los detalles del coche. O Tipo de contenedor.  *Para implementarlo, hay que crear su derivada oportuna.*

2. Debe tener campo `Tipo`. 
   Este es importante para saber qué se puede hacer: ¿Vender? ¿Desmontar?. Si una empresa no lo usa, puede crear un tipo usar siempre el mismo.  *Para implementarlo, hay que crear su derivada oportuna.*

3. Debe tener campo `Estado`
   Para saber el estado del recurso. Si una empresa no lo usa, puede crear un estado y usar siempre el mismo.   *Para implementarlo, hay que crear su derivada oportuna.*

4. Pestaña de Localización.

5. Pestaña de Compra - Venta

6. Funcionalidad de peso. 

   1. El campo medida debe rellenarse inicialmente con el valor kilogramos

   2. Se debe copiar el peso del campo detalles (Si es superior a 0)
      Script en Evento `Campo cambiado` del campo `Detalles`, nombre `Copiar peso de detalles`

      ```python
      if C.ReferenciaDetalles <> ''
      	if C.ReferenciaDetalles.peso > 0
              C.Peso = C.ReferenciaDetalles.Peso 
              C.ReferenciaMedidaPeso = C.ReferenciaDetalles.ReferenciaMedidaPeso        
      	end if 
      end if 
      ```

   3. El campo Medida peso debe filtrarse en medidas de tipo gramos
		Script en Evento `Filtro desplegable` del campo `Peso (Medida)`, nombre `Filtrado de peso`
      
		```python
		F.CampoDesplegableAplicarFiltro(S.Campos.UnidadesDeMedidaBase.EsPeso.id, '=', 1)
	
	