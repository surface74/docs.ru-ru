---
title: Элемент <Thread_UseAllCpuGroups>
ms.date: 03/30/2017
ms.assetid: d30fe7c5-8469-46e2-b804-e3eec7b24256
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e9ee6bdb7094ea2bc9e283e331c0f6ad9b68e4f9
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/21/2019
ms.locfileid: "69663427"
---
# <a name="thread_useallcpugroups-element"></a>\<Элемент > Thread_UseAllCpuGroups

Указывает, распределяет ли среда выполнения управляемые потоки во всех группах ЦП.

\<> конфигурации \
\<> среды выполнения \
\<Thread_UseAllCpuGroups >

## <a name="syntax"></a>Синтаксис

```xml
<Thread_UseAllCpuGroups
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>Атрибуты и элементы

В следующих разделах описаны атрибуты, дочерние и родительские элементы.

### <a name="attributes"></a>Атрибуты

|Атрибут|Описание|
|---------------|-----------------|
|`enabled`|Обязательный атрибут.<br /><br /> Указывает, распределяет ли среда выполнения управляемые потоки во всех группах ЦП.|

## <a name="enabled-attribute"></a>Атрибут enabled

|Значение|Описание|
|-----------|-----------------|
|`false`|Среда выполнения не распределяет управляемые потоки между несколькими группами ЦП. Это значение по умолчанию.|
|`true`|Среда выполнения распределяет управляемые потоки между несколькими группами ЦП, если компьютер имеет несколько групп ЦП, а [ \<элемент гккпуграуп >](gccpugroup-element.md) включен.|

### <a name="child-elements"></a>Дочерние элементы

Нет.

### <a name="parent-elements"></a>Родительские элементы

|Элемент|Описание|
|-------------|-----------------|
|`configuration`|Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями .NET Framework.|
|`runtime`|Содержит сведения о привязке сборок и сборке мусора.|

## <a name="remarks"></a>Примечания

Если компьютер имеет несколько групп ЦП, включение этого элемента приводит к тому, что среда выполнения распределяет управляемые потоки по всем группам ЦП. Чтобы использовать эту функцию, необходимо также включить [ \<элемент гккпуграуп >](gccpugroup-element.md) , который расширяет сборку мусора на все группы ЦП и учитывает все ядра при создании и балансировке куч. Чтобы включить элемент [> гккпуграуп,необходимовключитьэлемент>gcServer.\<](gccpugroup-element.md) [ \<](gcserver-element.md) Если эти элементы не включены, включение `<Thread_UseAllCpuGroups>` элемента не оказывает никакого влияния.

## <a name="example"></a>Пример

В следующем примере показано, как включить поддержку нескольких групп ЦП.

```xml
<configuration>
   <runtime>
      <Thread_UseAllCpuGroups enabled="true"/>
      <GCCpuGroup enabled="true"/>
      <gcServer enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>См. также

- [Схема параметров среды выполнения](index.md)
- [Схема файла конфигурации](../index.md)
- [\<Элемент > Гккпуграуп](gccpugroup-element.md)
