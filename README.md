# 23BCS10234-Vijay-Bhaskar

import java.util.*;
import java.util.stream.*;

class Employee {
    int id;
    String name;
    double salary;

    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public String toString() {
        return id + " - " + name + " - $" + salary;
    }
}

class Student {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    public String toString() {
        return name + " - Marks: " + marks;
    }
}

class Product {
    int id;
    String name;
    double price;

    Product(int id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    public String toString() {
        return id + " - " + name + " - $" + price;
    }
}

public class LambdaStreamDemo {
    public static void main(String[] args) {
        List<Employee> employees = Arrays.asList(
            new Employee(3, "Ravindra", 50000),
            new Employee(1, "Nikhil", 70000),
            new Employee(2, "Mukesh", 60000)
        );

        System.out.println("Employees sorted by Name:");
        employees.sort((e1, e2) -> e1.name.compareTo(e2.name));
        employees.forEach(System.out::println);

        System.out.println("\nEmployees sorted by Salary:");
        employees.sort((e1, e2) -> Double.compare(e1.salary, e2.salary));
        employees.forEach(System.out::println);

        List<Student> students = Arrays.asList(
            new Student("Vijay", 85),
            new Student("Bhaskar", 45),
            new Student("Anshu", 72),
            new Student("Deepak", 90)
        );

        System.out.println("\nStudents with marks >= 60 sorted by name:");
        students.stream()
                .filter(s -> s.marks >= 60)
                .sorted(Comparator.comparing(s -> s.name))
                .forEach(System.out::println);

        List<Product> products = Arrays.asList(
            new Product(1, "Laptop", 800),
            new Product(2, "Phone", 500),
            new Product(3, "Monitor", 300),
            new Product(4, "Keyboard", 50)
        );

        System.out.println("\nProducts with price > $100:");
        products.stream()
                .filter(p -> p.price > 100)
                .forEach(System.out::println);

        System.out.println("\nList of product names:");
        List<String> names = products.stream()
                                     .map(p -> p.name)
                                     .collect(Collectors.toList());
        names.forEach(System.out::println);

        double total = products.stream()
                               .mapToDouble(p -> p.price)
                               .sum();
        System.out.println("\nTotal price of all products: $" + total);
    }
}
