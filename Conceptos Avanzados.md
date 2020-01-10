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

