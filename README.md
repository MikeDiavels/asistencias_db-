<div><b>Universidad Nacional Abierta y a Distancia UNAD</b><br/>
<b>Ingenieria de sistemas</b><br/>
<b>Curso Bigdata: 202016911A_2034</b><br/>
<b>Curso # 2</b><br/>
<b>Estudiante: Marcial Alberto Diaz Velaides</b><br/>
<b>Tutor: Jaime Rubiano LLorente</b><br/>

</div><br/>
<b>Sistema de registro de asistencia estudiantil</b><br/>
Este caso de uso se centra en la creación de un sistema para gestionar la asistencia de estudiantes en una institución educativa. El sistema debe permitir registrar la presencia, ausencia o tardanza de cada estudiante en distintos cursos y fechas. MongoDB es adecuado porque permite almacenar registros con diferentes cantidades de asistencias por estudiante, añadir observaciones opcionales, y manejar información variable sin requerir la rigidez de una base de datos relacional. El objetivo es facilitar consultas como asistencia por curso, porcentajes de asistencia, historial por estudiante y reportes para seguimiento académico.

<b>Diseño de la base de datos</b><br/>
La base de datos asistencias_db se divide en tres colecciones: estudiantes, cursos y asistencias. Los registros de asistencia se relacionan con estudiantes y cursos mediante identificadores, permitiendo almacenar fechas, estados y observaciones. El modelo documental facilita manejar múltiples asistencias por estudiante sin una estructura rígida.
<br/>
<br/>
<br/>
<b>Los datos a continuacion son datos dummy, generados para simular la base de datos en MONGODB</b>

<br/><b>Tabla 1</b> 
<br/><b>Colección: estudiantes</b>

<table>
  <thead>
    <th>Campo</th>
     <th>Tipo</th>
     <th>Descripción</th>
  </thead>
  <tbody>
    <tr>
      <td>_id</td>
       <td>ObjectId</td>
       <td>Identificador único</td>
    </tr>
     <tr>
      <td>codigo</td>
       <td>string</td>
       <td>Código institucional del estudiante</td>
    </tr>
     <tr>
      <td>nombre</td>
       <td>string</td>
       <td>Nombre completo</td>
    </tr>
     <tr>
      <td>programa</td>
       <td>string</td>
       <td>Programa académico</td>
    </tr>
  </tbody>
</table>

<br/><b>Tabla 2</b> 
<br/><b>Colección: cursos</b>

<table>
  <thead>
    <th>Campo</th>
     <th>Tipo</th>
     <th>Descripción</th>
  </thead>
  <tbody>
    <tr>
      <td>_id</td>
       <td>ObjectId</td>
       <td>Identificador único</td>
    </tr>
     <tr>
      <td>codigo</td>
       <td>string</td>
       <td>Código del curso</td>
    </tr>
     <tr>
      <td>nombre</td>
       <td>string</td>
       <td>Nombre de la asignatura</td>
    </tr>
     <tr>
      <td>docente</td>
       <td>string</td>
       <td>Nombre del profesor</td>
    </tr>
  </tbody>
</table>

<br/><b>Tabla 3</b> 
<br/><b>Colección: asistencias</b>

<table>
  <thead>
    <th>Campo</th>
     <th>Tipo</th>
     <th>Descripción</th>
  </thead>
  <tbody>
    <tr>
      <td>_id</td>
       <td>ObjectId</td>
       <td>Identificador único</td>
    </tr>
     <tr>
      <td>estudiante_id</td>
       <td>ObjectId</td>
       <td>Referencia al estudiante</td>
    </tr>
     <tr>
      <td>curso_id</td>
       <td>ObjectId</td>
       <td>Referencia al estudiante</td>
    </tr>
     <tr>
      <td>fecha</td>
       <td>date</td>
       <td>Fecha del registro</td>
    </tr>
     <tr>
      <td>estado</td>
       <td>string</td>
       <td>Presente / Ausente / Tarde</td>
    </tr>
    <tr>
      <td>observacion</td>
       <td>string</td>
       <td>Comentario opcional</td>
    </tr>
  </tbody>
</table>

1.1 Creación de base de datos, colecciones, campos y documentos
use asistencias_db<br/>
<br/>
Consulta 1<br/>
Creación de la base de datos asistencias_db<br/>
use asistencias_db<br/>
<img width="1919" height="1004" alt="image" src="https://github.com/user-attachments/assets/7672b286-2b7d-4043-8dd3-167fdfb8e0c2" />
<br/>
Resultados: La base de datos asistencias_db queda seleccionada para almacenar las colecciones del sistema de asistencia.<br/>
<br/>
Consulta 2<br/>
Creación de las colecciones (estudiantes, cursos y asistencias)<br/>
db.createCollection("estudiantes")<br/>
db.createCollection("cursos")<br/>
db.createCollection("asistencias")<br/>
Resultados: Se crean las tres colecciones principales que estructuran el sistema: estudiantes, cursos y asistencias.<br/>
<br/>
Consulta 3<br/>
Inserción de un documento en la colección estudiantes<br/>
db.estudiantes.insertOne({
  codigo: "EST1001",
  nombre: "María González",
  programa: "Ingeniería de Sistemas"
})<br/>
<img width="1913" height="1004" alt="image" src="https://github.com/user-attachments/assets/8b498464-c427-41fc-995a-a94a067eb18e" />
<br/>
Resultados: Se registra un estudiante con su código institucional, nombre y programa académico.<br/>
<br/>
1.2 Consultas básicas <br/>
<br/>
Consulta 4<br/>
Inserción (Agregar un nuevo curso)<br/>
db.cursos.insertOne({
  codigo: "CURS-200",
  nombre: "Bases de Datos I",
  docente: "Carlos Ruiz"
})<br/>
<img width="1909" height="1003" alt="image" src="https://github.com/user-attachments/assets/f6a54652-550e-4be6-8781-bf2975142514" />
<br/>
Resultados: Se añade un curso nuevo que podrá asociarse posteriormente a registros de asistencia.<br/>
<br/>
Consulta 5<br/>
Actualización (Modificar el nombre de un estudiante)<br/>
db.estudiantes.updateOne(
  { codigo: "EST1001" },
  { $set: { nombre: "María Alejandra González" } }
)<br/>
<img width="1910" height="1004" alt="image" src="https://github.com/user-attachments/assets/bc41cd07-2ebd-43ce-8f9b-69d991b3be98" />
<br/>
Resultados: El nombre del estudiante se actualiza correctamente en la base de datos.
<br/>
<br/>
Consulta 6<br/>
Eliminación (Eliminar un curso por código)<br/>
db.cursos.deleteOne({ codigo: "CURS-200" })<br/>
<img width="1913" height="1002" alt="image" src="https://github.com/user-attachments/assets/ee62be4c-0e60-4de6-a6d8-088d443ccb99" />
<br/>
Resultados: El curso con dicho código es eliminado del sistema de manera definitiva.<br/>
<br/>
Consulta 7<br/>
Selección (Consultar todos los estudiantes del programa Ingeniería de Sistemas)<br/>
db.estudiantes.find({ programa: "Ingeniería de Sistemas" })<br/>
<img width="1918" height="1010" alt="image" src="https://github.com/user-attachments/assets/8c118dbf-2e62-4850-8322-c9c3e9cabed7" />
<br/>
Resultados: Se muestran únicamente los estudiantes inscritos en el programa solicitado.<br/>
1.3 Consultas con filtros y operadores<br/>
<br/>
Consulta 8<br/>
Buscar asistencias marcadas como “Ausente”<br/>
db.asistencias.find({ estado: "Ausente" })<br/>
<img width="959" height="500" alt="image" src="https://github.com/user-attachments/assets/64016dbc-8e4b-4902-bc77-65733fb22605" />
<br/>
Resultados: Se listan todos los registros donde el estudiante no asistió a clase.<br/>
<br/>
Consulta 9<br/>
Buscar asistencias posteriores a una fecha específica<br/>
db.asistencias.find({
  fecha: { $gt: ISODate("2025-03-01") }
})<br/>
<img width="953" height="503" alt="image" src="https://github.com/user-attachments/assets/4a4aea35-2e5b-406f-b2c7-aa843d7d92bf" />
<br/>
Resultados: Devuelve todas las asistencias registradas después de la fecha indicada.
<br/>
<br/>
Consulta 10<br/>
Buscar asistencias con observaciones registradas<br/>
db.asistencias.find({
  observacion: { $exists: true, $ne: "" }
})<br/>
<img width="955" height="505" alt="image" src="https://github.com/user-attachments/assets/6a86b431-8ff6-416b-afbb-83c91c9e7f9e" />
<br/>
Resultados: Muestra los registros que incluyen una observación adicional.<br/>
<br/>
Consulta 11<br/>
Filtrar asistencias por estado utilizando operadores OR<br/>
db.asistencias.find({
  $or: [
    { estado: "Tarde" },
    { estado: "Ausente" }
  ]
})<br/>
<img width="956" height="502" alt="image" src="https://github.com/user-attachments/assets/a5cdd865-3c5e-4c22-a720-ac1a56a99c39" />
<br/>
Resultados: Retorna las asistencias en las que el estudiante llegó tarde o estuvo ausente.<br/>
<br/>
1.4 Consultas de agregación para calcular estadísticas <br/>
<br/>
Consulta 12<br/>
Contar asistencias por estado<br/>
db.asistencias.aggregate([
  { $group: { _id: "$estado", total: { $sum: 1 } } },
  { $sort: { total: -1 } }
])<br/>
<img width="959" height="502" alt="image" src="https://github.com/user-attachments/assets/20765947-22a4-431e-96c3-c45c74787ac7" />
<br/>
Resultado: Se obtiene cuántas asistencias hay de cada tipo (Presente, Ausente, Tarde).<br/>
<br/>
Consulta 13<br/>
Calcular el número de asistencias registradas por estudiante<br/>
db.asistencias.aggregate([
  { $group: { _id: "$estudiante_id", total_asistencias: { $sum: 1 } } }
])<br/>
<img width="952" height="503" alt="image" src="https://github.com/user-attachments/assets/25a93cb2-e9b9-4cb3-95ae-cdafce656fac" />
<br/>
Resultado: La salida muestra cuántos registros tiene cada estudiante en la colección asistencias.<br/>
<br/>
<br/>
Consulta 14<br/>
Contar el total de estudiantes registrados<br/>
db.estudiantes.aggregate([
  { $count: "total_estudiantes" }
])<br/>
<img width="955" height="503" alt="image" src="https://github.com/user-attachments/assets/aa9d173f-5110-4806-9453-343cd2702543" />
<br/>
Resultado: Devuelve la cantidad total de estudiantes registrados en el sistema.<br/>
<br/>
Consulta 15<br/>
Calcular porcentaje de asistencias presentes<br/>
db.asistencias.aggregate([
  { $match: { estado: "Presente" } },
  { $group: { _id: null, presentes: { $sum: 1 } } }
])<br/>
<img width="959" height="503" alt="image" src="https://github.com/user-attachments/assets/31e8fc84-7208-4f9d-b8ca-eb296bd00f61" />
<br/>
Resultado: Muestra cuántas asistencias han sido marcadas como "Presente", útil para cálculos de desempeño.<br/>
<br/>
<br/>
<br/>
<br/>
<div style="text-align: center;"><b>2025</b><br/></div>
