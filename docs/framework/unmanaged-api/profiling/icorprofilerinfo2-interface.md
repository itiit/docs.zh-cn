---
title: ICorProfilerInfo2 接口
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2
helpviewer_keywords:
- ICorProfilerInfo2 interface [.NET Framework profiling]
ms.assetid: 91bd49b6-4d12-494f-a8f1-2f251e8c65e3
topic_type:
- apiref
ms.openlocfilehash: 23fd44a6865b0487296f3ade37c1219e8feba288
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76862576"
---
# <a name="icorprofilerinfo2-interface"></a>ICorProfilerInfo2 接口
提供代码探查器用于与公共语言运行时（CLR）进行通信以控制事件监视和请求信息的方法。 `ICorProfilerInfo2` 接口是[ICorProfilerInfo](icorprofilerinfo-interface.md)接口的扩展。 也就是说，它提供 .NET Framework 版本2.0 及更高版本中支持的新方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[DoStackSnapshot 方法](icorprofilerinfo2-dostacksnapshot-method.md)|遍历指定线程的堆栈，将托管调用帧报告给探查器。|  
|[EnumModuleFrozenObjects 方法](icorprofilerinfo2-enummodulefrozenobjects-method.md)|获取一个枚举器，该枚举数允许对指定模块中的冻结对象进行迭代。|  
|[GetAppDomainStaticAddress 方法](icorprofilerinfo2-getappdomainstaticaddress-method.md)|获取指定应用程序域静态字段在指定应用程序域范围内的地址。|  
|[GetArrayObjectInfo 方法](icorprofilerinfo2-getarrayobjectinfo-method.md)|获取有关数组对象的详细信息。|  
|[GetBoxClassLayout 方法](icorprofilerinfo2-getboxclasslayout-method.md)|获取有关已装箱的指定值类型的类布局信息。|  
|[GetClassFromTokenAndTypeArgs 方法](icorprofilerinfo2-getclassfromtokenandtypeargs-method.md)|使用指定的元数据标记和任何类型参数的 `ClassID` 值获取类型的 `ClassID`。|  
|[GetClassIDInfo2 方法](icorprofilerinfo2-getclassidinfo2-method.md)|获取指定的泛型类的父模块、类的元数据标记、其父类的 `ClassID`，以及类的每个类型参数（如果存在）的 `ClassID`。|  
|[GetClassLayout 方法](icorprofilerinfo2-getclasslayout-method.md)|获取内存中由指定的类定义的字段的布局信息。 也就是说，此方法获取类的字段的偏移量。|  
|[GetCodeInfo2 方法](icorprofilerinfo2-getcodeinfo2-method.md)|获取与指定 `FunctionID` 关联的本机代码的范围。|  
|[GetContextStaticAddress 方法](icorprofilerinfo2-getcontextstaticaddress-method.md)|获取指定上下文的范围内的指定上下文静态字段的地址。|  
|[GetFunctionFromTokenAndTypeArgs 方法](icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md)|使用指定的元数据标记（包含类）和任何类型参数 `ClassID` 值获取函数的 `FunctionID`。|  
|[GetFunctionInfo2 方法](icorprofilerinfo2-getfunctioninfo2-method.md)|获取每个类型参数或某个函数（如果存在）的父类、元数据标记和 `ClassID`。|  
|[GetGenerationBounds 方法](icorprofilerinfo2-getgenerationbounds-method.md)|获取组成垃圾回收堆的代的内存区域（堆的段）。|  
|[GetNotifiedExceptionClauseInfo 方法](icorprofilerinfo2-getnotifiedexceptionclauseinfo-method.md)|获取即将运行或刚刚运行的异常子句的本机地址和帧信息（`catch`/`finally`/`filter`）。|  
|[GetObjectGeneration 方法](icorprofilerinfo2-getobjectgeneration-method.md)|获取包含指定对象的堆段。|  
|[GetRVAStaticAddress 方法](icorprofilerinfo2-getrvastaticaddress-method.md)|获取指定的相对虚拟地址（RVA）静态字段的地址。|  
|[GetStaticFieldInfo 方法](icorprofilerinfo2-getstaticfieldinfo-method.md)|获取指定字段为静态的作用域。|  
|[GetStringLayout 方法](icorprofilerinfo2-getstringlayout-method.md)|获取有关字符串对象布局的信息。|  
|[GetThreadAppDomain 方法](icorprofilerinfo2-getthreadappdomain-method.md)|获取指定线程当前正在执行代码的应用程序域的 ID。|  
|[GetThreadStaticAddress 方法](icorprofilerinfo2-getthreadstaticaddress-method.md)|获取指定线程范围内的指定线程静态字段的地址。|  
|[SetEnterLeaveFunctionHooks2 方法](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)|指定在托管函数的 "enter"、"leave" 和 "tailcall" 挂钩上调用的探查器实现函数。|  
  
## <a name="remarks"></a>备注  
 探查器调用 `ICorProfilerInfo2` 接口中的方法，以便与 CLR 通信以控制事件监视和请求信息。  
  
 使用自由线程模型的 CLR 实现 `ICorProfilerInfo2` 接口的方法。 每个方法均返回一个 HRESULT，指示成功或失败。 有关可能的返回代码的列表，请参阅 CorError.h 文件。  
  
 当使用探查器的[ICorProfilerCallback：： Initialize](icorprofilercallback-initialize-method.md)实现时，CLR 将 `ICorProfilerInfo2` 接口传递到每个代码探查器。 然后，代码探查器可以调用 `ICorProfilerInfo2` 接口的方法，以获取有关在 CLR 控制下执行的托管代码的信息。  
  
## <a name="requirements"></a>需求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **头文件：** CorProf.idl、CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [Profiling 接口](profiling-interfaces.md)
- [ICorProfilerInfo 接口](icorprofilerinfo-interface.md)
