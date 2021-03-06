---
title: Сборка типов (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 41fa7bde-8d20-4a3f-a3d2-fb791e128010
ms.openlocfilehash: 7113aaf1c2caa982a8ab4751928856c1271570cb
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251125"
---
# <a name="constructing-types-entity-sql"></a>Сборка типов (Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)]предоставляет три вида конструкторов: конструкторы строк, конструкторы именованных типов и конструкторы коллекций.  
  
## <a name="row-constructors"></a>Конструкторы строк  
 В [!INCLUDE[esql](../../../../../../includes/esql-md.md)] конструкторы строк можно использовать для создания анонимных структурно типизированных записей из одного или нескольких значений. Результирующий тип конструктора строк является типом строки, типы полей которого соответствуют типам значений, использовавшихся для создания этой строки. Например, следующее выражение конструирует значение типа `Record(a int, b string, c int)`:  
  
 `ROW(1 AS a, "abc" AS b, a + 34 AS c)`  
  
 Если в конструкторе строк не указан псевдоним для выражения, то платформа Entity Framework попытается сформировать его. Дополнительные сведения см. в разделе "правила присвоения псевдонимов" статьи [идентификаторы](identifiers-entity-sql.md).  
  
 В конструкторе строк псевдонимы присваиваются выражениям по следующим правилам.  
  
- Выражение в конструкторе строк не может ссылаться на другие псевдонимы в этом же конструкторе.  
  
- Два выражения в одном конструкторе строк не могут иметь одинаковый псевдоним.  
  
 Дополнительные сведения о конструкторах строк см. в разделе [Row](row-entity-sql.md).  
  
## <a name="collection-constructors"></a>Конструкторы коллекций  
 В [!INCLUDE[esql](../../../../../../includes/esql-md.md)] конструкторы коллекций можно использовать для создания экземпляра мультинабора из списка значений. Все значения в конструкторе должны иметь взаимно совместимый тип `T`. Конструктор формирует коллекцию типа `Multiset<T>`. Например, следующее выражение создает коллекцию целых чисел.  
  
 `Multiset(1, 2, 3)`  
  
 `{1, 2, 3}`  
  
 Конструкторы пустых мультинаборов не разрешены, так как в этом случае нельзя определить тип элементов. Недопустимый мультинабор:  
  
 `multiset() {}`  
  
 Дополнительные сведения см. в разделе [мультинабор](multiset-entity-sql.md).  
  
## <a name="named-type-constructors-namedtype-initializers"></a>Конструкторы именованных типов (инициализаторы NamedType)  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] позволяет конструкторам типов (инициализаторам) создавать экземпляры именованных сложных типов и типов сущностей. Например, следующее выражение создает экземпляр типа `Person`.  
  
 `Person("abc", 12)`  
  
 Приведенное далее выражение создает экземпляр сложного типа.  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 Приведенное далее выражение создает экземпляр вложенного сложного типа.  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 Приведенное далее выражение создает экземпляр сущности с вложенным сложным типом.  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 В следующем примере показано, как инициализировать свойство сложного типа значением null. `MyModel.ZipCode(‘98118’, null)`  
  
 Предполагается, что аргументы конструктора находятся в порядке, соответствующем порядку декларации атрибутов типа.  
  
 Дополнительные сведения см. в разделе [Конструктор именованного типа](named-type-constructor-entity-sql.md).  
  
## <a name="see-also"></a>См. также

- [Справочник по Entity SQL](entity-sql-reference.md)
- [Общие сведения об Entity SQL](entity-sql-overview.md)
- [Система типов](type-system-entity-sql.md)
