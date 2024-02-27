import javax.persistence.*;

@Entity
@Table(name = "employees")
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;

    @Column(name = "salary")
    private double salary;

    // Constructors, getters, and setters
}

public class Main {

    public static void main(String[] args) {
        EntityManagerFactory entityManagerFactory = Persistence.createEntityManagerFactory("EmployeePU");
        EntityManager entityManager = entityManagerFactory.createEntityManager();

        EntityTransaction transaction = entityManager.getTransaction();
        transaction.begin();

        // Create a new employee
        Employee employee = new Employee();
        employee.setName("John Doe");
        employee.setSalary(50000.0);

        // Persist the employee object
        entityManager.persist(employee);

        transaction.commit();

        // Retrieve the employee object by ID
        Employee retrievedEmployee = entityManager.find(Employee.class, employee.getId());
        System.out.println("Retrieved Employee: " + retrievedEmployee.getName() + ", Salary: " + retrievedEmployee.getSalary());

        entityManager.close();
        entityManagerFactory.close();
    }
}
