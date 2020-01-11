#Se pueden usar alias para hacer varias consultas a la vez y leerlo facilmente
Aliases:
```graphql
{
	AllCourses: getCourses{
    _id
    title
  }
  Course1: getCourse(id: "5e164c3842c66cc9b2afd1af"){
    _id
    title
    description
  }
  Course2: getCourse(id: "5e164c3842c66cc9b2afd1b0"){
    title
    description
    topic
  }
}
```
#Fragment sirve para agrupar campos para reutilizarlos en otras queries
Fragments:
```graphql
{
	AllCourses: getCourses{
    _id
    title
  }
  Course1: getCourse(id: "5e164c3842c66cc9b2afd1af"){
    ...CourseFields
    teacher
  }
  Course2: getCourse(id: "5e164c3842c66cc9b2afd1b0"){
    ...CourseFields
    topic
  }
}

fragment CourseFields on Course{
  _id
  title
  description
  people{
    _id
    name
  }
}
```
#Las variables permiten extraer complejidad y datos de un mutation
Variables
```graphql
mutation CreateNewCourse($createInput: CourseInput!){
  createCourse(input: $createInput){
    _id
    title
  }
}

#query variables
{
  "createInput": {
    "title": "Mi Titulo 6",
    "teacher": "Profesor 6",
    "description": "Curso de ejemplo 6",
    "topic": "programacion",
    "level": "principiante"
  }
}
```

#Enum sirve para definir un tipo de dato con valores fijos
Enum en schema.graphql
```graphql
"Valida los tipos de nivel"
enum Level{
  principiante
  intermedio
  avanzado
}
type Course {
  _id: ID!
  title: String!
  teacher: String
  description: String!
  topic: String
  people: [Student]
  level: Level
}
input CourseInput {
  title: String!
  teacher: String
  description: String!
  topic: String 
  level: Level
}
```

#Directivas permite agregar condicionales para mostrar info o no
```graphql
query getPeopleData($monitor: Boolean!, $avatar: Boolean!){
	getPeople{
    _id
    name
  	... on Monitor @include(if: $monitor){
      phone
    }
    ... on Student @include(if: $avatar){
      avatar
      email
    }
  }
}

//Query variables
{
  "monitor": true,
  "avatar": true
}
```