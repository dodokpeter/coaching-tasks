# coaching-tasks
My tasks for coaching

## Git

Prequisites:

- installed GitBash
- account on GitHub

Theory:

- what is repository, branch, tags
- succesfull branching model
  - https://nvie.com/posts/a-successful-git-branching-model
- Git tutorial
  - https://git-scm.com/book/cs/v2

Tasks:

1. Create own repository on github.com with README file

2. Check the ssh public key on github account

3. Clone the repository into the file system

   `git clone [url]`

   `gitk --all`

   NOTE: check git settings or run

   ```
   $ git config --global user.name "John Doe"
   $ git config --global user.email johndoe@example.com
   ```

4. Change the file Readme.md

5. Stash your changes

   `git stash`

   `git stash pop`

6. Commit your changes (local) with 

   `git gui`

7. Push your commits to the remote

   `git push origin master`

8. Change the repository of your colleague and push it 

9. Change your own repository and commit changes, then try to push it

10. Recovering from conflicts

    

## Spring Boot

**Prequisites:**

- Java JDK 8 installed
- Maven installed

**Basic Spring Application:**

1. Visit page https://start.spring.io/
2. Customize your application properties
3.  Input in box **Search for dependencies:**
   - Web
   - JPA
   - Actuator
   - H2
   - Rest Repositories
   - Lombok
4. Click on Generate Project
5. Extract zip into the git repository or folder
6. Commit your work

**Theory**

- Main Application class
- Annotations and Autoconfiguration
- Properties files versus .ymls
- *ApplicationTests class
- Inmemory DBS
- http://localhost:8080

**First access to the database:**

1. create packeges:

   -  model
   - repositories
   - services

2. in model Create class **Customer** with attributes **name, surname, age**

   - @Entitie

   - Lombok annotations

   - @Id

     ```
     @Id
     @GeneratedValue(strategy=GenerationType.AUTO)
     private Long id;
     ```

3. in repositories create **CustomerRepository** interface, which **extends JpaRepository**

   - look up methods

     ```
     List<Customer> findBySurname(String lastName);
     
     @Query("SELECT u FROM User u WHERE u.age < 30")
     List<Customer> findAllUnder30();
     ```

4. in services create **CustomerService** class with reference to the repository (Dependency injection)

```
  @Autowired
  private CustomerRepository customerRepository;

//  @Autowired
//  public CustomerService(CustomerRepository customerRepository) {
//    this.customerRepository = customerRepository;
//  }
  
  public Customer getCustomer(Long id){
    Customer one = customerRepository.getOne(id);
    //operations on it
    return one;
  }

  public List<Customer> getCustomer(String surname){
    List<Customer> bySurname = customerRepository.findBySurname(surname);
    if (bySurname.size()==0){
      throw new IllegalArgumentException("No Customer with such lastname")  
    }
    return bySurname;
  }
```

5. Lombok and spring Autowiring

   ```
   @AllArgsConstructor(onConstructor = @__(@Autowired))
   ```

6. Test in JUnit

**First REST full endpoint:**

1. Add new package controllers
2. Add new class CustomerAPI
3. Add endpoint for reaching all customers by surname
4. Add Swagger  http://localhost:8080/swagger-ui.html#/

**Additional tasks:**

1. Add error handler
2. Add Spring Data Rest
3. Settings: change a port of the server
4. Settings: LOG level