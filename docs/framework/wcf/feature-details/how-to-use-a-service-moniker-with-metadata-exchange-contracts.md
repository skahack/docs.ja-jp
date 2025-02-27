---
title: '方法: Metadata Exchange コントラクトと共にサービス モニカーを使用する'
ms.date: 03/30/2017
ms.assetid: c41a07e5-cb9d-45d6-9ea4-34511e227faf
ms.openlocfilehash: 00aa1bbde95c0636391f213f830fc67b2dedf459
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968791"
---
# <a name="how-to-use-a-service-moniker-with-metadata-exchange-contracts"></a>方法: Metadata Exchange コントラクトと共にサービス モニカーを使用する
新しい WCF サービスを開発した後、これらのサービスをスクリプトまたは Visual Basic 6.0 アプリケーションから呼び出すことができるようにすることができます。 1つの方法として、WCF クライアントアセンブリを生成し、アセンブリを COM に登録し、アセンブリを GAC にインストールしてから、Visual Basic コードから COM 型を参照する方法があります。 アプリケーションを配布する場合は、WCF クライアントアセンブリも配布する必要があります。 次にユーザーは COM を使用して WCF クライアント アセンブリを登録し、それを GAC に配置する必要があります。 WCF COM 相互運用機能を使用すると、WCF クライアントアセンブリに依存することなく、同じサービス呼び出しを行うこともできます。 WCF モニカーを使用すると、サービスモニカーが型を抽出するために使用する metadata exchange (Mex) エンドポイント URI を指定することで、任意の COM 互換言語 (Visual Basic、VBScript、Visual Basic for Applications (VBA) など) から任意の WCF サービスを呼び出すことができます。サービスに関する情報。 このトピックでは、Mex エンドポイントを指定する WCF モニカーを使用してはじめに WCF サンプルを呼び出す方法について説明します。  
  
> [!NOTE]
> WCF クライアントアセンブリによって定義された型は、実際にはインスタンス化されません。 アセンブリはメタデータにのみ使用されます。  
  
### <a name="using-the-service-moniker-with-a-mex-address"></a>Mex アドレスを使うサービス モニカーの使用  
  
1. はじめにサンプルをビルドし、Internet Explorer を使用してその URL http://localhost/ServiceModelSamples/Service.svc) を参照します (サービスが動作していることを確認します)。  
  
2. Visual Basic スクリプトまたは Visual Basic アプリケーションを作成し、次のコードを記述します。  
  
    ```  
    monString = "service:mexaddress=http://localhost/ServiceModelSamples/Service.svc/MEX"  
    monString = monString + ", address=http://localhost/ServiceModelSamples/Service.svc"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
    Set calc = GetObject(monString)  
    MsgBox calc.Add(3, 4)  
    ```  
  
3. 作成した Visual Basic アプリケーションまたはスクリプトを実行します。  
  
    > [!NOTE]
    > モニカーがサービスのメタデータを読み取るには、呼び出すサービスで、Mex エンドポイントが公開されている必要があります。 詳細については、「[方法 :構成ファイル](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)を使用して、サービスのメタデータを公開します。  
  
    > [!NOTE]
    > モニカーの形式が正しくないか、`GetObject` を呼び出せない場合は、"構文が無効です" というメッセージが返されます。  このエラーが発生した場合は、使用しているモニカーが正しく、サービスが使用可能であることを確認してください。  
  
## <a name="see-also"></a>関連項目

- [方法: 登録せずに Windows Communication Foundation サービスモニカーを使用する](../../../../docs/framework/wcf/feature-details/use-the-wcf-service-moniker-without-registration.md)
- [方法: WSDL コントラクトでのサービスモニカーの使用](../../../../docs/framework/wcf/feature-details/how-to-use-a-service-moniker-with-wsdl-contracts.md)
