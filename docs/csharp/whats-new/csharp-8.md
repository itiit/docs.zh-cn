---
title: C# 8.0 中的新增功能 - C# 指南
description: 简要介绍 C# 8.0 中提供的新功能。 本文使用最新的预览版 2。
ms.date: 02/12/2019
ms.openlocfilehash: 874420775215502ebdacb8420b3fe0e027d6660f
ms.sourcegitcommit: 8f95d3a37e591963ebbb9af6e90686fd5f3b8707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56747617"
---
# <a name="whats-new-in-c-80"></a><span data-ttu-id="17d16-104">C# 8.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="17d16-104">What's new in C# 8.0</span></span>

<span data-ttu-id="17d16-105">C# 语言有许多增强功能，可以通过预览版 2 进行试用。</span><span class="sxs-lookup"><span data-stu-id="17d16-105">There are many enhancements to the C# language that you can try out already with preview 2.</span></span> <span data-ttu-id="17d16-106">预览版 2 中的新增功能包括：</span><span class="sxs-lookup"><span data-stu-id="17d16-106">The new features added in preview 2 are:</span></span>

- <span data-ttu-id="17d16-107">[模式匹配增强功能](#more-patterns-in-more-places)：</span><span class="sxs-lookup"><span data-stu-id="17d16-107">[Pattern matching enhancements](#more-patterns-in-more-places):</span></span>
  * [<span data-ttu-id="17d16-108">Switch 表达式</span><span class="sxs-lookup"><span data-stu-id="17d16-108">Switch expressions</span></span>](#switch-expressions)
  * [<span data-ttu-id="17d16-109">属性模式</span><span class="sxs-lookup"><span data-stu-id="17d16-109">Property patterns</span></span>](#property-patterns)
  * [<span data-ttu-id="17d16-110">元组模式</span><span class="sxs-lookup"><span data-stu-id="17d16-110">Tuple patterns</span></span>](#tuple-patterns)
  * [<span data-ttu-id="17d16-111">位置模式</span><span class="sxs-lookup"><span data-stu-id="17d16-111">Positional patterns</span></span>](#positional-patterns)
- [<span data-ttu-id="17d16-112">Using 声明</span><span class="sxs-lookup"><span data-stu-id="17d16-112">Using declarations</span></span>](#using-declarations)
- [<span data-ttu-id="17d16-113">静态本地函数</span><span class="sxs-lookup"><span data-stu-id="17d16-113">Static local functions</span></span>](#static-local-functions)
- [<span data-ttu-id="17d16-114">可处置的 ref 结构</span><span class="sxs-lookup"><span data-stu-id="17d16-114">Disposable ref structs</span></span>](#disposable-ref-structs)

<span data-ttu-id="17d16-115">以下语言功能最先出现在 C# 8.0 预览版 1 中：</span><span class="sxs-lookup"><span data-stu-id="17d16-115">The following language features first appeared in C# 8.0 preview 1:</span></span>

- [<span data-ttu-id="17d16-116">可为空引用类型</span><span class="sxs-lookup"><span data-stu-id="17d16-116">Nullable reference types</span></span>](#nullable-reference-types)
- [<span data-ttu-id="17d16-117">异步流</span><span class="sxs-lookup"><span data-stu-id="17d16-117">Asynchronous streams</span></span>](#asynchronous-streams)
- [<span data-ttu-id="17d16-118">索引和范围</span><span class="sxs-lookup"><span data-stu-id="17d16-118">Indices and ranges</span></span>](#indices-and-ranges)

> [!NOTE]
> <span data-ttu-id="17d16-119">本文针对 C# 8.0 预览版 2 进行了最后一次更新。</span><span class="sxs-lookup"><span data-stu-id="17d16-119">This article was last updated for C# 8.0 preview 2.</span></span>

<span data-ttu-id="17d16-120">本文的剩余部分将简要介绍这些功能。</span><span class="sxs-lookup"><span data-stu-id="17d16-120">The remainder of this article briefly describes these features.</span></span> <span data-ttu-id="17d16-121">如果有详细讲解的文章，则将提供指向这些教程和概述的链接。</span><span class="sxs-lookup"><span data-stu-id="17d16-121">Where in-depth articles are available, links to those tutorials and overviews are provided.</span></span>

## <a name="more-patterns-in-more-places"></a><span data-ttu-id="17d16-122">在更多位置中使用更多模式</span><span class="sxs-lookup"><span data-stu-id="17d16-122">More patterns in more places</span></span>

<span data-ttu-id="17d16-123">模式匹配提供了在相关但不同类型的数据中提供形状相关功能的工具。</span><span class="sxs-lookup"><span data-stu-id="17d16-123">**Pattern matching** gives tools to provide shape-dependent functionality across related but different kinds of data.</span></span> <span data-ttu-id="17d16-124">C# 7.0 通过使用 [`is`](../language-reference/keywords/is.md) 表达式和 [`switch`](../language-reference/keywords/switch.md) 语句引入了类型模式和常量模式的语法。</span><span class="sxs-lookup"><span data-stu-id="17d16-124">C# 7.0 introduced syntax for type patterns and constant patterns by using the [`is`](../language-reference/keywords/is.md) expression and the [`switch`](../language-reference/keywords/switch.md) statement.</span></span> <span data-ttu-id="17d16-125">这些功能代表了支持数据和功能分离的编程范例的初步尝试。</span><span class="sxs-lookup"><span data-stu-id="17d16-125">These features represented the first tentative steps toward supporting programming paradigms where data and functionality live apart.</span></span> <span data-ttu-id="17d16-126">随着行业转向更多微服务和其他基于云的体系结构，还需要其他语言工具。</span><span class="sxs-lookup"><span data-stu-id="17d16-126">As the industry moves toward more microservices and other cloud-based architectures, other language tools are needed.</span></span>

<span data-ttu-id="17d16-127">C# 8.0 扩展了此词汇表，这样就可以在代码中的更多位置使用更多模式表达式。</span><span class="sxs-lookup"><span data-stu-id="17d16-127">C# 8.0 expands this vocabulary so you can use more pattern expressions in more places in your code.</span></span> <span data-ttu-id="17d16-128">当数据和功能分离时，请考虑使用这些功能。</span><span class="sxs-lookup"><span data-stu-id="17d16-128">Consider these features when your data and functionality are separate.</span></span> <span data-ttu-id="17d16-129">当算法依赖于对象运行时类型以外的事实时，请考虑使用模式匹配。</span><span class="sxs-lookup"><span data-stu-id="17d16-129">Consider pattern matching when your algorithms depend on a fact other than the runtime type of an object.</span></span> <span data-ttu-id="17d16-130">这些技术提供了另一种表达设计的方式。</span><span class="sxs-lookup"><span data-stu-id="17d16-130">These techniques provide another way to express designs.</span></span>

<span data-ttu-id="17d16-131">除了可以在新位置使用新模式之外，C# 8.0 还添加了“递归模式”。</span><span class="sxs-lookup"><span data-stu-id="17d16-131">In addition to new patterns in new places, C# 8.0 adds **recursive patterns**.</span></span> <span data-ttu-id="17d16-132">任何模式表达式的结果都是一个表达式。</span><span class="sxs-lookup"><span data-stu-id="17d16-132">The result of any pattern expression is an expression.</span></span> <span data-ttu-id="17d16-133">递归模式只是应用于另一个模式表达式输出的模式表达式。</span><span class="sxs-lookup"><span data-stu-id="17d16-133">A recursive pattern is simply a pattern expression applied to the output of another pattern expression.</span></span>

### <a name="switch-expressions"></a><span data-ttu-id="17d16-134">Switch 表达式</span><span class="sxs-lookup"><span data-stu-id="17d16-134">switch expressions</span></span>

<span data-ttu-id="17d16-135">通常情况下，[`switch`](../language-reference/keywords/switch.md) 语句在其每个 `case` 块中生成一个值。</span><span class="sxs-lookup"><span data-stu-id="17d16-135">Often, a [`switch`](../language-reference/keywords/switch.md) statement produces a value in each of its `case` blocks.</span></span> <span data-ttu-id="17d16-136">借助 Switch 表达式，可以使用更简洁的表达式语法。</span><span class="sxs-lookup"><span data-stu-id="17d16-136">**Switch expressions** enable you to use more concise expression syntax.</span></span> <span data-ttu-id="17d16-137">只有些许重复的 `case` 和 `break` 关键字和大括号。</span><span class="sxs-lookup"><span data-stu-id="17d16-137">There are fewer repetitive `case` and `break` keywords, and fewer curly braces.</span></span>  <span data-ttu-id="17d16-138">以下面列出彩虹颜色的枚举为例：</span><span class="sxs-lookup"><span data-stu-id="17d16-138">As an example, consider the following enum that lists the colors of the rainbow:</span></span>

```csharp
public enum Rainbow
{
    Red,
    Orange,
    Yellow,
    Blue,
    Indigo,
    Violet
}
```

<span data-ttu-id="17d16-139">可以使用以下包含 swith 表达式的方法将 `Rainbow` 值转换为其 RGB 值：</span><span class="sxs-lookup"><span data-stu-id="17d16-139">You could convert a `Rainbow` value to its RGB values using the following method containing a switch expression:</span></span>

```csharp
public static RGBColor FromRainbow(Rainbow colorBand) =>
    colorBand switch
    {
        Rainbow.Red    => new RGBColor(0xFF, 0x00, 0x00),
        Rainbow.Orange => new RGBColor(0xFF, 0x7F, 0x00),
        Rainbow.Yellow => new RGBColor(0xFF, 0xFF, 0x00),
        Rainbow.Blue   => new RGBColor(0x00, 0x00, 0xFF),
        Rainbow.Indigo => new RGBColor(0x4B, 0x00, 0x82),
        Rainbow.Violet => new RGBColor(0x94, 0x00, 0xD3),
        _              => throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand)),
    };
```

<span data-ttu-id="17d16-140">这里有几个语法改进：</span><span class="sxs-lookup"><span data-stu-id="17d16-140">There are several syntax improvements here:</span></span>

- <span data-ttu-id="17d16-141">变量位于 `switch` 关键字之前。</span><span class="sxs-lookup"><span data-stu-id="17d16-141">The variable comes before the `switch` keyword.</span></span> <span data-ttu-id="17d16-142">不同的顺序使得在视觉上可以很轻松地区分 switch 表达式和 switch 语句。</span><span class="sxs-lookup"><span data-stu-id="17d16-142">The different order makes it visually easy to distinguish the switch expression from the switch statement.</span></span>
- <span data-ttu-id="17d16-143">将 `case` 和 `:` 元素替换为 `=>`。</span><span class="sxs-lookup"><span data-stu-id="17d16-143">The `case` and `:` elements are replaced with `=>`.</span></span> <span data-ttu-id="17d16-144">它更简洁，更直观。</span><span class="sxs-lookup"><span data-stu-id="17d16-144">It's more concise and intuitive.</span></span>
- <span data-ttu-id="17d16-145">将 `default` 事例替换为 `_` 弃元。</span><span class="sxs-lookup"><span data-stu-id="17d16-145">The `default` case is replaced with a `_` discard.</span></span>
- <span data-ttu-id="17d16-146">正文是表达式，不是语句。</span><span class="sxs-lookup"><span data-stu-id="17d16-146">The bodies are expressions, not statements.</span></span>

<span data-ttu-id="17d16-147">将其与使用经典 `switch` 语句的等效代码进行对比：</span><span class="sxs-lookup"><span data-stu-id="17d16-147">Contrast that with the equivalent code using the classic `switch` statement:</span></span>

```csharp
public static RGBColor fromRainbowClassic(Rainbow colorBand)
{
    switch (colorBand)
    {
        case Rainbow.Red:
            return new RGBColor(0xFF, 0x00, 0x00);
        case Rainbow.Orange:
            return new RGBColor(0xFF, 0x7F, 0x00);
        case Rainbow.Yellow:
            return new RGBColor(0xFF, 0xFF, 0x00);
        case Rainbow.Blue:
            return new RGBColor(0x00, 0x00, 0xFF);
        case Rainbow.Indigo:
            return new RGBColor(0x4B, 0x00, 0x82);
        case Rainbow.Violet:
            return new RGBColor(0x94, 0x00, 0xD3);
        default:
            throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand));
    };
}
```

### <a name="property-patterns"></a><span data-ttu-id="17d16-148">属性模式</span><span class="sxs-lookup"><span data-stu-id="17d16-148">Property patterns</span></span>

<span data-ttu-id="17d16-149">借助属性模式，可以匹配所检查的对象的属性。</span><span class="sxs-lookup"><span data-stu-id="17d16-149">The **property pattern** enables you to match on properties of the object examined.</span></span> <span data-ttu-id="17d16-150">请看一个电子商务网站的示例，该网站必须根据买家地址计算销售税。</span><span class="sxs-lookup"><span data-stu-id="17d16-150">Consider an eCommerce site that must compute sales tax based on the buyer's address.</span></span> <span data-ttu-id="17d16-151">这种计算不是 `Address` 类的核心职责。</span><span class="sxs-lookup"><span data-stu-id="17d16-151">That computation is not a core responsibility of an `Address` class.</span></span> <span data-ttu-id="17d16-152">它会随时间变化，可能比地址格式的更改更频繁。</span><span class="sxs-lookup"><span data-stu-id="17d16-152">It will change over time, likely more often than address format changes.</span></span> <span data-ttu-id="17d16-153">销售税的金额取决于地址的 `State` 属性。</span><span class="sxs-lookup"><span data-stu-id="17d16-153">The amount of sales tax depends on the `State` property of the address.</span></span> <span data-ttu-id="17d16-154">下面的方法使用属性模式从地址和价格计算销售税：</span><span class="sxs-lookup"><span data-stu-id="17d16-154">The following method uses the property pattern to compute the sales tax from the address and the price:</span></span>

```csharp
public static decimal ComputeSalesTax(Address location, decimal salePrice) =>
    location switch
    {
        { State: "WA" } => salePrice * 0.06M,
        { State: "MN" } => salePrice * 0.75M,
        { State: "MI" } => salePrice * 0.05M,
        // other cases removed for brevity...
        _ => 0M
    };
    ```

Pattern matching creates a concise syntax for expressing this algorithm.

### Tuple patterns

Some algorithms depend on multiple inputs. **Tuple patterns** allow you to switch based on multiple values expressed as a [tuple](../tuples.md).  The following code shows a switch expression for the game *rock, paper, scissors*:

```csharp
public static string RockPaperScissors(string first, string second)
    => (first, second) switch
    {
        ("rock", "paper") => "rock is covered by paper. Paper wins.",
        ("rock", "scissors") => "rock breaks scissors. Rock wins.",
        ("paper", "rock") => "paper covers rock. Paper wins.",
        ("paper", "scissors") => "paper is cut by scissors. Scissors wins.",
        ("scissors", "rock") => "scissors is broken by rock. Rock wins.",
        ("scissors", "paper") => "scissors cuts paper. Scissors wins.",
        (_, _) => "tie"
    };
    ```

The messages indicate the winner. The discard case represents the three combinations for ties, or other text inputs.

### Positional patterns

Some types include a `Deconstruct` method that deconstructs its properties into discrete variables. When a `Deconstruct` method is accessible, you can use **positional patterns** to inspect properties of the object and use those properties for a pattern.  Consider the following `Point` class that includes a `Deconstruct` method to create discrete variables for `X` and `Y`:

```csharp
public class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) => (X, Y) = (x, y);

    public void Deconstruct(out int x, out int y) =>
        (x, y) = (X, Y);
}
```

<span data-ttu-id="17d16-155">下面的方法使用位置模式来提取 `x` 和 `y` 的值。</span><span class="sxs-lookup"><span data-stu-id="17d16-155">The following method uses the **positional pattern** to extract the values of `x` and `y`.</span></span> <span data-ttu-id="17d16-156">然后，它使用 `when` 子句来确定该点的象限：</span><span class="sxs-lookup"><span data-stu-id="17d16-156">Then, it uses a `when` clause to determine the quadrant of the point:</span></span>

```csharp
static string Quadrant(Point p) => p switch
{
    (0, 0) => "origin",
    (var x, var y) when x > 0 && y > 0 => "Quadrant 1",
    (var x, var y) when x < 0 && y > 0 => "Quadrant 2",
    (var x, var y) when x < 0 && y < 0 => "Quadrant 3",
    (var x, var y) when x > 0 && y < 0 => "Quadrant 4",
    (var x, var y) => "on a border",
    _ => "unknown"
};
```

<span data-ttu-id="17d16-157">当 `x` 或 `y` 为 0（但不是两者同时为 0）时，前一个开关中的弃元模式匹配。</span><span class="sxs-lookup"><span data-stu-id="17d16-157">The discard pattern in the preceding switch matches when either `x` or `y`, but not both, is 0.</span></span> <span data-ttu-id="17d16-158">Switch 表达式必须要么生成值，要么引发异常。</span><span class="sxs-lookup"><span data-stu-id="17d16-158">A switch expression must either produce a value or throw an exception.</span></span> <span data-ttu-id="17d16-159">如果这些情况都不匹配，则 switch 表达式将引发异常。</span><span class="sxs-lookup"><span data-stu-id="17d16-159">If none of the cases match, the switch expression throws an exception.</span></span> <span data-ttu-id="17d16-160">如果没有在 switch 表达式中涵盖所有可能的情况，编译器将生成一个警告。</span><span class="sxs-lookup"><span data-stu-id="17d16-160">The compiler generates a warning for you if you do not cover all possible cases in your switch expression.</span></span>

## <a name="using-declarations"></a><span data-ttu-id="17d16-161">using 声明</span><span class="sxs-lookup"><span data-stu-id="17d16-161">using declarations</span></span>

<span data-ttu-id="17d16-162">using 声明是前面带 `using` 关键字的变量声明。</span><span class="sxs-lookup"><span data-stu-id="17d16-162">A **using declaration** is a variable declaration preceded by the `using` keyword.</span></span> <span data-ttu-id="17d16-163">它指示编译器声明的变量应在封闭范围的末尾进行处理。</span><span class="sxs-lookup"><span data-stu-id="17d16-163">It tells the compiler that the variable being declared should be disposed at the end of the enclosing scope.</span></span> <span data-ttu-id="17d16-164">以下面编写文本文件的代码为例：</span><span class="sxs-lookup"><span data-stu-id="17d16-164">For example, consider the following code that writes a text file:</span></span>

```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using var file = new System.IO.StreamWriter("WriteLines2.txt");
    foreach (string line in lines)
    {
        // If the line doesn't contain the word 'Second', write the line to the file.
        if (!line.Contains("Second"))
        {
            file.WriteLine(line);
        }
    }
// file is disposed here
}
```

<span data-ttu-id="17d16-165">在前面的示例中，当到达方法的右括号时，将对该文件进行处理。</span><span class="sxs-lookup"><span data-stu-id="17d16-165">In the preceding example, the file is disposed when the closing brace for the method is reached.</span></span> <span data-ttu-id="17d16-166">这是声明 `file` 的范围的末尾。</span><span class="sxs-lookup"><span data-stu-id="17d16-166">That's the end of the scope in which `file` is declared.</span></span> <span data-ttu-id="17d16-167">前面的代码相当于下面使用经典 [using 语句](../language-reference/keywords/using-statement.md)语句的代码：</span><span class="sxs-lookup"><span data-stu-id="17d16-167">The preceding code is equivalent to the following code using the classic [using statements](../language-reference/keywords/using-statement.md) statement:</span></span>


```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using (var file = new System.IO.StreamWriter("WriteLines2.txt"))
    {
        foreach (string line in lines)
        {
            // If the line doesn't contain the word 'Second', write the line to the file.
            if (!line.Contains("Second"))
            {
                file.WriteLine(line);
            }
        }
    } // file is disposed here
}
```

<span data-ttu-id="17d16-168">在前面的示例中，当到达与 `using` 语句关联的右括号时，将对该文件进行处理。</span><span class="sxs-lookup"><span data-stu-id="17d16-168">In the preceding example, the file is disposed when the closing brace associated with the `using` statement is reached.</span></span>

<span data-ttu-id="17d16-169">在这两种情况下，编译器将生成对 `Dispose()` 的调用。</span><span class="sxs-lookup"><span data-stu-id="17d16-169">In both cases, the compiler generates the call to `Dispose()`.</span></span> <span data-ttu-id="17d16-170">如果 using 语句中的表达式不可处置，编译器将生成一个错误。</span><span class="sxs-lookup"><span data-stu-id="17d16-170">The compiler generates an error if the expression in the using statement is not disposable.</span></span>

## <a name="static-local-functions"></a><span data-ttu-id="17d16-171">静态本地函数</span><span class="sxs-lookup"><span data-stu-id="17d16-171">Static local functions</span></span>

<span data-ttu-id="17d16-172">现在可以向本地函数添加 `static` 修饰符，以确保本地函数不会从封闭范围捕获（引用）任何变量。</span><span class="sxs-lookup"><span data-stu-id="17d16-172">You can now add the `static` modifier to local functions to ensure that local function doesn't capture (reference) any variables from the enclosing scope.</span></span> <span data-ttu-id="17d16-173">这样做会生成 `CS8421`，“静态本地函数不能包含对 <variable> 的引用。”</span><span class="sxs-lookup"><span data-stu-id="17d16-173">Doing so generates `CS8421`, "A static local function can't contain a reference to <variable>."</span></span> 

<span data-ttu-id="17d16-174">考虑下列代码。</span><span class="sxs-lookup"><span data-stu-id="17d16-174">Consider the following code.</span></span> <span data-ttu-id="17d16-175">本地函数 `LocalFunction` 访问在封闭范围（方法 `M`）中声明的变量 `y`。</span><span class="sxs-lookup"><span data-stu-id="17d16-175">The local function `LocalFunction` accesses the variable `y`, declared in the enclosing scope (the method `M`).</span></span> <span data-ttu-id="17d16-176">因此，不能用 `static` 修饰符来声明 `LocalFunction`：</span><span class="sxs-lookup"><span data-stu-id="17d16-176">Therefore, `LocalFunction` can't be declared with the `static` modifier:</span></span>

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

<span data-ttu-id="17d16-177">下面的代码包含一个静态本地函数。</span><span class="sxs-lookup"><span data-stu-id="17d16-177">The following code contains a static local function.</span></span> <span data-ttu-id="17d16-178">它可以是静态的，因为它不访问封闭范围中的任何变量：</span><span class="sxs-lookup"><span data-stu-id="17d16-178">It can be static because it doesn't access any variables in the enclosing scope:</span></span>

```csharp
int M()
{
    int y = 5;
    int x = 7;
    return Add(x, y);

    static int Add(int left, int right) => left + right;
}
```

## <a name="disposable-ref-structs"></a><span data-ttu-id="17d16-179">可处置的 ref 结构</span><span class="sxs-lookup"><span data-stu-id="17d16-179">Disposable ref structs</span></span>

<span data-ttu-id="17d16-180">用 `ref` 修饰符声明的 `struct` 可能无法实现任何接口，因此无法实现 <xref:System.IDisposable>。</span><span class="sxs-lookup"><span data-stu-id="17d16-180">A `struct` declared with the `ref` modifier may not implement any interfaces and so cannot implement <xref:System.IDisposable>.</span></span> <span data-ttu-id="17d16-181">因此，要能够处理 `ref struct`，它必须有一个可访问的 `void Dispose()` 方法。</span><span class="sxs-lookup"><span data-stu-id="17d16-181">Therefore, to enable a `ref struct` to be disposed, it must have an accessible `void Dispose()` method.</span></span> <span data-ttu-id="17d16-182">这同样适用于 `readonly ref struct` 声明。</span><span class="sxs-lookup"><span data-stu-id="17d16-182">This also applies to `readonly ref struct` declarations.</span></span>

## <a name="nullable-reference-types"></a><span data-ttu-id="17d16-183">可为空引用类型</span><span class="sxs-lookup"><span data-stu-id="17d16-183">Nullable reference types</span></span>

<span data-ttu-id="17d16-184">在可为空注释上下文中，引用类型的任何变量都被视为不可为空引用类型。</span><span class="sxs-lookup"><span data-stu-id="17d16-184">Inside a nullable annotation context, any variable of a reference type is considered to be a **nonnullable reference type**.</span></span> <span data-ttu-id="17d16-185">若要指示一个变量可能为 null，必须在类型名称后面附加 `?`，以将该变量声明为可为空引用类型。</span><span class="sxs-lookup"><span data-stu-id="17d16-185">If you want to indicate that a variable may be null, you must append the type name with the `?` to declare the variable as a **nullable reference type**.</span></span>

<span data-ttu-id="17d16-186">对于不可为空引用类型，编译器使用流分析来确保在声明时将本地变量初始化为非 Null 值。</span><span class="sxs-lookup"><span data-stu-id="17d16-186">For nonnullable reference types, the compiler uses flow analysis to ensure that local variables are initialized to a non-null value when declared.</span></span> <span data-ttu-id="17d16-187">字段必须在构造过程中初始化。</span><span class="sxs-lookup"><span data-stu-id="17d16-187">Fields must be initialized during construction.</span></span> <span data-ttu-id="17d16-188">如果没有通过调用任何可用的构造函数或通过初始化表达式来设置变量，编译器将生成警告。</span><span class="sxs-lookup"><span data-stu-id="17d16-188">The compiler generates a warning if the variable is not set by a call to any of the available constructors or by an initializer.</span></span> <span data-ttu-id="17d16-189">此外，不能向不可为空引用类型分配一个可以为 Null 的值。</span><span class="sxs-lookup"><span data-stu-id="17d16-189">Furthermore, nonnullable reference types can't be assigned a value that could be null.</span></span>

<span data-ttu-id="17d16-190">不对可为空引用类型进行检查以确保它们没有被赋予 Null 值或初始化为 Null。</span><span class="sxs-lookup"><span data-stu-id="17d16-190">Nullable reference types aren't checked to ensure they aren't assigned or initialized to null.</span></span> <span data-ttu-id="17d16-191">不过，编译器使用流分析来确保可为空引用类型的任何变量在被访问或分配给不可为空引用类型之前，都会对其 Null 性进行检查。</span><span class="sxs-lookup"><span data-stu-id="17d16-191">However, the compiler uses flow analysis to ensure that any variable of a nullable reference type is checked against null before it's accessed or assigned to a nonnullable reference type.</span></span>

<span data-ttu-id="17d16-192">可以在[可为空引用类型](../nullable-references.md)的概述中了解该功能的更多信息。</span><span class="sxs-lookup"><span data-stu-id="17d16-192">You can learn more about the feature in the overview of [nullable reference types](../nullable-references.md).</span></span> <span data-ttu-id="17d16-193">可以在此[可为空引用类型教程](../tutorials/nullable-reference-types.md)中的新应用程序中自行尝试。</span><span class="sxs-lookup"><span data-stu-id="17d16-193">Try it yourself in a new application in this [nullable reference types tutorial](../tutorials/nullable-reference-types.md).</span></span> <span data-ttu-id="17d16-194">在[迁移应用程序以使用可为空引用类型教程](../tutorials/upgrade-to-nullable-references.md)中了解迁移现有代码库以使用可为空引用类型的步骤。</span><span class="sxs-lookup"><span data-stu-id="17d16-194">Learn about the steps to migrate an existing codebase to make use of nullable reference types in the [migrating an application to use nullable reference types tutorial](../tutorials/upgrade-to-nullable-references.md).</span></span>

## <a name="asynchronous-streams"></a><span data-ttu-id="17d16-195">异步流</span><span class="sxs-lookup"><span data-stu-id="17d16-195">Asynchronous streams</span></span>

<span data-ttu-id="17d16-196">从 C# 8.0 开始，可以创建并以异步方式使用流。</span><span class="sxs-lookup"><span data-stu-id="17d16-196">Starting with C# 8.0, you can create and consume streams asynchronously.</span></span> <span data-ttu-id="17d16-197">返回异步流的方法有三个属性：</span><span class="sxs-lookup"><span data-stu-id="17d16-197">A method that returns an asynchronous stream has three properties:</span></span>

1. <span data-ttu-id="17d16-198">它是用 `async` 修饰符声明的。</span><span class="sxs-lookup"><span data-stu-id="17d16-198">It was declared with the `async` modifier.</span></span>
1. <span data-ttu-id="17d16-199">它将返回 <xref:System.Collections.Generic.IAsyncEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="17d16-199">It returns an <xref:System.Collections.Generic.IAsyncEnumerable%601>.</span></span>
1. <span data-ttu-id="17d16-200">该方法包含用于在异步流中返回连续元素的 `yield return` 语句。</span><span class="sxs-lookup"><span data-stu-id="17d16-200">The method contains `yield return` statements to return successive elements in the asynchronous stream.</span></span>

<span data-ttu-id="17d16-201">使用异步流需要在枚举流元素时在 `foreach` 关键字前面添加 `await` 关键字。</span><span class="sxs-lookup"><span data-stu-id="17d16-201">Consuming an asynchronous stream requires you to add the `await` keyword before the `foreach` keyword when you enumerate the elements of the stream.</span></span> <span data-ttu-id="17d16-202">添加 `await` 关键字需要枚举异步流的方法，以使用 `async` 修饰符进行声明并返回 `async` 方法允许的类型。</span><span class="sxs-lookup"><span data-stu-id="17d16-202">Adding the `await` keyword requires the method that enumerates the asynchronous stream to be declared with the `async` modifier and to return a type allowed for an `async` method.</span></span> <span data-ttu-id="17d16-203">通常这意味着返回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>。</span><span class="sxs-lookup"><span data-stu-id="17d16-203">Typically that means returning a <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="17d16-204">也可以为 <xref:System.Threading.Tasks.ValueTask> 或 <xref:System.Threading.Tasks.ValueTask%601>。</span><span class="sxs-lookup"><span data-stu-id="17d16-204">It can also be a <xref:System.Threading.Tasks.ValueTask> or <xref:System.Threading.Tasks.ValueTask%601>.</span></span> <span data-ttu-id="17d16-205">方法既可以使用异步流，也可以生成异步流，这意味着它将返回 <xref:System.Collections.Generic.IAsyncEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="17d16-205">A method can both consume and produce an asynchronous stream, which means it would return an <xref:System.Collections.Generic.IAsyncEnumerable%601>.</span></span> <span data-ttu-id="17d16-206">下面的代码生成一个从 1 到 20 的序列，在生成每个数字之间等待 100 毫秒：</span><span class="sxs-lookup"><span data-stu-id="17d16-206">The following code generates a sequence from 1 to 20, waiting 100 ms between generating each number:</span></span>

```csharp
public static async System.Collections.Generic.IAsyncEnumerable<int> GenerateSequence()
{
    for (int i = 0; i < 20; i++)
    {
        await Task.Delay(100);
        yield return i;
    }
}
```

<span data-ttu-id="17d16-207">可以使用 `await foreach` 语句来枚举序列：</span><span class="sxs-lookup"><span data-stu-id="17d16-207">You would enumerate the sequence using the `await foreach` statement:</span></span>

```csharp
await foreach (var number in GenerateSequence())
{
    Console.WriteLine(number);
}
```

<span data-ttu-id="17d16-208">可以在[创建和使用异步流](../tutorials/generate-consume-asynchronous-stream.md)的教程中自行尝试异步流。</span><span class="sxs-lookup"><span data-stu-id="17d16-208">You can try asynchronous streams yourself in our tutorial on [creating and consuming async streams](../tutorials/generate-consume-asynchronous-stream.md).</span></span>

## <a name="indices-and-ranges"></a><span data-ttu-id="17d16-209">索引和范围</span><span class="sxs-lookup"><span data-stu-id="17d16-209">Indices and ranges</span></span>

<span data-ttu-id="17d16-210">范围和索引为在数组中指定子范围（<xref:System.Span%601> 或 <xref:System.ReadOnlySpan%601>）提供了简洁语法。</span><span class="sxs-lookup"><span data-stu-id="17d16-210">Ranges and indices provide a succinct syntax for specifying subranges in an array, <xref:System.Span%601>, or <xref:System.ReadOnlySpan%601>.</span></span>

<span data-ttu-id="17d16-211">可以指定一个倒数索引。</span><span class="sxs-lookup"><span data-stu-id="17d16-211">You can specify an index **from the end**.</span></span> <span data-ttu-id="17d16-212">使用 `^` 运算符指定倒数。</span><span class="sxs-lookup"><span data-stu-id="17d16-212">You specify **from the end** using the `^` operator.</span></span> <span data-ttu-id="17d16-213">你熟悉表示元素“顺数第 2”的 `array[2]`。</span><span class="sxs-lookup"><span data-stu-id="17d16-213">You are familiar with `array[2]` meaning the element "2 from the start".</span></span> <span data-ttu-id="17d16-214">现在，`array[^2]` 意味着元素“倒数第 2”。</span><span class="sxs-lookup"><span data-stu-id="17d16-214">Now, `array[^2]` means the element "2 from the end".</span></span> <span data-ttu-id="17d16-215">索引 `^0` 意味着“结束”或最后一个元素后面的索引。</span><span class="sxs-lookup"><span data-stu-id="17d16-215">The index `^0` means "the end", or the index that follows the last element.</span></span>

<span data-ttu-id="17d16-216">可以使用范围运算符指定范围：`..`。</span><span class="sxs-lookup"><span data-stu-id="17d16-216">You can specify a **range** with the **range operator**: `..`.</span></span> <span data-ttu-id="17d16-217">例如，`0..^0` 指定数组的整个范围：从起始 0 开始，但不包括最后的 0。</span><span class="sxs-lookup"><span data-stu-id="17d16-217">For example, `0..^0` specifies the entire range of the array: 0 from the start up to, but not including 0 from the end.</span></span> <span data-ttu-id="17d16-218">两个操作数都可以使用“顺数”或“倒数”。</span><span class="sxs-lookup"><span data-stu-id="17d16-218">Either operand may use "from the start" or "from the end".</span></span> <span data-ttu-id="17d16-219">此外，可以省略其中一个操作数。</span><span class="sxs-lookup"><span data-stu-id="17d16-219">Furthermore, either operand may be omitted.</span></span> <span data-ttu-id="17d16-220">默认值为起始索引的 `0` 和结束索引的 `^0`。</span><span class="sxs-lookup"><span data-stu-id="17d16-220">The defaults are `0` for the start index, and `^0` for the end index.</span></span>

<span data-ttu-id="17d16-221">请看以下几个示例。</span><span class="sxs-lookup"><span data-stu-id="17d16-221">Let's look at a few examples.</span></span> <span data-ttu-id="17d16-222">请考虑以下数组，用其顺数索引和倒数索引进行注释：</span><span class="sxs-lookup"><span data-stu-id="17d16-222">Consider the following array, annotated with its index from the start and from the end:</span></span>

```csharp
var words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};
```

<span data-ttu-id="17d16-223">每个元素的索引均强化了“顺数”和“倒数”的概念，且范围不包括结束范围。</span><span class="sxs-lookup"><span data-stu-id="17d16-223">The index of each element reinforces the concept of "from the start", and "from the end", and that ranges are exclusive of the end of the range.</span></span> <span data-ttu-id="17d16-224">整个数组的“start”是第一个元素。</span><span class="sxs-lookup"><span data-stu-id="17d16-224">The "start" of the entire array is the first element.</span></span> <span data-ttu-id="17d16-225">整个数组的“end”在最后一个元素之后。</span><span class="sxs-lookup"><span data-stu-id="17d16-225">The "end" of the entire array is *past* the last element.</span></span>

<span data-ttu-id="17d16-226">可以使用 `^1` 索引检索最后一个词：</span><span class="sxs-lookup"><span data-stu-id="17d16-226">You can retrieve the last word with the `^1` index:</span></span>

```csharp
Console.WriteLine($"The last word is {words[^1]}");
// writes "dog"
```

<span data-ttu-id="17d16-227">以下代码创建了一个包含单词“quick”、“brown”和“fox”的子范围。</span><span class="sxs-lookup"><span data-stu-id="17d16-227">The following code creates a subrange with the words "quick", "brown", and "fox".</span></span> <span data-ttu-id="17d16-228">它包括 `words[1]` 到 `words[3]`。</span><span class="sxs-lookup"><span data-stu-id="17d16-228">It includes `words[1]` through `words[3]`.</span></span> <span data-ttu-id="17d16-229">元素 `words[4]` 不在此范围内。</span><span class="sxs-lookup"><span data-stu-id="17d16-229">The element `words[4]` is not in the range.</span></span>

```csharp
var brownFox = words[1..4];
```

<span data-ttu-id="17d16-230">以下代码使用“lazy”和“dog”创建一个子范围。</span><span class="sxs-lookup"><span data-stu-id="17d16-230">The following code creates a subrange with "lazy" and "dog".</span></span> <span data-ttu-id="17d16-231">它包括 `words[^2]` 和 `words[^1]`。</span><span class="sxs-lookup"><span data-stu-id="17d16-231">It includes `words[^2]` and `words[^1]`.</span></span> <span data-ttu-id="17d16-232">不包括结束索引 `words[^0]`：</span><span class="sxs-lookup"><span data-stu-id="17d16-232">The end index `words[^0]` is not included:</span></span>

```csharp
var lazyDog = words[^2..^0];
```

<span data-ttu-id="17d16-233">下面的示例为开始和/或结束创建了开放范围：</span><span class="sxs-lookup"><span data-stu-id="17d16-233">The following examples create ranges that are open ended for the start, end, or both:</span></span>

```csharp
var allWords = words[..]; // contains "The" through "dog".
var firstPhrase = words[..4]; // contains "The" through "fox"
var lastPhrase = words[6..]; // contains "the, "lazy" and "dog"
```

<span data-ttu-id="17d16-234">此外可以将范围声明为变量：</span><span class="sxs-lookup"><span data-stu-id="17d16-234">You can also declare ranges as variables:</span></span>

```csharp
Range phrase = 1..4;
```

<span data-ttu-id="17d16-235">然后可以在 `[` 和 `]` 字符中使用该范围：</span><span class="sxs-lookup"><span data-stu-id="17d16-235">The range can then be used inside the `[` and `]` characters:</span></span>

```csharp
var text = words[phrase];
```