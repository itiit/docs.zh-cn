---
title: 形参和实参之间的差异
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- parameters [Visual Basic], and arguments
- procedure arguments
- Visual Basic code, procedures
- arguments [Visual Basic], and parameters
- procedure parameters
- parameters [Visual Basic], definition
ms.assetid: c237c056-74f4-4749-9f2c-15864f139a31
ms.openlocfilehash: c4249dbf86bd1bfa7ef08e94059d2880333e9a92
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74341377"
---
# <a name="differences-between-parameters-and-arguments-visual-basic"></a>参数和变量之间的差异 (Visual Basic)
在大多数情况下，过程必须具有有关在其中调用该过程的环境的一些信息。 执行重复或共享任务的过程对每个调用使用不同的信息。 此信息包含变量、常量和在您调用过程时传递给该过程的表达式。  
  
 若要将此信息传递给过程，过程定义了一个*参数*，并且调用代码将*参数*传递给该参数。 可以将参数视为停车空间，将参数视为汽车。 正如不同的汽车可以在不同时间的停车空间中停放一样，每次调用该过程时，调用代码都可以将不同的参数传递给相同的参数。  
  
## <a name="parameters"></a>参数  
 *参数*表示一个值，在调用该过程时，该过程要求您传递该值。 过程声明定义了其参数。  
  
 在定义 `Function` 或 `Sub` 过程时，请在紧跟在过程名称后面的括号中指定*参数列表*。 对于每个参数，可以指定名称、数据类型和传递机制（[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)或[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)）。 还可以指示参数是可选的。 这意味着，调用代码不必为其传递值。  
  
 每个参数的名称作为过程中的*局部变量*。 使用参数名称的方式与使用任何其他变量的方式相同。  
  
## <a name="arguments"></a>参数  
 *参数*表示在调用过程时传递给过程参数的值。 调用代码在调用过程时提供自变量。  
  
 调用 `Function` 或 `Sub` 过程时，将在紧跟过程名称的括号中包含*参数列表*。 每个参数都对应于列表中同一位置的参数。  
  
 与参数定义不同，参数没有名称。 每个自变量都是一个表达式，它可以包含零个或多个变量、常量和文本。 计算表达式的数据类型通常应与为相应参数定义的数据类型匹配，在任何情况下，它都必须可以转换为参数类型。  
  
## <a name="see-also"></a>另请参阅

- [过程](./index.md)
- [Sub 过程](./sub-procedures.md)
- [Function 过程](./function-procedures.md)
- [属性过程](./property-procedures.md)
- [运算符过程](./operator-procedures.md)
- [如何：为过程定义参数](./how-to-define-a-parameter-for-a-procedure.md)
- [如何：将自变量传递给过程](./how-to-pass-arguments-to-a-procedure.md)
- [按值和按引用传递自变量](./passing-arguments-by-value-and-by-reference.md)
- [递归过程](./recursive-procedures.md)
- [过程重载](./procedure-overloading.md)
