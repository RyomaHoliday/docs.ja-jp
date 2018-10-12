---
title: .NET での I/O エラーの処理
ms.date: 08/27/2018
ms.technology: dotnet-standard
ms.topic: article
helpviewer_keywords:
- I/O, exception handling
- I/O, errors
author: rpetrusha
ms.author: ronpet
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 50dee427913e1ec94a06f1202966bb0f7f5f2099
ms.sourcegitcommit: ad99773e5e45068ce03b99518008397e1299e0d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2018
ms.locfileid: "46696418"
---
# <a name="handling-io-errors-in-net"></a><span data-ttu-id="31f0e-102">.NET での I/O エラーの処理</span><span class="sxs-lookup"><span data-stu-id="31f0e-102">Handling I/O errors in .NET</span></span>

<span data-ttu-id="31f0e-103">任意のメソッド呼び出しでスローできる例外 (システムに負荷がかかっているときの <xref:System.OutOfMemoryException> やプログラム エラーによる <xref:System.NullReferenceException> など) に加え、.NET ファイル システムのメソッドは、次の例外をスローできます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-103">In addition to the exceptions that can be thrown in any method call (such as an <xref:System.OutOfMemoryException> when a system is stressed or an <xref:System.NullReferenceException> due to programmer error), .NET file system methods can throw the following exceptions:</span></span>

- <span data-ttu-id="31f0e-104"><xref:System.IO.IOException?displayProperty=nameWithType>。すべての <xref:System.IO> 例外の種類の基底クラス。</span><span class="sxs-lookup"><span data-stu-id="31f0e-104"><xref:System.IO.IOException?displayProperty=nameWithType>, the base class of all <xref:System.IO> exception types.</span></span> <span data-ttu-id="31f0e-105">これは、オペレーティング システムからのリターン コードが他の例外の種類に直接マップされないエラーに対してスローされます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-105">It is thrown for errors whose return codes from the operating system don't directly map to any other exception type.</span></span>
- <span data-ttu-id="31f0e-106"><xref:System.IO.FileNotFoundException?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="31f0e-106"><xref:System.IO.FileNotFoundException?displayProperty=nameWithType>.</span></span>
- <span data-ttu-id="31f0e-107"><xref:System.IO.DirectoryNotFoundException?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="31f0e-107"><xref:System.IO.DirectoryNotFoundException?displayProperty=nameWithType>.</span></span>
- <span data-ttu-id="31f0e-108"><xref:System.IO.DriveNotFoundException??displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="31f0e-108"><xref:System.IO.DriveNotFoundException??displayProperty=nameWithType>.</span></span>
- <span data-ttu-id="31f0e-109"><xref:System.IO.PathTooLongException?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="31f0e-109"><xref:System.IO.PathTooLongException?displayProperty=nameWithType>.</span></span>
- <span data-ttu-id="31f0e-110"><xref:System.OperationCanceledException?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="31f0e-110"><xref:System.OperationCanceledException?displayProperty=nameWithType>.</span></span>
- <span data-ttu-id="31f0e-111"><xref:System.UnauthorizedAccessException?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="31f0e-111"><xref:System.UnauthorizedAccessException?displayProperty=nameWithType>.</span></span>
- <span data-ttu-id="31f0e-112"><xref:System.ArgumentException?displayProperty=nameWithType>、.NET Framework と .NET Core 2.0 以前のバージョンで、無効なパス文字に対してスローされます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-112"><xref:System.ArgumentException?displayProperty=nameWithType>, which is thrown for invalid path characters on .NET Framework and on .NET Core 2.0 and previous versions.</span></span>
- <span data-ttu-id="31f0e-113"><xref:System.NotSupportedException?displayProperty=nameWithType>、.NET Framework で無効なコロンに対してスローされます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-113"><xref:System.NotSupportedException?displayProperty=nameWithType>, which is thrown for invalid colons in .NET Framework.</span></span>
- <span data-ttu-id="31f0e-114"><xref:System.Security.SecurityException?displayProperty=nameWithType>、.NET Framework で必要な権限が欠けている限定的な信頼で実行されているアプリケーションに対してスローされます </span><span class="sxs-lookup"><span data-stu-id="31f0e-114"><xref:System.Security.SecurityException?displayProperty=nameWithType>, which is thrown for applications running in limited trust that lack the necessary permissions on .NET Framework only.</span></span> <span data-ttu-id="31f0e-115">(完全な信頼は .NET Framework の既定の設定です)。</span><span class="sxs-lookup"><span data-stu-id="31f0e-115">(Full trust is the default on .NET Framework.)</span></span>

## <a name="mapping-error-codes-to-exceptions"></a><span data-ttu-id="31f0e-116">エラー コードの例外へのマッピング</span><span class="sxs-lookup"><span data-stu-id="31f0e-116">Mapping error codes to exceptions</span></span>

<span data-ttu-id="31f0e-117">ファイル システムは、オペレーティング システムのリソースであるため、.NET Core と .NET Framework の両方の I/O メソッドは、基になるオペレーティング システムに呼び出しをラップします。</span><span class="sxs-lookup"><span data-stu-id="31f0e-117">Because the file system is an operating system resource, I/O methods in both .NET Core and .NET Framework wrap calls to the underlying operating system.</span></span> <span data-ttu-id="31f0e-118">オペレーティング システムによって実行されるコードで I/O エラーが発生すると、オペレーティング システムは、.NET の I/O メソッドにエラー情報を返します。</span><span class="sxs-lookup"><span data-stu-id="31f0e-118">When an I/O error occurs in code executed by the operating system, the operating system returns error information to the .NET I/O method.</span></span> <span data-ttu-id="31f0e-119">その後、メソッドがエラー情報を .NET 例外の種類に変換します。通常はエラー コードの形式に変換されます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-119">The method then translates the error information, typically in the form of an error code, into a .NET exception type.</span></span> <span data-ttu-id="31f0e-120">ほとんどの場合、これは、エラー コードを対応する例外の種類に直接変換することによって実行され、メソッド呼び出しのコンテキストに基づく特別なエラーのマッピングは行われません。</span><span class="sxs-lookup"><span data-stu-id="31f0e-120">In most cases, it does this by directly translating the error code into its corresponding exception type; it does not perform any special mapping of the error based on the context of the method call.</span></span>

<span data-ttu-id="31f0e-121">たとえば、Windows オペレーティング システムでは、エラー コード`ERROR_FILE_NOT_FOUND` (または 0x02) を返すメソッドの呼び出しは <xref:System.IO.FileNotFoundException> にマップされ、エラー コード `ERROR_PATH_NOT_FOUND` (または 0x03) は <xref:System.IO.DirectoryNotFoundException> にマップされます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-121">For example, on the Windows operating system, a method call that returns an error code of `ERROR_FILE_NOT_FOUND` (or 0x02) maps to a <xref:System.IO.FileNotFoundException>, and an error code of `ERROR_PATH_NOT_FOUND` (or 0x03) maps to a <xref:System.IO.DirectoryNotFoundException>.</span></span>

<span data-ttu-id="31f0e-122">ただし、オペレーティング システムが特定のエラー コードが返す正確な条件は、多くの場合、文書化されていないか、適切に文書化されていません。</span><span class="sxs-lookup"><span data-stu-id="31f0e-122">However, the precise conditions under which the operating system returns particular error codes is often undocumented or poorly documented.</span></span> <span data-ttu-id="31f0e-123">その結果、予期しない例外が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="31f0e-123">As a result, unexpected exceptions can occur.</span></span> <span data-ttu-id="31f0e-124">たとえば、ファイルではなくディレクトリを操作している場合、無効なディレクトリ パスを <xref:System.IO.DirectoryInfo.%23ctor%2A?displayProperty=nameWithType> に提供すると、<xref:System.IO.DirectoryNotFoundException> コンストラクターがスローされることが想定されます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-124">For example, because you are working with a directory rather than a file, you would expect that providing an invalid directory path to the <xref:System.IO.DirectoryInfo.%23ctor%2A?displayProperty=nameWithType> constructor throws a <xref:System.IO.DirectoryNotFoundException>.</span></span> <span data-ttu-id="31f0e-125">ただし、<xref:System.IO.FileNotFoundException> がスローされる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="31f0e-125">However, it may also throw a <xref:System.IO.FileNotFoundException>.</span></span>

## <a name="exception-handling-in-io-operations"></a><span data-ttu-id="31f0e-126">I/O 操作の例外処理</span><span class="sxs-lookup"><span data-stu-id="31f0e-126">Exception handling in I/O operations</span></span>

<span data-ttu-id="31f0e-127">オペレーティング システムへのこの依存性によって、同じ例外条件 (例に示したディレクトリが見つからないというエラーなど) で、I/O メソッドが I/O 例外クラス全体のいずれかをスルーする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="31f0e-127">Because of this reliance on the operating system, identical exception conditions (such as the directory not found error in our example) can result in an I/O method throwing any one of the entire class of I/O exceptions.</span></span> <span data-ttu-id="31f0e-128">これは、I/O API を呼び出すときは、次の表に示すように、これらの例外のほとんどまたはすべてを処理するようにコードを準備する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="31f0e-128">This means that, when calling I/O APIs, your code should be prepared to handle most or all of these exceptions, as shown in the following table:</span></span>

| <span data-ttu-id="31f0e-129">例外の種類</span><span class="sxs-lookup"><span data-stu-id="31f0e-129">Exception type</span></span> | <span data-ttu-id="31f0e-130">.NET Core</span><span class="sxs-lookup"><span data-stu-id="31f0e-130">.NET Core</span></span> | <span data-ttu-id="31f0e-131">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="31f0e-131">.NET Framework</span></span> |
|---|---|---|
| <xref:System.IO.IOException> | <span data-ttu-id="31f0e-132">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-132">Yes</span></span> | <span data-ttu-id="31f0e-133">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-133">Yes</span></span> |
| <xref:System.IO.FileNotFoundException> | <span data-ttu-id="31f0e-134">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-134">Yes</span></span> | <span data-ttu-id="31f0e-135">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-135">Yes</span></span> |
| <xref:System.IO.DirectoryNotFoundException> | <span data-ttu-id="31f0e-136">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-136">Yes</span></span> | <span data-ttu-id="31f0e-137">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-137">Yes</span></span> |
| <xref:System.IO.DriveNotFoundException?> | <span data-ttu-id="31f0e-138">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-138">Yes</span></span> | <span data-ttu-id="31f0e-139">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-139">Yes</span></span> |
| <xref:System.IO.PathTooLongException> | <span data-ttu-id="31f0e-140">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-140">Yes</span></span> | <span data-ttu-id="31f0e-141">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-141">Yes</span></span> |
| <xref:System.OperationCanceledException> | <span data-ttu-id="31f0e-142">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-142">Yes</span></span> | <span data-ttu-id="31f0e-143">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-143">Yes</span></span> |
| <xref:System.UnauthorizedAccessException> | <span data-ttu-id="31f0e-144">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-144">Yes</span></span> | <span data-ttu-id="31f0e-145">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-145">Yes</span></span> |
| <xref:System.ArgumentException> | <span data-ttu-id="31f0e-146">.NET Core 2.0 以前</span><span class="sxs-lookup"><span data-stu-id="31f0e-146">.NET Core 2.0 and earlier</span></span>| <span data-ttu-id="31f0e-147">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-147">Yes</span></span> |
| <xref:System.NotSupportedException> | <span data-ttu-id="31f0e-148">いいえ</span><span class="sxs-lookup"><span data-stu-id="31f0e-148">No</span></span> | <span data-ttu-id="31f0e-149">はい</span><span class="sxs-lookup"><span data-stu-id="31f0e-149">Yes</span></span> |
| <xref:System.Security.SecurityException> | <span data-ttu-id="31f0e-150">いいえ</span><span class="sxs-lookup"><span data-stu-id="31f0e-150">No</span></span> | <span data-ttu-id="31f0e-151">限定的な信頼のみ</span><span class="sxs-lookup"><span data-stu-id="31f0e-151">Limited trust only</span></span> |

## <a name="handling-ioexception"></a><span data-ttu-id="31f0e-152">IOException の処理</span><span class="sxs-lookup"><span data-stu-id="31f0e-152">Handling IOException</span></span>

<span data-ttu-id="31f0e-153"><xref:System.IO> 名前空間内の例外の基底クラスとして、定義済みの例外の種類にマップされないすべてのエラー コードに対して <xref:System.IO.IOException> もスローされます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-153">As the base class for exceptions in the <xref:System.IO> namespace, <xref:System.IO.IOException> is also thrown for any error code that does not map to a predefined exception type.</span></span> <span data-ttu-id="31f0e-154">つまり、すべての I/O 操作によってスローされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="31f0e-154">This means that it can be thrown by any I/O operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31f0e-155"><xref:System.IO.IOException> は、<xref:System.IO> 名前空間内の他の例外の種類の基底クラスであるため、他の I/O 関連例外を処理した後で `catch` ブロック内で処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31f0e-155">Because <xref:System.IO.IOException> is the base class of the other exception types in the <xref:System.IO> namespace, you should handle in a `catch` block after you've handled the other I/O-related exceptions.</span></span>

<span data-ttu-id="31f0e-156">さらに、.NET Core 2.1 以降、パスの正確性の検証チェック (たとえばパス内に無効な文字が存在しないことを確認するためのチェック) が削除されており、ランタイムでは、独自の検証コードではなく、オペレーティング システムのエラー コードからマップされた例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-156">In addition, starting with .NET Core 2.1, validation checks for path correctness (for example, to ensure that invalid characters are not present in a path) have been removed, and the runtime throws an exception mapped from an operating system error code rather than from its own validation code.</span></span> <span data-ttu-id="31f0e-157">この場合、最もスローされる可能性が高い例外は <xref:System.IO.IOException> ですが、その他の種類の例外もスローされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="31f0e-157">The most likely exception to be thrown in this case is an <xref:System.IO.IOException>, although any other exception type could also be thrown.</span></span>

<span data-ttu-id="31f0e-158">例外処理コードでは、<xref:System.IO.IOException> は常に最後に処理する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="31f0e-158">Note that, in your exception handling code, you should always handle the <xref:System.IO.IOException> last.</span></span> <span data-ttu-id="31f0e-159">それ以外の場合、それは他のすべての IO 例外の基底クラスであるため、派生クラスの catch ブロックは評価されません。</span><span class="sxs-lookup"><span data-stu-id="31f0e-159">Otherwise, because it is the base class of all other IO exceptions, the catch blocks of derived classes will not be evaluated.</span></span>

<span data-ttu-id="31f0e-160"><xref:System.IO.IOException> の場合、[IOException.HResult](xref:System.Exception.HResult) プロパティから追加のエラー情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="31f0e-160">In the case of an <xref:System.IO.IOException>, you can get additional error information from the [IOException.HResult](xref:System.Exception.HResult) property.</span></span> <span data-ttu-id="31f0e-161">HResult 値を Win32 エラー コードに変換するには、32 ビット値の上位 16 ビットを削除します。</span><span class="sxs-lookup"><span data-stu-id="31f0e-161">To convert the HResult value to a Win32 error code, you strip out the upper 16 bits of the 32-bit value.</span></span> <span data-ttu-id="31f0e-162">次の表に、<xref:System.IO.IOException> にラップされる可能性があるエラー コードの一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="31f0e-162">The following table lists error codes that may be wrapped in an <xref:System.IO.IOException>.</span></span>

| <span data-ttu-id="31f0e-163">HResult</span><span class="sxs-lookup"><span data-stu-id="31f0e-163">HResult</span></span> | <span data-ttu-id="31f0e-164">定数</span><span class="sxs-lookup"><span data-stu-id="31f0e-164">Constant</span></span> | <span data-ttu-id="31f0e-165">説明</span><span class="sxs-lookup"><span data-stu-id="31f0e-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31f0e-166">ERROR_SHARING_VIOLATION</span><span class="sxs-lookup"><span data-stu-id="31f0e-166">ERROR_SHARING_VIOLATION</span></span> | <span data-ttu-id="31f0e-167">32</span><span class="sxs-lookup"><span data-stu-id="31f0e-167">32</span></span> | <span data-ttu-id="31f0e-168">ファイル名が存在しないか、ファイルまたはディレクトリが使用中です。</span><span class="sxs-lookup"><span data-stu-id="31f0e-168">The file name is missing, or the file or directory is in use.</span></span> |
| <span data-ttu-id="31f0e-169">ERROR_FILE_EXISTS</span><span class="sxs-lookup"><span data-stu-id="31f0e-169">ERROR_FILE_EXISTS</span></span> | <span data-ttu-id="31f0e-170">80</span><span class="sxs-lookup"><span data-stu-id="31f0e-170">80</span></span> | <span data-ttu-id="31f0e-171">ファイルは既に存在します。</span><span class="sxs-lookup"><span data-stu-id="31f0e-171">The file already exists.</span></span> |
| <span data-ttu-id="31f0e-172">ERROR_INVALID_PARAMETER</span><span class="sxs-lookup"><span data-stu-id="31f0e-172">ERROR_INVALID_PARAMETER</span></span> | <span data-ttu-id="31f0e-173">87</span><span class="sxs-lookup"><span data-stu-id="31f0e-173">87</span></span> | <span data-ttu-id="31f0e-174">メソッドに指定された引数が無効です。</span><span class="sxs-lookup"><span data-stu-id="31f0e-174">An argument supplied to the method is invalid.</span></span> |
| <span data-ttu-id="31f0e-175">ERROR_ALREADY_EXISTS</span><span class="sxs-lookup"><span data-stu-id="31f0e-175">ERROR_ALREADY_EXISTS</span></span> | <span data-ttu-id="31f0e-176">183</span><span class="sxs-lookup"><span data-stu-id="31f0e-176">183</span></span> | <span data-ttu-id="31f0e-177">ファイルまたはディレクトリは既に存在します。</span><span class="sxs-lookup"><span data-stu-id="31f0e-177">The file or directory already exists.</span></span> |

<span data-ttu-id="31f0e-178">catch ステートメントの `When` 句を使用してこれらを処理できます。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="31f0e-178">You can handle these using a `When` clause in a catch statement, as the following example shows.</span></span>

[!code-csharp[io-exception-handling](~/samples/snippets/standard/io/io-exceptions/cs/io-exceptions.cs)]
[!code-vb[io-exception-handling](~/samples/snippets/standard/io/io-exceptions/vb/io-exceptions.vb)]

## <a name="see-also"></a><span data-ttu-id="31f0e-179">関連項目</span><span class="sxs-lookup"><span data-stu-id="31f0e-179">See also</span></span>

- [<span data-ttu-id="31f0e-180">.NET での例外の処理とスロー</span><span class="sxs-lookup"><span data-stu-id="31f0e-180">Handling and throwing exceptions in .NET</span></span>](../exceptions/index.md)
- [<span data-ttu-id="31f0e-181">例外処理 (タスク並列ライブラリ)</span><span class="sxs-lookup"><span data-stu-id="31f0e-181">Exception handling (Task Parallel Library)</span></span>](../parallel-programming/exception-handling-task-parallel-library.md)
- [<span data-ttu-id="31f0e-182">例外のベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="31f0e-182">Best practices for exceptions</span></span>](../exceptions/best-practices-for-exceptions.md)
- [<span data-ttu-id="31f0e-183">catch ブロックで特定の例外を使用する方法</span><span class="sxs-lookup"><span data-stu-id="31f0e-183">How to use specific exceptions in a catch block</span></span>](../exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)