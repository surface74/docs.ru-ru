---
title: Внешнее сопоставление
ms.date: 03/30/2017
ms.assetid: 076606b8-d889-4ba0-b5da-ae577b146f23
ms.openlocfilehash: 70372473eb2de5d3c4751e237e7beb66315b690e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950332"
---
# <a name="external-mapping"></a>Внешнее сопоставление
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]поддерживает *внешнее сопоставление*— процесс, в котором используется отдельный XML-файл для указания сопоставления между моделью данных базы данных и объектной моделью. Файл внешнего сопоставления имеет следующие преимущества.  
  
- Код сопоставления можно хранить вне кода приложения. Этот подход уменьшает перегруженность кода приложения.  
  
- Файл внешнего сопоставления можно считать подобным файлу конфигурации. Например, можно изменить поведение приложения после предоставления двоичных файлов, просто выгрузив файл внешнего сопоставления.  
  
## <a name="requirements"></a>Требования  
 Файл сопоставления должен быть XML-файлом, а файл должен быть проверен на [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] соответствие с файлом определения схемы (XSD).  
  
 Действуют следующие правила.  
  
- Файл сопоставления должен быть файлом XML.  
  
- Файл сопоставления XML должен быть проверен на соответствие файлу определения схемы XML. Дополнительные сведения см. в разделе [Практическое руководство. Проверьте DBML и внешние файлы](../../../../../../docs/framework/data/adonet/sql/linq/how-to-validate-dbml-and-external-mapping-files.md)сопоставления.  
  
- Внешнее сопоставление переопределяет сопоставление на основе атрибутов. Другими словами, если для создания <xref:System.Data.Linq.DataContext> используется источник внешнего сопоставления, <xref:System.Data.Linq.DataContext> игнорирует все созданные в классах атрибуты сопоставления. Данная модель работает, если класс включен в файл внешнего сопоставления.  
  
- [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] не поддерживает комбинированное использование двух типов сопоставлений (на основе атрибутов и внешнее).  
  
## <a name="xml-schema-definition-file"></a>Файл определения схемы XML  
 Внешнее сопоставление в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] должно быть проверено на соответствие определению схемы XML.  
  
 Следует отличать этот файл определения схемы от файла определения схемы, который используется для проверки DBML-файла. Дополнительные сведения см. [в разделе Создание кода в LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)).  
  
> [!NOTE]
> Пользователи Visual Studio также будут искать этот XSD-файл в диалоговом окне схемы XML в формате "Линктосклмаппинг. xsd". Чтобы правильно использовать этот файл для проверки внешнего файла сопоставления, см. [раздел как Проверьте DBML и внешние файлы](../../../../../../docs/framework/data/adonet/sql/linq/how-to-validate-dbml-and-external-mapping-files.md)сопоставления.  
  
```  
?<?xml version="1.0" encoding="utf-16"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="http://schemas.microsoft.com/linqtosql/mapping/2007" xmlns="http://schemas.microsoft.com/linqtosql/mapping/2007"  
elementFormDefault="qualified" >  
  <xs:element name="Database" type="Database" />  
  <xs:complexType name="Database">  
    <xs:sequence>  
      <xs:element name="Table" type="Table" minOccurs="0" maxOccurs="unbounded" />  
      <xs:element name="Function" type="Function" minOccurs="0" maxOccurs="unbounded" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Provider" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Table">  
    <xs:sequence>  
      <xs:element name="Type" type="Type" minOccurs="1" maxOccurs="1" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Type">  
    <xs:sequence>  
      <xs:choice minOccurs="0" maxOccurs="unbounded">  
        <xs:element name="Column" type="Column" minOccurs="0" maxOccurs="unbounded" />  
        <xs:element name="Association" type="Association" minOccurs="0" maxOccurs="unbounded" />  
      </xs:choice>  
      <xs:element name="Type" type="Type" minOccurs="0" maxOccurs="unbounded" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="required" />  
    <xs:attribute name="InheritanceCode" type="xs:string" use="optional" />  
    <xs:attribute name="IsInheritanceDefault" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Column">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="required" />  
    <xs:attribute name="Storage" type="xs:string" use="optional" />  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
    <xs:attribute name="IsPrimaryKey" type="xs:boolean" use="optional" />  
    <xs:attribute name="IsDbGenerated" type="xs:boolean" use="optional" />  
    <xs:attribute name="CanBeNull" type="xs:boolean" use="optional" />  
    <xs:attribute name="UpdateCheck" type="UpdateCheck" use="optional" />  
    <xs:attribute name="IsDiscriminator" type="xs:boolean" use="optional" />  
    <xs:attribute name="Expression" type="xs:string" use="optional" />  
    <xs:attribute name="IsVersion" type="xs:boolean" use="optional" />  
    <xs:attribute name="AutoSync" type="AutoSync" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Association">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="required" />  
    <xs:attribute name="Storage" type="xs:string" use="optional" />  
    <xs:attribute name="ThisKey" type="xs:string" use="optional" />  
    <xs:attribute name="OtherKey" type="xs:string" use="optional" />  
    <xs:attribute name="IsForeignKey" type="xs:boolean" use="optional" />  
    <xs:attribute name="IsUnique" type="xs:boolean" use="optional" />  
    <xs:attribute name="DeleteRule" type="xs:string" use="optional" />  
    <xs:attribute name="DeleteOnNull" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Function">  
    <xs:sequence>  
      <xs:element name="Parameter" type="Parameter" minOccurs="0" maxOccurs="unbounded" />  
      <xs:choice>  
        <xs:element name="ElementType" type="Type" minOccurs="0" maxOccurs="unbounded" />  
        <xs:element name="Return" type="Return" minOccurs="0" maxOccurs="1" />  
      </xs:choice>  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Method" type="xs:string" use="required" />  
    <xs:attribute name="IsComposable" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Parameter">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Parameter" type="xs:string" use="required" />  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
    <xs:attribute name="Direction" type="ParameterDirection" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Return">  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:simpleType name="UpdateCheck">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="Always" />  
      <xs:enumeration value="Never" />  
      <xs:enumeration value="WhenChanged" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="ParameterDirection">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="In" />  
      <xs:enumeration value="Out" />  
      <xs:enumeration value="InOut" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="AutoSync">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="Never" />  
      <xs:enumeration value="OnInsert" />  
      <xs:enumeration value="OnUpdate" />  
      <xs:enumeration value="Always" />  
      <xs:enumeration value="Default" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
```  
  
## <a name="see-also"></a>См. также

- [Создание кода в LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
- [Ссылки](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)
- [Практическое руководство. Создать объектную модель как внешний файл](../../../../../../docs/framework/data/adonet/sql/linq/how-to-generate-the-object-model-as-an-external-file.md)
