---
title: 解決 (アセンブリ読み込みを)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- assemblies [.NET Framework], resolving loads
- application domains, loading assemblies
- resolving assembly loads
- assemblies [.NET Framework], loading
- application domains, resolving assembly loads
ms.assetid: 5099e549-f4fd-49fb-a290-549edd456c6a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3844f3f1f4135167ac5575dafb4ba63a19b8b55e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927914"
---
# <a name="resolving-assembly-loads"></a>解決 (アセンブリ読み込みを)
.NET Framework では、アセンブリの読み込みをより細かく制御する必要があるアプリケーションのために、<xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> イベントが用意されています。 アプリケーションでこのイベントを処理することにより、通常のプローブ パスの外部から読み込みコンテキストにアセンブリを読み込んだり、アセンブリの複数のバージョンから読み込むものを選んだり、動的アセンブリを生成してそれを返したりすることができます。 ここでは、<xref:System.AppDomain.AssemblyResolve> イベントの処理について説明します。  
  
> [!NOTE]
> リフレクションのみのコンテキストでアセンブリの読み込みを解決する場合は、代わりに <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> イベントを使います。  
  
## <a name="how-the-assemblyresolve-event-works"></a>AssemblyResolve イベントのしくみ  
 <xref:System.AppDomain.AssemblyResolve> イベント用のハンドラーを登録すると、ランタイムが名前によるアセンブリへのバインドに失敗すると、常にハンドラーが呼び出されます。 たとえば、ユーザー コードから次のメソッドを呼び出すと、<xref:System.AppDomain.AssemblyResolve> イベントが発生する可能性があります。  
  
- 1 番目の引数が読み込むアセンブリの表示名を表す文字列 (つまり、<xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> プロパティによって返される文字列) である、<xref:System.AppDomain.Load%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> メソッドのオーバーロード。  
  
- 1 番目の引数が読み込むアセンブリを示す <xref:System.Reflection.AssemblyName> オブジェクトである、<xref:System.AppDomain.Load%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> メソッドのオーバーロード。  
  
- <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> メソッドのオーバーロード。  
  
- 別のアプリケーション ドメインでオブジェクトをインスタンス化する、<xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> メソッドまたは <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> メソッドのオーバーロード。  
  
### <a name="what-the-event-handler-does"></a>イベント ハンドラーでの処理  
 <xref:System.AppDomain.AssemblyResolve> イベントのハンドラーは、読み込まれるアセンブリの表示名を、<xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> プロパティで受け取ります。 ハンドラーは、アセンブリ名を認識できない場合は null を返します (Visual Basic では `Nothing`、C++ では `nullptr`)。  
  
 ハンドラーは、アセンブリ名を認識すると、要求を満たすアセンブリを読み込んで返すことができます。 シナリオの例をいくつか示します。  
  
- ハンドラーは、アセンブリのバージョンの場所がわかっている場合は、<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> メソッドを使ってアセンブリを読み込むことができ、正常に読み込んだ場合はアセンブリを返すことができます。  
  
- ハンドラーは、バイト配列として格納されているアセンブリのデータベースにアクセスできる場合は、<xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> メソッドのバイト配列を受け取るオーバーロードのいずれかを使って、バイト配列を読み込むことができます。  
  
- ハンドラーは、動的アセンブリを生成して返すことができます。  
  
> [!NOTE]
> ハンドラーは、アセンブリを読み込み元コンテキストまたは読み込みコンテキストに読み込むか、コンテキストなしで読み込む必要があります。ハンドラーが <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> メソッドを使ってリフレクションのみのコンテキストにアセンブリを読み込むと、<xref:System.AppDomain.AssemblyResolve> イベントを生成した読み込みの試みは失敗します。  
  
 適切なアセンブリを返すのはイベント ハンドラーの役目です。 ハンドラーは、<xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> プロパティの値を <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> コンストラクターに渡すことによって、要求されたアセンブリの表示名を解析できます。 .NET Framework 4 以降では、ハンドラーは <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> プロパティを使って、現在の要求が別のアセンブリの依存関係であるかどうかを確認できます。 この情報は、依存関係を満たすアセンブリを特定するのに役立ちます。  
  
 イベント ハンドラーは、要求されたバージョンとは異なるバージョンのアセンブリを返すことができます。  
  
 ほとんどの場合、ハンドラーによって返されたアセンブリは、ハンドラーがそれを読み込んだコンテキストに関係なく、読み込みコンテキストで表示されます。 たとえば、ハンドラーが <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> メソッドを使って読み込み元コンテキストにアセンブリを読み込んだ場合でも、ハンドラーによって返されたアセンブリは、読み込みコンテキストに表示されます。 ただし、次の場合は、ハンドラーによって返されたアセンブリはコンテキストなしで表示されます。  
  
- ハンドラーがコンテキストなしでアセンブリを読み込んだ場合。  
  
- <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> プロパティが null ではない場合。  
  
- 要求元のアセンブリ (つまり、<xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> プロパティによって返されるアセンブリ) がコンテキストなしで読み込まれた場合。  
  
 コンテキストについて詳しくは、<xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> メソッドのオーバーロードをご覧ください。  
  
 同じアセンブリの複数のバージョンを、同じアプリケーション ドメインに読み込むことができます。 ただし、型の割り当ての問題が発生する可能性があるため、この方法は推奨されません。 「[アセンブリの読み込みのベスト プラクティス](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)」をご覧ください。  
  
### <a name="what-the-event-handler-should-not-do"></a>イベント ハンドラーで行ってはいけないこと  
 <xref:System.AppDomain.AssemblyResolve> イベントの処理に関する基本原則は、認識できないアセンブリを返そうとしてはならない、ということです。 ハンドラーを記述するときは、イベントを発生させる可能性があるアセンブリを知っておく必要があります。 それ以外のアセンブリに対して、ハンドラーは null を返す必要があります。  
  
> [!IMPORTANT]
> .NET Framework 4 以降では、<xref:System.AppDomain.AssemblyResolve> イベントはサテライト アセンブリに対して発生します。 以前のバージョンの .NET Framework で作成されたイベント ハンドラーが、すべてのアセンブリ読み込み要求を解決しようとしている場合、この変更によって影響を受けます。 認識しないアセンブリを無視するイベント ハンドラーはこの変更の影響を受けません。null を返し、通常のフォールバック メカニズムがそれに続きます。  
  
 アセンブリを読み込むとき、イベント ハンドラーは、<xref:System.AppDomain.AssemblyResolve> イベントを再帰的に生成する可能性がある <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> メソッドまたは <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> メソッドのオーバー ロードを、使わないようにする必要があります。使った場合、スタック オーバーフローが発生することがあります (このトピックで先に示したリストを参照)。すべてのイベント ハンドラーから返るまで例外はスローされないため、読み込み要求に対して例外処理を提供した場合でも、この問題は発生します。 したがって、次のようなコードでは、`MyAssembly` が見つからないとスタック オーバーフローが発生します。  
  
 [!code-cpp[AssemblyResolveRecursive#1](../../../samples/snippets/cpp/VS_Snippets_CLR/assemblyresolverecursive/cpp/example.cpp#1)]
 [!code-csharp[AssemblyResolveRecursive#1](../../../samples/snippets/csharp/VS_Snippets_CLR/assemblyresolverecursive/cs/example.cs#1)]
 [!code-vb[AssemblyResolveRecursive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/assemblyresolverecursive/vb/example.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [アセンブリの読み込みのベスト プラクティス](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)
- [アプリケーション ドメインの使用](../../../docs/framework/app-domains/use.md)
