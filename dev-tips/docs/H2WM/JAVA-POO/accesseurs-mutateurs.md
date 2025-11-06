## Accesseur / mot clé :  access

exemple un getter avec le mot clé get

```JAVA
public class Student {

	private String name;

	public String getName() {
		return name;
	}
}
```


## Mutateurs / mot clé : muter

exemple un setter avec le mot clé set

```JAVA
public class Student {

	private String name;

	public void setName(String name) {
		this.name = name;
	}
}
```

```JAVA
import java.util.Arrays;

public class Student {

	private String name;
	private Integer ID;
	private String DOB;
	private double GPA;
	private String[] courses;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Integer getID() {
		return ID;
	}

	public void setID(Integer iD) {
		this.ID = iD;
	}

	public String getDOB() {
		return DOB;
	}

	public void setDOB(String dOB) {
		this.DOB = dOB;
	}

	public double getGPA() {
		return GPA;
	}

	public void setGPA(double gPA) {
		this.GPA = gPA;
	}

	public String[] getCourses() {
		return courses;
	}

	public void setCourses(String[] courses) {
		this.courses = courses;
	}
```

Dans le main 

```JAVA
	public static void main(String[] args) {

		Student student1 = new Student();

		System.out.println("Student Bio [ Before using Accessors & Mutators ]");

		// calling accessor methods
		System.out.print("Name: " + student1.getName());
		System.out.print("\tID: " + student1.getID());
		System.out.print("\tGPA: " + student1.getGPA());
		System.out.print("\tDOB: " + student1.getDOB());
		System.out.println("\tCourses: " +  Arrays.toString(student1.getCourses()));

		// calling mutator methods
		student1.setName("Alex Coy");
		student1.setID(3115);
		student1.setGPA(2.79);
		student1.setDOB("08/08/1998");
		String[] courses = { "Object Oriented Programming", "Cryptography", "Photography", "Network Security" };
		student1.setCourses(courses);

		System.out.println("\nStudent Bio [ After using Mutators & Accessors ]");

		// calling accessor methods
		System.out.print("Name: " + student1.getName());
		System.out.print("\tID: " + student1.getID());
		System.out.print("\tGPA: " + student1.getGPA());
		System.out.print("\tDOB: " + student1.getDOB());
		System.out.println("\tCourses: " + Arrays.toString(student1.getCourses()));
	}
}
```

Rendu Terminal:

![alt text](img/getter-setter.png)
