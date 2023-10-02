# PPT_Brajendra

FOR WRITING XML AS DOCUMENT


using System;
using System.Xml;

class Program
{
    static void Main()
    {
        // Create an XML document
        XmlDocument xmlDoc = new XmlDocument();

        // Create the root element
        XmlElement rootElement = xmlDoc.CreateElement("Students");
        xmlDoc.AppendChild(rootElement);

        // Create a student element
        XmlElement studentElement = xmlDoc.CreateElement("Student");
        rootElement.AppendChild(studentElement);

        // Add attributes to the student element
        studentElement.SetAttribute("ID", "1");

        // Add child elements to the student element
        XmlElement nameElement = xmlDoc.CreateElement("Name");
        nameElement.InnerText = "John Doe";
        studentElement.AppendChild(nameElement);

        XmlElement ageElement = xmlDoc.CreateElement("Age");
        ageElement.InnerText = "25";
        studentElement.AppendChild(ageElement);

        // Save the XML document to a file
        xmlDoc.Save("students.xml");

        Console.WriteLine("XML document saved successfully.");
    }
}









FOR READING XML AS DOCUMENT




using System;
using System.Xml;

class Program
{
    static void Main()
    {
        // Load the XML document from a file
        XmlDocument xmlDoc = new XmlDocument();
        xmlDoc.Load("students.xml");

        // Get the root element
        XmlElement rootElement = xmlDoc.DocumentElement;

        // Loop through the child elements (students)
        foreach (XmlElement studentElement in rootElement.ChildNodes)
        {
            string studentId = studentElement.GetAttribute("ID");
            string name = studentElement.SelectSingleNode("Name").InnerText;
            string age = studentElement.SelectSingleNode("Age").InnerText;

            Console.WriteLine("Student ID: {0}, Name: {1}, Age: {2} ",studentId,name,age);
        }
    }
}






XML File.

<Student>
    <Name>John Doe</Name>
    <Age>25</Age>
</Student>







Deserialization code


using System;
using System.IO;
using System.Xml.Serialization;

// Define a class that matches the XML structure
[Serializable]
public class Student
{
    public string Name { get; set; }
    public int Age { get; set; }
}

class Program
{
    static void Main()
    {
        // Read the XML data from the file
        string xmlData = File.ReadAllText("student.xml");

        // Create an XmlSerializer for the Student class
        XmlSerializer serializer = new XmlSerializer(typeof(Student));

        // Deserialize the XML data into a Student object
        using (TextReader reader = new StringReader(xmlData))
        {
            Student student = (Student)serializer.Deserialize(reader);

            // Access the deserialized object's properties
            Console.WriteLine("Name: " + student.Name);
            Console.WriteLine("Age: " + student.Age);
        }
    }
}

