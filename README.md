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

<b>Consultas basicas</b><br/>
<br/>Creacion y uso de la base de datos<br/>
use asistencias_db<br/>

// Colección: estudiantes (30 documentos)<br/>
db.estudiantes.insertMany([

  { _id: ObjectId("651a12345678901234567891"), codigo: "20230001", nombre: "Ana María García López", programa: "Ingeniería de Sistemas" },
  { _id: ObjectId("651a12345678901234567892"), codigo: "20230002", nombre: "Carlos Andrés Rodríguez", programa: "Ingeniería de Sistemas" },
  { _id: ObjectId("651a12345678901234567893"), codigo: "20230003", nombre: "María Fernanda Pérez", programa: "Ingeniería de Sistemas" },
  { _id: ObjectId("651a12345678901234567894"), codigo: "20230004", nombre: "Javier Antonio Mendoza", programa: "Ingeniería Civil" },
  { _id: ObjectId("651a12345678901234567895"), codigo: "20230005", nombre: "Laura Patricia Silva", programa: "Ingeniería Civil" },
  { _id: ObjectId("651a12345678901234567896"), codigo: "20230006", nombre: "Diego Alejandro Torres", programa: "Administración" },
  { _id: ObjectId("651a12345678901234567897"), codigo: "20230007", nombre: "Sofia Camila Rojas", programa: "Administración" },
  { _id: ObjectId("651a12345678901234567898"), codigo: "20230008", nombre: "Miguel Ángel Castro", programa: "Medicina" },
  { _id: ObjectId("651a12345678901234567899"), codigo: "20230009", nombre: "Valentina Ruiz Díaz", programa: "Medicina" },
  { _id: ObjectId("651a1234567890123456789a"), codigo: "20230010", nombre: "Andrés Felipe Vargas", programa: "Derecho" },
  { _id: ObjectId("651a1234567890123456789b"), codigo: "20230011", nombre: "Carolina Herrera", programa: "Derecho" },
  { _id: ObjectId("651a1234567890123456789c"), codigo: "20230012", nombre: "Ricardo José Morales", programa: "Psicología" },
  { _id: ObjectId("651a1234567890123456789d"), codigo: "20230013", nombre: "Daniela Alejandra Ortiz", programa: "Psicología" },
  { _id: ObjectId("651a1234567890123456789e"), codigo: "20230014", nombre: "Juan Pablo Ramírez", programa: "Ingeniería Industrial" },
  { _id: ObjectId("651a1234567890123456789f"), codigo: "20230015", nombre: "Paola Andrea Núñez", programa: "Ingeniería Industrial" },
  { _id: ObjectId("651a123456789012345678a0"), codigo: "20230016", nombre: "Luis Fernando Gómez", programa: "Contaduría" },
  { _id: ObjectId("651a123456789012345678a1"), codigo: "20230017", nombre: "Isabella Martínez", programa: "Contaduría" },
  { _id: ObjectId("651a123456789012345678a2"), codigo: "20230018", nombre: "Sebastián Jiménez", programa: "Arquitectura" },
  { _id: ObjectId("651a123456789012345678a3"), codigo: "20230019", nombre: "Camila Andrea Paredes", programa: "Arquitectura" },
  { _id: ObjectId("651a123456789012345678a4"), codigo: "20230020", nombre: "Óscar David León", programa: "Biología" },
  { _id: ObjectId("651a123456789012345678a5"), codigo: "20230021", nombre: "Natalia Sánchez", programa: "Biología" },
  { _id: ObjectId("651a123456789012345678a6"), codigo: "20230022", nombre: "Héctor Manuel Ríos", programa: "Matemáticas" },
  { _id: ObjectId("651a123456789012345678a7"), codigo: "20230023", nombre: "Gabriela Montes", programa: "Matemáticas" },
  { _id: ObjectId("651a123456789012345678a8"), codigo: "20230024", nombre: "Fernando José Peña", programa: "Física" },
  { _id: ObjectId("651a123456789012345678a9"), codigo: "20230025", nombre: "Adriana Lucía Mora", programa: "Física" },
  { _id: ObjectId("651a123456789012345678aa"), codigo: "20230026", nombre: "Roberto Carlos Duarte", programa: "Química" },
  { _id: ObjectId("651a123456789012345678ab"), codigo: "20230027", nombre: "Mónica Patricia Reyes", programa: "Química" },
  { _id: ObjectId("651a123456789012345678ac"), codigo: "20230028", nombre: "Esteban Augusto Linares", programa: "Economía" },
  { _id: ObjectId("651a123456789012345678ad"), codigo: "20230029", nombre: "Verónica Isabel Cordero", programa: "Economía" },
  { _id: ObjectId("651a123456789012345678ae"), codigo: "20230030", nombre: "Raúl Eduardo Pacheco", programa: "Ingeniería Electrónica" }
])
<br/>
// Colección: cursos (15 documentos)<br/>
db.cursos.insertMany([

  { _id: ObjectId("651b12345678901234567891"), codigo: "MAT101", nombre: "Cálculo I", docente: "Dr. Roberto Álvarez" },
  { _id: ObjectId("651b12345678901234567892"), codigo: "MAT102", nombre: "Cálculo II", docente: "Dra. Carmen Sarmiento" },
  { _id: ObjectId("651b12345678901234567893"), codigo: "FIS101", nombre: "Física General", docente: "Dr. Luis Méndez" },
  { _id: ObjectId("651b12345678901234567894"), codigo: "FIS102", nombre: "Física Avanzada", docente: "Dra. Patricia Rojas" },
  { _id: ObjectId("651b12345678901234567895"), codigo: "QUI101", nombre: "Química General", docente: "Dr. Jorge Silva" },
  { _id: ObjectId("651b12345678901234567896"), codigo: "ING101", nombre: "Inglés I", docente: "Prof. Laura Thompson" },
  { _id: ObjectId("651b12345678901234567897"), codigo: "ING102", nombre: "Inglés II", docente: "Prof. Michael Brown" },
  { _id: ObjectId("651b12345678901234567898"), codigo: "PRO101", nombre: "Programación I", docente: "Ing. Carlos Fuentes" },
  { _id: ObjectId("651b12345678901234567899"), codigo: "PRO102", nombre: "Programación II", docente: "Ing. Ana Martínez" },
  { _id: ObjectId("651b1234567890123456789a"), codigo: "BDD101", nombre: "Bases de Datos", docente: "Mg. Ricardo Ortega" },
  { _id: ObjectId("651b1234567890123456789b"), codigo: "RED101", nombre: "Redes de Computadores", docente: "Dr. Fernando Castro" },
  { _id: ObjectId("651b1234567890123456789c"), codigo: "ETI101", nombre: "Ética Profesional", docente: "Dra. Marta Villanueva" },
  { _id: ObjectId("651b1234567890123456789d"), codigo: "ADM101", nombre: "Administración", docente: "Mg. Pedro Navarro" },
  { _id: ObjectId("651b1234567890123456789e"), codigo: "ECO101", nombre: "Economía", docente: "Dr. Sergio Ramírez" },
  { _id: ObjectId("651b1234567890123456789f"), codigo: "DER101", nombre: "Derecho Constitucional", docente: "Dra. Isabel Mendoza" }
])<br/>

// Colección: asistencias (60 documentos - 2 asistencias por estudiante en diferentes cursos)<br/>
db.asistencias.insertMany([
  // Asistencias para la primera semana de marzo
  { _id: ObjectId("651c12345678901234567891"), estudiante_id: ObjectId("651a12345678901234567891"), curso_id: ObjectId("651b12345678901234567891"), fecha: ISODate("2024-03-01"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c12345678901234567892"), estudiante_id: ObjectId("651a12345678901234567891"), curso_id: ObjectId("651b12345678901234567898"), fecha: ISODate("2024-03-02"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c12345678901234567893"), estudiante_id: ObjectId("651a12345678901234567892"), curso_id: ObjectId("651b12345678901234567891"), fecha: ISODate("2024-03-01"), estado: "Tarde", observacion: "Llegó 15 minutos tarde" },
  { _id: ObjectId("651c12345678901234567894"), estudiante_id: ObjectId("651a12345678901234567892"), curso_id: ObjectId("651b12345678901234567899"), fecha: ISODate("2024-03-03"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c12345678901234567895"), estudiante_id: ObjectId("651a12345678901234567893"), curso_id: ObjectId("651b12345678901234567892"), fecha: ISODate("2024-03-01"), estado: "Ausente", observacion: "Justificado - Enfermedad" },
  { _id: ObjectId("651c12345678901234567896"), estudiante_id: ObjectId("651a12345678901234567893"), curso_id: ObjectId("651b1234567890123456789a"), fecha: ISODate("2024-03-04"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c12345678901234567897"), estudiante_id: ObjectId("651a12345678901234567894"), curso_id: ObjectId("651b12345678901234567893"), fecha: ISODate("2024-03-02"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c12345678901234567898"), estudiante_id: ObjectId("651a12345678901234567894"), curso_id: ObjectId("651b1234567890123456789b"), fecha: ISODate("2024-03-05"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c12345678901234567899"), estudiante_id: ObjectId("651a12345678901234567895"), curso_id: ObjectId("651b12345678901234567894"), fecha: ISODate("2024-03-03"), estado: "Tarde", observacion: "Problemas de transporte" },
  { _id: ObjectId("651c1234567890123456789a"), estudiante_id: ObjectId("651a12345678901234567895"), curso_id: ObjectId("651b1234567890123456789c"), fecha: ISODate("2024-03-06"), estado: "Presente", observacion: "" },<br/>
  
  // Continuación con más estudiantes...<br/>
  { _id: ObjectId("651c1234567890123456789b"), estudiante_id: ObjectId("651a12345678901234567896"), curso_id: ObjectId("651b12345678901234567895"), fecha: ISODate("2024-03-04"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c1234567890123456789c"), estudiante_id: ObjectId("651a12345678901234567896"), curso_id: ObjectId("651b1234567890123456789d"), fecha: ISODate("2024-03-07"), estado: "Ausente", observacion: "" },
  { _id: ObjectId("651c1234567890123456789d"), estudiante_id: ObjectId("651a12345678901234567897"), curso_id: ObjectId("651b12345678901234567896"), fecha: ISODate("2024-03-05"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c1234567890123456789e"), estudiante_id: ObjectId("651a12345678901234567897"), curso_id: ObjectId("651b1234567890123456789e"), fecha: ISODate("2024-03-08"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c1234567890123456789f"), estudiante_id: ObjectId("651a12345678901234567898"), curso_id: ObjectId("651b12345678901234567897"), fecha: ISODate("2024-03-06"), estado: "Tarde", observacion: "Llegó 10 minutos tarde" },
  { _id: ObjectId("651c123456789012345678a0"), estudiante_id: ObjectId("651a12345678901234567898"), curso_id: ObjectId("651b1234567890123456789f"), fecha: ISODate("2024-03-09"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678a1"), estudiante_id: ObjectId("651a12345678901234567899"), curso_id: ObjectId("651b12345678901234567898"), fecha: ISODate("2024-03-07"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678a2"), estudiante_id: ObjectId("651a12345678901234567899"), curso_id: ObjectId("651b12345678901234567891"), fecha: ISODate("2024-03-10"), estado: "Ausente", observacion: "Sin justificación" },
  { _id: ObjectId("651c123456789012345678a3"), estudiante_id: ObjectId("651a1234567890123456789a"), curso_id: ObjectId("651b12345678901234567899"), fecha: ISODate("2024-03-08"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678a4"), estudiante_id: ObjectId("651a1234567890123456789a"), curso_id: ObjectId("651b12345678901234567892"), fecha: ISODate("2024-03-11"), estado: "Presente", observacion: "" },
  <br/>
  // Segunda semana de marzo<br/>
  { _id: ObjectId("651c123456789012345678a5"), estudiante_id: ObjectId("651a12345678901234567891"), curso_id: ObjectId("651b12345678901234567893"), fecha: ISODate("2024-03-15"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678a6"), estudiante_id: ObjectId("651a12345678901234567892"), curso_id: ObjectId("651b12345678901234567894"), fecha: ISODate("2024-03-16"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678a7"), estudiante_id: ObjectId("651a12345678901234567893"), curso_id: ObjectId("651b12345678901234567895"), fecha: ISODate("2024-03-15"), estado: "Tarde", observacion: "Llegó 5 minutos tarde" },
  { _id: ObjectId("651c123456789012345678a8"), estudiante_id: ObjectId("651a12345678901234567894"), curso_id: ObjectId("651b12345678901234567896"), fecha: ISODate("2024-03-17"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678a9"), estudiante_id: ObjectId("651a12345678901234567895"), curso_id: ObjectId("651b12345678901234567897"), fecha: ISODate("2024-03-16"), estado: "Ausente", observacion: "Justificado - Médico" },
  { _id: ObjectId("651c123456789012345678aa"), estudiante_id: ObjectId("651a12345678901234567896"), curso_id: ObjectId("651b12345678901234567898"), fecha: ISODate("2024-03-18"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678ab"), estudiante_id: ObjectId("651a12345678901234567897"), curso_id: ObjectId("651b12345678901234567899"), fecha: ISODate("2024-03-17"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678ac"), estudiante_id: ObjectId("651a12345678901234567898"), curso_id: ObjectId("651b1234567890123456789a"), fecha: ISODate("2024-03-19"), estado: "Tarde", observacion: "Tráfico pesado" },
  { _id: ObjectId("651c123456789012345678ad"), estudiante_id: ObjectId("651a12345678901234567899"), curso_id: ObjectId("651b1234567890123456789b"), fecha: ISODate("2024-03-18"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678ae"), estudiante_id: ObjectId("651a1234567890123456789a"), curso_id: ObjectId("651b1234567890123456789c"), fecha: ISODate("2024-03-20"), estado: "Presente", observacion: "" },
  <br/>
  // Continuar con más asistencias para completar 60...<br/>
  { _id: ObjectId("651c123456789012345678af"), estudiante_id: ObjectId("651a1234567890123456789b"), curso_id: ObjectId("651b1234567890123456789d"), fecha: ISODate("2024-03-15"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678b0"), estudiante_id: ObjectId("651a1234567890123456789b"), curso_id: ObjectId("651b1234567890123456789e"), fecha: ISODate("2024-03-21"), estado: "Ausente", observacion: "" },
  { _id: ObjectId("651c123456789012345678b1"), estudiante_id: ObjectId("651a1234567890123456789c"), curso_id: ObjectId("651b1234567890123456789f"), fecha: ISODate("2024-03-16"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678b2"), estudiante_id: ObjectId("651a1234567890123456789c"), curso_id: ObjectId("651b12345678901234567891"), fecha: ISODate("2024-03-22"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678b3"), estudiante_id: ObjectId("651a1234567890123456789d"), curso_id: ObjectId("651b12345678901234567892"), fecha: ISODate("2024-03-17"), estado: "Tarde", observacion: "Problemas familiares" },
  { _id: ObjectId("651c123456789012345678b4"), estudiante_id: ObjectId("651a1234567890123456789d"), curso_id: ObjectId("651b12345678901234567893"), fecha: ISODate("2024-03-23"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678b5"), estudiante_id: ObjectId("651a1234567890123456789e"), curso_id: ObjectId("651b12345678901234567894"), fecha: ISODate("2024-03-18"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678b6"), estudiante_id: ObjectId("651a1234567890123456789e"), curso_id: ObjectId("651b12345678901234567895"), fecha: ISODate("2024-03-24"), estado: "Ausente", observacion: "Viaje familiar" },
  { _id: ObjectId("651c123456789012345678b7"), estudiante_id: ObjectId("651a1234567890123456789f"), curso_id: ObjectId("651b12345678901234567896"), fecha: ISODate("2024-03-19"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678b8"), estudiante_id: ObjectId("651a1234567890123456789f"), curso_id: ObjectId("651b12345678901234567897"), fecha: ISODate("2024-03-25"), estado: "Presente", observacion: "" },
  <br/>
  // Últimas asistencias...<br/>
  { _id: ObjectId("651c123456789012345678b9"), estudiante_id: ObjectId("651a123456789012345678a0"), curso_id: ObjectId("651b12345678901234567898"), fecha: ISODate("2024-03-20"), estado: "Tarde", observacion: "Despertador no sonó" },
  { _id: ObjectId("651c123456789012345678ba"), estudiante_id: ObjectId("651a123456789012345678a0"), curso_id: ObjectId("651b12345678901234567899"), fecha: ISODate("2024-03-26"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678bb"), estudiante_id: ObjectId("651a123456789012345678a1"), curso_id: ObjectId("651b1234567890123456789a"), fecha: ISODate("2024-03-21"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678bc"), estudiante_id: ObjectId("651a123456789012345678a1"), curso_id: ObjectId("651b1234567890123456789b"), fecha: ISODate("2024-03-27"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678bd"), estudiante_id: ObjectId("651a123456789012345678a2"), curso_id: ObjectId("651b1234567890123456789c"), fecha: ISODate("2024-03-22"), estado: "Ausente", observacion: "Sin comunicación" },
  { _id: ObjectId("651c123456789012345678be"), estudiante_id: ObjectId("651a123456789012345678a2"), curso_id: ObjectId("651b1234567890123456789d"), fecha: ISODate("2024-03-28"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678bf"), estudiante_id: ObjectId("651a123456789012345678a3"), curso_id: ObjectId("651b1234567890123456789e"), fecha: ISODate("2024-03-23"), estado: "Presente", observacion: "" },
  { _id: ObjectId("651c123456789012345678c0"), estudiante_id: ObjectId("651a123456789012345678a3"), curso_id: ObjectId("651b1234567890123456789f"), fecha: ISODate("2024-03-29"), estado: "Tarde", observacion: "Llegó 8 minutos tarde" }
])
<br/>
<br/>
<br/>
// Verificar conteos<br/>
print("Total estudiantes: " + db.estudiantes.countDocuments())<br/>
print("Total cursos: " + db.cursos.countDocuments())<br/>
print("Total asistencias: " + db.asistencias.countDocuments())<br/>

<br/>
<br/>
<br/>
Consultas con filtros y operadores.
<br/>
Consulta 1: Lista estudiantes complicados.
<br/>
db.asistencias.aggregate([

  {
    $match: { estado: "Ausente" }
  },
  {
    $group: {
      _id: "$estudiante_id",
      totalAusencias: { $sum: 1 }
    }
  },
  {
    $match: { totalAusencias: { $gt: 2 } }
  },
  {
    $lookup: {
      from: "estudiantes",
      localField: "_id",
      foreignField: "_id",
      as: "estudiante"
    }
  },
  {
    $unwind: "$estudiante"
  },
  {
    $project: {
      "nombre": "$estudiante.nombre",
      "codigo": "$estudiante.codigo", 
      "programa": "$estudiante.programa",
      "total_ausencias": "$totalAusencias"
    }
  }
])

<br/>
<br/>
<br/>
Consulta 2: Ranking de cursos por asistencia
<br/>
db.asistencias.aggregate([
  {
    $group: {
      _id: "$curso_id",
      total: { $sum: 1 },
      presentes: { $sum: { $cond: [{ $eq: ["$estado", "Presente"] }, 1, 0] } },
      tardes: { $sum: { $cond: [{ $eq: ["$estado", "Tarde"] }, 1, 0] } },
      ausentes: { $sum: { $cond: [{ $eq: ["$estado", "Ausente"] }, 1, 0] } }
    }
  },
  {
    $lookup: {
      from: "cursos",
      localField: "_id",
      foreignField: "_id",
      as: "curso"
    }
  },
  {
    $unwind: "$curso"
  },
  {
    $project: {
      "curso": "$curso.nombre",
      "docente": "$curso.docente",
      "total_registros": "$total",
      "presentes": "$presentes",
      "tardes": "$tardes", 
      "ausentes": "$ausentes",
      "porcentaje_asistencia": {
        $round: [
          {
            $multiply: [
              {
                $divide: [
                  { $add: ["$presentes", "$tardes"] },
                  "$total"
                ]
              },
              100
            ]
          },
          2
        ]
      }
    }
  },
  {
    $sort: { porcentaje_asistencia: -1 }
  }
])
<br/>
<br/>
<br/>

Consulta 3: Incidencias específicas con justificación
<br/>
db.asistencias.find({
  $and: [
    { 
      fecha: { 
        $gte: ISODate("2024-03-15"), 
        $lte: ISODate("2024-03-21") 
      } 
    },
    { 
      estado: { $in: ["Tarde", "Ausente"] } 
    },
    { 
      observacion: { $ne: "" } 
    }
  ]
})
<br/>
<br/>
<br/>
Consulta 4: Comparativa entre programas académicos
<br/>
db.estudiantes.aggregate([
  {
    $lookup: {
      from: "asistencias",
      localField: "_id",
      foreignField: "estudiante_id",
      as: "asistencias"
    }
  },
  {
    $unwind: "$asistencias"
  },
  {
    $group: {
      _id: "$programa",
      total_estudiantes: { $addToSet: "$_id" },
      total_registros: { $sum: 1 },
      presentes: { $sum: { $cond: [{ $eq: ["$asistencias.estado", "Presente"] }, 1, 0] } },
      tardes: { $sum: { $cond: [{ $eq: ["$asistencias.estado", "Tarde"] }, 1, 0] } }
    }
  },
  {
    $project: {
      "programa": "$_id",
      "total_estudiantes": { $size: "$total_estudiantes" },
      "total_registros": "$total_registros",
      "porcentaje_asistencia": {
        $round: [
          {
            $multiply: [
              {
                $divide: [
                  { $add: ["$presentes", "$tardes"] },
                  "$total_registros"
                ]
              },
              100
            ]
          },
          2
        ]
      }
    }
  },
  {
    $sort: { porcentaje_asistencia: -1 }
  }
])

<br/>
<br/>
<br/>

Consultas de agregación para calcular estadísticas <br/>
Consulta 1: Evolución mensual de asistencia<br/>

db.asistencias.aggregate([
  {
    $addFields: {
      mes: { $month: "$fecha" },
      año: { $year: "$fecha" }
    }
  },
  {
    $group: {
      _id: { mes: "$mes", año: "$año" },
      total_registros: { $sum: 1 },
      total_presentes: { $sum: { $cond: [{ $eq: ["$estado", "Presente"] }, 1, 0] } },
      total_tardes: { $sum: { $cond: [{ $eq: ["$estado", "Tarde"] }, 1, 0] } },
      total_ausentes: { $sum: { $cond: [{ $eq: ["$estado", "Ausente"] }, 1, 0] } },
      estudiantes_unicos: { $addToSet: "$estudiante_id" }
    }
  },
  {
    $project: {
      _id: 0,
      periodo: { $concat: [{ $toString: "$_id.mes" }, "-", { $toString: "$_id.año" }] },
      total_registros: 1,
      total_presentes: 1,
      total_tardes: 1,
      total_ausentes: 1,
      total_estudiantes: { $size: "$estudiantes_unicos" },
      porcentaje_asistencia: {
        $round: [
          {
            $multiply: [
              {
                $divide: [
                  { $add: ["$total_presentes", { $multiply: ["$total_tardes", 0.8] }] },
                  "$total_registros"
                ]
              },
              100
            ]
          },
          2
        ]
      },
      promedio_asistencias_por_estudiante: {
        $round: [
          { $divide: ["$total_registros", { $size: "$estudiantes_unicos" }] },
          2
        ]
      }
    }
  },
  {
    $sort: { periodo: 1 }
  }
])
<br/>
<br/>
<br/>
Consulta 2: Ranking de estudiantes (mejores y peores)
<br/>
db.asistencias.aggregate([
  {
    $group: {
      _id: "$estudiante_id",
      total_asistencias: { $sum: 1 },
      presentes: { $sum: { $cond: [{ $eq: ["$estado", "Presente"] }, 1, 0] } },
      tardes: { $sum: { $cond: [{ $eq: ["$estado", "Tarde"] }, 1, 0] } },
      ausentes: { $sum: { $cond: [{ $eq: ["$estado", "Ausente"] }, 1, 0] } }
    }
  },
  {
    $match: {
      total_asistencias: { $gte: 5 }
    }
  },
  {
    $addFields: {
      porcentaje_asistencia: {
        $round: [
          {
            $multiply: [
              {
                $divide: [
                  { $add: ["$presentes", { $multiply: ["$tardes", 0.8] }] },
                  "$total_asistencias"
                ]
              },
              100
            ]
          },
          2
        ]
      }
    }
  },
  {
    $lookup: {
      from: "estudiantes",
      localField: "_id",
      foreignField: "_id",
      as: "estudiante_info"
    }
  },
  {
    $unwind: "$estudiante_info"
  },
  {
    $facet: {
      "mejor_asistencia": [
      { $sort: { porcentaje_asistencia: -1 } },
        { $limit: 5 },
        {
          $project: {
            _id: 0,
            estudiante: "$estudiante_info.nombre",
            codigo: "$estudiante_info.codigo",
            programa: "$estudiante_info.programa",
            total_asistencias: 1,
            presentes: 1,
            tardes: 1,
            ausentes: 1,
            porcentaje_asistencia: 1
          }
        }
      ],
      "peor_asistencia": [
        { $sort: { porcentaje_asistencia: 1 } },
        { $limit: 5 },
        {
          $project: {
            _id: 0,
            estudiante: "$estudiante_info.nombre",
            codigo: "$estudiante_info.codigo",
            programa: "$estudiante_info.programa",
            total_asistencias: 1,
            presentes: 1,
            tardes: 1,
            ausentes: 1,
            porcentaje_asistencia: 1
          }
        }
      ]
    }
  }
])
<br/>
<br/>
<br/>
Consulta 3: Comportamiento por días de la semana
<br/>
db.asistencias.aggregate([
  {
    $addFields: {
      dia_semana: { $dayOfWeek: "$fecha" },
      nombre_dia: {
        $switch: {
          branches: [
            { case: { $eq: [{ $dayOfWeek: "$fecha" }, 1] }, then: "Domingo" },
            { case: { $eq: [{ $dayOfWeek: "$fecha" }, 2] }, then: "Lunes" },
            { case: { $eq: [{ $dayOfWeek: "$fecha" }, 3] }, then: "Martes" },
            { case: { $eq: [{ $dayOfWeek: "$fecha" }, 4] }, then: "Miércoles" },
            { case: { $eq: [{ $dayOfWeek: "$fecha" }, 5] }, then: "Jueves" },
            { case: { $eq: [{ $dayOfWeek: "$fecha" }, 6] }, then: "Viernes" },
            { case: { $eq: [{ $dayOfWeek: "$fecha" }, 7] }, then: "Sábado" }
          ],
          default: "Desconocido"
        }
      }
    }
  },
  {
    $group: {
      _id: "$nombre_dia",
      dia_numero: { $first: "$dia_semana" },
      total_registros: { $sum: 1 },
      presentes: { $sum: { $cond: [{ $eq: ["$estado", "Presente"] }, 1, 0] } },
      tardes: { $sum: { $cond: [{ $eq: ["$estado", "Tarde"] }, 1, 0] } },
      ausentes: { $sum: { $cond: [{ $eq: ["$estado", "Ausente"] }, 1, 0] } },
      cursos_unicos: { $addToSet: "$curso_id" }
    }
  },
  {
    $project: {
      _id: 0,
      dia: "$_id",
      dia_numero: 1,
      total_registros: 1,
      total_cursos: { $size: "$cursos_unicos" },
      porcentaje_asistencia: {
        $round: [
          {
            $multiply: [
              {
                $divide: [
                  { $add: ["$presentes", { $multiply: ["$tardes", 0.8] }] },
                  "$total_registros"
                ]
              },
              100
            ]
          },
          2
        ]
      },
      indice_tardanzas: {
        $round: [
          {
            $multiply: [
              { $divide: ["$tardes", "$total_registros"] },
              100
            ]
          },
          2
        ]
      },
      indice_ausentismo: {
        $round: [
          {
            $multiply: [
              { $divide: ["$ausentes", "$total_registros"] },
              100
            ]
          },
          2
        ]
      }
    }
  },
  {
    $sort: { dia_numero: 1 }
  }
])
<br/>
<br/>
<br/>
Consulta 4: Comparativa entre programas con calificaciones, podemos ver el número del día, el día en letras, total registros, total cursos, porcentajes de asistencias, índice de tardanzas, índice de ausentismo.
<br/>
db.estudiantes.aggregate([
  {
    $lookup: {
      from: "asistencias",
      localField: "_id",
      foreignField: "estudiante_id",
      as: "asistencias"
    }
  },
  {
    $unwind: "$asistencias"
  },
  {
    $group: {
      _id: "$programa",
      total_estudiantes: { $addToSet: "$_id" },
      total_registros: { $sum: 1 },
      total_presentes: { $sum: { $cond: [{ $eq: ["$asistencias.estado", "Presente"] }, 1, 0] } },
      total_tardes: { $sum: { $cond: [{ $eq: ["$asistencias.estado", "Tarde"] }, 1, 0] } },
      total_ausentes: { $sum: { $cond: [{ $eq: ["$asistencias.estado", "Ausente"] }, 1, 0] } },
      cursos_unicos: { $addToSet: "$asistencias.curso_id" }
    }
  },
  {
    $project: {
      _id: 0,
      programa: "$_id",
      total_estudiantes: { $size: "$total_estudiantes" },
      total_registros: 1,
      total_cursos: { $size: "$cursos_unicos" },
      metricas: {
        porcentaje_asistencia: {
          $round: [
            {
              $multiply: [
                {
                  $divide: [
                    { $add: ["$total_presentes", { $multiply: ["$total_tardes", 0.8] }] },
                    "$total_registros"
                  ]
                },
                100
              ]
            },
            2
          ]
        },
        porcentaje_tardanzas: {
          $round: [
            { $multiply: [{ $divide: ["$total_tardes", "$total_registros"] }, 100] },
            2
          ]
        },
        porcentaje_ausentismo: {
          $round: [
            { $multiply: [{ $divide: ["$total_ausentes", "$total_registros"] }, 100] },
            2
          ]
        },
        promedio_asistencias_por_estudiante: {
          $round: [
            { $divide: ["$total_registros", { $size: "$total_estudiantes" }] },
            2
          ]
        }
      },
      ranking: {
        $switch: {
          branches: [
            {
              case: { $gte: [{ $multiply: [{ $divide: [{ $add: ["$total_presentes", { $multiply: ["$total_tardes", 0.8] }] }, "$total_registros"] }, 100] }, 90] },
              then: "Excelente"
            },
            {
              case: { $gte: [{ $multiply: [{ $divide: [{ $add: ["$total_presentes", { $multiply: ["$total_tardes", 0.8] }] }, "$total_registros"] }, 100] }, 80] },
              then: "Bueno"
            },
            {
              case: { $gte: [{ $multiply: [{ $divide: [{ $add: ["$total_presentes", { $multiply: ["$total_tardes", 0.8] }] }, "$total_registros"] }, 100] }, 70] },
              then: "Regular"
            },
            {
              case: { $gte: [{ $multiply: [{ $divide: [{ $add: ["$total_presentes", { $multiply: ["$total_tardes", 0.8] }] }, "$total_registros"] }, 100] }, 60] },
              then: "Deficiente"
            }
          ],
          default: "Crítico"
        }
      }
    }
  },
  {
    $sort: { "metricas.porcentaje_asistencia": -1 }
  }
])
<br/>


<b>2025</b>
