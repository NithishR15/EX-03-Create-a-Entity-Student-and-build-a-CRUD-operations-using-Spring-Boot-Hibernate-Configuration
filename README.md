# EXp_03_-Entity-Student-and-build-a-CRUD-operations-using-Spring-Boot-Hibernate-Configuration
## Reg no:212223040135

## AIM:
To develop a Spring Boot application that performs CRUD (Create, Read, Update, Delete) operations on a Student entity using Spring Data JPA (Hibernate).

## ALGORITHM:
Create Spring Boot Project

Add dependencies: Spring Web, Spring Data JPA, H2 Database or MySQL, Spring Boot DevTools

Configure application.properties

Define database connection

Enable Hibernate auto DDL

Create Student Entity Class

Annotate with @Entity

Define fields with @Id, @GeneratedValue, etc.

Create StudentRepository

Extend JpaRepository<Student, Long> for CRUD methods

Create StudentController

Handle HTTP methods:

POST /students → Add student

GET /students → Get all students

GET /students/{id} → Get student by ID

PUT /students/{id} → Update student

DELETE /students/{id} → Delete student

##PROGRAM CODE

### pom.xml
```
<dependencies>
    <!-- Spring Boot Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Spring Boot JPA -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <!-- H2 Database (In-memory) -->
    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```
 ### application.properties
```
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=update
spring.h2.console.enabled=true
```
### Student.java
```
package com.example.ex3.model;

import jakarta.persistence.*;

@Entity
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String department;
    private int age;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
### StudentRepository.java
```
package com.example.ex3.repository;

import com.example.ex3.model.Student;
import org.springframework.data.jpa.repository.JpaRepository;

public interface StudentRepository extends JpaRepository<Student, Long> {
}
```
### StudentController.java
```
package com.example.ex3.controller;

import com.example.ex3.model.Student;
import com.example.ex3.repository.StudentRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;
import java.util.Optional;

@RestController
@RequestMapping("/students")
public class StudentController {

    @Autowired
    private StudentRepository studentRepository;

    @PostMapping
    public Student addStudent(@RequestBody Student student) {
        return studentRepository.save(student);
    }

    @GetMapping
    public List<Student> getAllStudents() {
        return studentRepository.findAll();
    }

    @GetMapping("/{id}")
    public Optional<Student> getStudent(@PathVariable Long id) {
        return studentRepository.findById(id);
    }

    @PutMapping("/{id}")
    public Student updateStudent(
            @PathVariable Long id,
            @RequestBody Student studentDetails) {

        Student student =
                studentRepository.findById(id).orElseThrow();

        student.setName(studentDetails.getName());
        student.setAge(studentDetails.getAge());
        student.setDepartment(studentDetails.getDepartment());

        return studentRepository.save(student);
    }

    @DeleteMapping("/{id}")
    public String deleteStudent(@PathVariable Long id) {

        studentRepository.deleteById(id);

        return "Student with ID " + id +
                " deleted successfully!";
    }
}
```
### DemoApplication.java
```
package com.example.ex3;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Ex3Application {

	public static void main(String[] args) {
		SpringApplication.run(Ex3Application.class, args);
	}
}
```
## Output:

## Add student
<img width="1917" height="1021" alt="Screenshot 2026-09-07 194410" src="https://github.com/user-attachments/assets/69092728-05c9-4fcc-8ee6-185a1f99cd13" />



## Get all students
<img width="1917" height="1015" alt="Screenshot 2026-09-07 194512" src="https://github.com/user-attachments/assets/185103ee-6db4-4303-8a7c-fa10734bfb67" />



## Get student by ID
<img width="1917" height="1020" alt="Screenshot 2026-09-07 194717" src="https://github.com/user-attachments/assets/19d3b9f6-00fb-4fdb-b1d3-2b2baa4300db" />



## Update student
<img width="1917" height="1020" alt="Screenshot 2026-09-07 194757" src="https://github.com/user-attachments/assets/0aa4f5e3-5d14-4ecf-8a90-12c5580ca6fd" />


## Delete student
<img width="1917" height="1020" alt="Screenshot 2026-09-07 194757" src="https://github.com/user-attachments/assets/fe247d9f-d2ad-42b4-a224-33124c018881" />


## H2-Console:
<img width="1917" height="1020" alt="Screenshot 2026-09-07 195344" src="https://github.com/user-attachments/assets/c101eae2-cb28-42dd-800e-87d9ccab2145" />


## Result:

Thus the development of a Spring Boot application that performs CRUD operations is completed successfully.
