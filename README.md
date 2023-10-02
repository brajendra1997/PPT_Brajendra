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
