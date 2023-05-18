![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Logotipo_de_la_Universidad_del_Norte.svg/512px-Logotipo_de_la_Universidad_del_Norte.svg.png)
## INFORMACIÓN DEL ESTUDIANTE
**Nombre:** Sebastián De Jesús Santos Vergara

**NRC:**  4519
* * *
## Dashboard de la actividad
[Looker studio](https://lookerstudio.google.com/reporting/ab3cfa3d-1283-43dc-a5fc-1e6a22607b46)
* * *
## PREGUNTA
### **_¿Cuál es el contaminante con mayor concentración total en cada estación?_**
Para responder esta pregunta se usó la siguiente consulta:

```sql
WITH contaminante_por_estacion AS (
SELECT Estacion, Par__metro AS Contaminante, SUM(CPM___g_m3) AS Total_Concentracion
FROM `is_act3.calidad del aire`
GROUP BY Estacion, Contaminante
),
contaminante_mayor_por_estacion AS (
SELECT Estacion, MAX(Total_Concentracion) AS Concentracion
FROM contaminante_por_estacion
GROUP BY Estacion
)
SELECT a.Estacion, a.Contaminante, a.Total_concentracion
FROM contaminante_por_estacion AS a
INNER JOIN contaminante_mayor_por_estacion b ON a.Total_Concentracion = b.Concentracion
ORDER BY a.Total_Concentracion DESC
```
en esta se utilizaron 2 subconsultas, la primera `contaminante_por_estacion` para obtener la concentración de cada contaminante registrado en una estación. En la segunda `contaminante_mayor_por_estacion` se obtienen la concentración de los mayores contaminantes en cada estación.

Con las subconsultas ya definidas se hace un `INNER JOIN` de las dos para así obtener el nombre de los contaminantes con mayor concentración en cada una de las estaciones
* * *
## DATASET UTILIZADO
[Dataset de datos abiertos](https://www.datos.gov.co/Ambiente-y-Desarrollo-Sostenible/Monitoreo-Calidad-de-Aire-departamento-del-Magdale/dgnf-6h7v)
* * *