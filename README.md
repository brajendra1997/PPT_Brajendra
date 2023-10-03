# PPT_Brajendra

FOR WRITING XML AS DOCUMENT


using System;
using System.Xml;

class Program
{
    static void Main1()
    {
        // Create a new XML document
        XmlDocument xmlDoc = new XmlDocument();

        // Create the root element
        XmlElement rootElement = xmlDoc.CreateElement("Students");
        xmlDoc.AppendChild(rootElement);

        // Add three sets of name, age, and ID elements
        AddStudent(xmlDoc, rootElement, "Dipankar", 25, 1);
        AddStudent(xmlDoc, rootElement, "Debajani", 25, 2);
        AddStudent(xmlDoc, rootElement, "Brajendra", 25, 3);

        // Save the XML document to a file
        string xmlFilePath = "write.xml";
        xmlDoc.Save(xmlFilePath);
        Console.WriteLine("Data written to XML file.");
    }

    static void AddStudent(XmlDocument xmlDoc, XmlElement rootElement, string name, int age, int id)
    {
        XmlElement studentElement = xmlDoc.CreateElement("Student");

        XmlElement nameElement = xmlDoc.CreateElement("Name");
        nameElement.InnerText = name;

        XmlElement ageElement = xmlDoc.CreateElement("Age");
        ageElement.InnerText = age.ToString();

        studentElement.AppendChild(nameElement);
        studentElement.AppendChild(ageElement);

        studentElement.SetAttribute("ID", id.ToString());

        rootElement.AppendChild(studentElement);
    }
}










FOR READING XML AS DOCUMENT




using System;
using System.Xml;

class Program1
{
    static void Main()
    {
        string xmlFilePath = "write.xml";

        // Create a new XML document
        XmlDocument xmlDoc = new XmlDocument();
        xmlDoc.Load(xmlFilePath);

        // Select all "Student" elements
        XmlNodeList studentNodes = xmlDoc.SelectNodes("/Students/Student");

        foreach (XmlNode studentNode in studentNodes)
        {
            string name = studentNode.SelectSingleNode("Name").InnerText;
            string age = studentNode.SelectSingleNode("Age").InnerText;
            string id = ((XmlElement)studentNode).GetAttribute("ID");

            Console.WriteLine("Name: {0}, Age: {1}, ID: {2}",name,age,id);
        }
    }
}





XML File.

<students>
    <student>
        <name>Dipankar</name>
        <age>25</age>
    </student>
    <student>
        <name>Debajani</name>
        <age>25</age>
    </student>
    <student>
        <name>Brajendra</name>
        <age>25</age>
    </student>
</students>







Deserialization code


using System;
using System.Collections.Generic;
using System.IO;
using System.Xml.Serialization;

[Serializable]
[XmlRoot("students")]
public class Students
{
    [XmlElement("student")]
    public List<Student> StudentList { get; set; }
}

public class Student
{
    [XmlElement("name")]
    public string Name { get; set; }

    [XmlElement("age")]
    public int Age { get; set; }
}

class Program
{
    static void Main()
    {
        string xmlFilePath = "Brajendra.xml"; // Replace with the path to your XML file
        string xmlData = File.ReadAllText(xmlFilePath);

        XmlSerializer serializer = new XmlSerializer(typeof(Students));

        using (StringReader reader = new StringReader(xmlData))
        {
            Students students = (Students)serializer.Deserialize(reader);

            foreach (var student in students.StudentList)
            {
                Console.WriteLine("Name:{0}", student.Name);
                Console.WriteLine("Age:{0}", student.Age);
                Console.WriteLine();
            }
        }
    }
}
