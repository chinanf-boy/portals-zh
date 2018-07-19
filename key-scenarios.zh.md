
# 关键方案

这是我们希望门户网站有助于解决的方案列表. 它包括未涵盖的所需隐私行为[v0解释者](explainer.md). 

## 来自不同网站的文章的旋转木马

新闻聚合器希望为其用户提供快速浏览来自涵盖相同新闻故事的各种出版物的文章的能力. 

典型的用户体验包括: 

-   视口顶部的导航UI,用于传达文章序列中的位置. 当用户向下滚动或备份时,可能会消失并重新出现. 
-   占据视口其余部分并允许垂直滚动的文章
-   左/右滑动手势可在上一篇/下一篇文章之间导航. 

要求: 

-   更新UA的地址栏以反映用户导航到的文章的URL. 
-   下一篇/前一篇文章之间的导航无缝地发生. 
-   导航UI与用户在文章序列中的位置保持同步. 
-   发布商只有在用户从该发布商处滑动文章时才能了解用户. 
-   当滑动手势完成时,新闻聚合器想要通过显示适当的URL来向用户传达他们正在从特定发布者读取内容,从而保持用户对其隐私的期望. 

激活后,新闻聚合器打开的门户现在将接收输入事件. 这意味着它必须与新闻聚合器合作才能保持所需的用户体验. 例如,这是如何工作的: 

-   新闻聚合器成为激活文章的门户. 
-   激活的文章将包括一个提供的脚本,让新闻聚合器检测任何滑动手势并与其门户进行通信. 


    <TODO sample code demonstrating how the API can be used to solve the use case>

publisher.com/articles/2018/05/monthly-trends ...

    [...]
    // tentative approach
    window.addEventListener('portalactivate', e => {
      let predecessor = e.adoptPredecessor(document);
      console.assert(predecessor instanceof HTMLPortalElement);
      // by special dispensation, this element keeps the portal alive for the duration of the portalactivate event
      // past that, the author must attach it to the document
      
      // maintain the user's expectations vis-a-vis the news aggregator flow
      // by keeping the news aggregator's UI around in the form of a portal 
      document.getElementById("extUI").appendChild(predecessor);
      
      // add script to forward swipe gestures to the news aggregator (portal)
      [...]
    });

## 出版物中包含无限的文章列表

网络出版物希望提供无限的文章列表,但无需重新设计其网站,该网站被构建为多页面应用程序. 所需的用户体验如下: 

-   当用户到达文章的末尾时,他们会看到相关文章的预览. 
-   如果它们进一步滚动,则会显示完整的文章并更新地址栏,因为它们现在已移至新文档. 向后滚动将导致返回先前的状态. 

要求: 

-   网络出版物希望避免对其网站进行复杂的更改. 他们希望通过使用第三方服务来实现此UX,即复制粘贴预先配置的代码段. 


    <TODO sample code demonstrating how the API can be used to solve the use case>

### 在评论网站上插入产品页面

网络出版物希望能够更容易地购买它所评论的产品. 

Web出版物希望实现以下UX: 

-   在产品评论结束时,插图显示来自信誉良好的电子商务网站的相关产品页面的预览,
-   当用户尝试与产品页面进行交互时,通过展开插入来执行无缝导航,直到它接管整个视口,然后导航到产品页面. 

要求: 

-   保护读者的隐私. 如果电子商务网站决定与产品页面插图进行交互,则该电子商务网站应该只知道读者对该产品感兴趣. 
-   从插入状态到导航状态的无缝转换. 
-   通过在地址栏中显示正确的URL,允许读者在转换结束后了解/确认他们是在信誉良好的电子商务网站上. 


    <TODO sample code demonstrating how the API can be used to solve the use case>

## 同源无缝导航

多页面应用程序希望实现与单页面应用程序的导航相当的导航. 

    <TODO sample code demonstrating how the API can be used to solve the use case>
