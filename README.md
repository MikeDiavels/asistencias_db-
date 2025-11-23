<b>Sistema de registro de asistencia estudiantil</b><br/>
Este caso de uso se centra en la creación de un sistema para gestionar la asistencia de estudiantes en una institución educativa. El sistema debe permitir registrar la presencia, ausencia o tardanza de cada estudiante en distintos cursos y fechas. MongoDB es adecuado porque permite almacenar registros con diferentes cantidades de asistencias por estudiante, añadir observaciones opcionales, y manejar información variable sin requerir la rigidez de una base de datos relacional. El objetivo es facilitar consultas como asistencia por curso, porcentajes de asistencia, historial por estudiante y reportes para seguimiento académico.

<b>Diseño de la base de datos</b><br/>
La base de datos asistencias_db se divide en tres colecciones: estudiantes, cursos y asistencias. Los registros de asistencia se relacionan con estudiantes y cursos mediante identificadores, permitiendo almacenar fechas, estados y observaciones. El modelo documental facilita manejar múltiples asistencias por estudiante sin una estructura rígida.
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
