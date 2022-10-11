# Base - Detalles de Recursos de la empresa





## Introducción







## Información estándar

- Se pueden crear derivadas: `Sí`
- Derivada principal: `Detalles de Recursos de la empresa`
- Autor de  la sección: `Ángel albaladejo`
- Descripción: 
- Casos de uso:
- Alternativa: 



## Comportamiento esperado de sus derivadas

-----

> Aunque no se vayan a utilizar, estas opciones deben ser implementadas en todas sus derivadas

1. Debe tener campo `Tipo` 
   Sirve para definir el tipo, por ejemplo, un Recurso puede ser un coche, aquí seria los detalles del coche. O Tipo de contenedor.  *Para implementarlo, hay que crear su derivada oportuna.*

2. Debe tener campo `Foto`. 
   Este es importante para saber qué se puede hacer: ¿Vender? ¿Desmontar?. Si una empresa no lo usa, puede crear un tipo usar siempre el mismo.  *Para implementarlo, hay que crear su derivada oportuna.*

3. Debe tener pestaña `Compra y Venta`

4. Funcionalidad de peso. 

   1. El campo medida debe rellenarse inicialmente con el valor kilogramos


   3. El campo Medida peso debe filtrarse en medidas de tipo gramos
      Script en Evento `Filtro desplegable` del campo `Peso (Medida)`, nombre `Filtrado de peso`

      ```python
      F.CampoDesplegableAplicarFiltro(S.Campos.UnidadesDeMedidaBase.EsPeso.id, '=', 1)
      ```

   