---
title: Практическое руководство. Проверка с использованием XSD (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: 6a7f83a9-2d74-4c2b-8417-0a8595879516
ms.openlocfilehash: 47704a5aa06bb837c9d76516762330e4aa24e074
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592238"
---
# <a name="how-to-validate-using-xsd-linq-to-xml-c"></a>Практическое руководство. Проверка с использованием XSD (LINQ to XML) (C#)
Пространство имен <xref:System.Xml.Schema> содержит методы расширения, облегчающие проверку правильности XML-дерева по XSD-файлу. Дополнительные сведения см. в документации метода <xref:System.Xml.Schema.Extensions.Validate%2A>.  
  
## <a name="example"></a>Пример  
 В следующем примере создается набор схем <xref:System.Xml.Schema.XmlSchemaSet>, затем с его помощью проводится проверка правильности двух объектов <xref:System.Xml.Linq.XDocument>. Правильность одного документа подтверждается, а второго - нет.  
  
```csharp  
string xsdMarkup =  
    @"<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'>  
       <xsd:element name='Root'>  
        <xsd:complexType>  
         <xsd:sequence>  
          <xsd:element name='Child1' minOccurs='1' maxOccurs='1'/>  
          <xsd:element name='Child2' minOccurs='1' maxOccurs='1'/>  
         </xsd:sequence>  
        </xsd:complexType>  
       </xsd:element>  
      </xsd:schema>";  
XmlSchemaSet schemas = new XmlSchemaSet();  
schemas.Add("", XmlReader.Create(new StringReader(xsdMarkup)));  
  
XDocument doc1 = new XDocument(  
    new XElement("Root",  
        new XElement("Child1", "content1"),  
        new XElement("Child2", "content1")  
    )  
);  
  
XDocument doc2 = new XDocument(  
    new XElement("Root",  
        new XElement("Child1", "content1"),  
        new XElement("Child3", "content1")  
    )  
);  
  
Console.WriteLine("Validating doc1");  
bool errors = false;  
doc1.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("doc1 {0}", errors ? "did not validate" : "validated");  
  
Console.WriteLine();  
Console.WriteLine("Validating doc2");  
errors = false;  
doc2.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("doc2 {0}", errors ? "did not validate" : "validated");  
```  
  
 В этом примере выводятся следующие данные:  
  
```  
Validating doc1  
doc1 validated  
  
Validating doc2  
The element 'Root' has invalid child element 'Child3'. List of possible elements expected: 'Child2'.  
doc2 did not validate  
```  
  
## <a name="example"></a>Пример  
 В следующем примере подтверждается, что XML-документ из статьи [Пример XML-файла. Заказчики и заказы (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md) является правильным согласно схеме из статьи [Пример XSD-файла. Заказчики и заказы](./sample-xsd-file-customers-and-orders1.md). Затем в исходный XML-документ вносятся изменения. Изменяется атрибут `CustomerID` первого клиента. После этого изменения заказы ссылаются на несуществующего клиента, поэтому XML-документ больше не должен пройти проверку правильности.  
  
 В этом примере используется следующий XML-документ: [Пример XML-файла. Заказчики и заказы (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
 В этом примере используется следующая XSD-схема: [Пример XSD-файла. Заказчики и заказы](./sample-xsd-file-customers-and-orders1.md).  
  
```csharp  
XmlSchemaSet schemas = new XmlSchemaSet();  
schemas.Add("", "CustomersOrders.xsd");  
  
Console.WriteLine("Attempting to validate");  
XDocument custOrdDoc = XDocument.Load("CustomersOrders.xml");  
bool errors = false;  
custOrdDoc.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("custOrdDoc {0}", errors ? "did not validate" : "validated");  
  
Console.WriteLine();  
// Modify the source document so that it will not validate.  
custOrdDoc.Root.Element("Orders").Element("Order").Element("CustomerID").Value = "AAAAA";  
Console.WriteLine("Attempting to validate after modification");  
errors = false;  
custOrdDoc.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("custOrdDoc {0}", errors ? "did not validate" : "validated");  
```  
  
 В этом примере выводятся следующие данные:  
  
```  
Attempting to validate  
custOrdDoc validated  
  
Attempting to validate after modification  
The key sequence 'AAAAA' in Keyref fails to refer to some key.  
custOrdDoc did not validate  
```  
  
## <a name="see-also"></a>См. также

- <xref:System.Xml.Schema.Extensions.Validate%2A>
- [Создание деревьев XML (C#)](creating-xml-trees-linq-to-xml-2.md)
