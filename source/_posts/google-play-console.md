---
title: "2022 年 Google 开发者账号注册避坑指南"
date: 2022-04-10 21:22:00
categories: "教程"
tags: [Android, Google, Developer]
cover: "https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/0.png"
toc: true
excerpt: "分享本人注册谷歌开发者账号期间有关填表，缴费，申诉等方面的经验。"
---
每一名开发者都希望自己的作品能被更多人使用与认可，上架应用商店就是其中一种最直接的方式。但国内乌烟瘴气的软件生态与繁杂的审核机制时常劝退我们这些独立开发者。作为一名“根正苗红”的 Android 开发者，Google Play 商店自然成为最为“正统”的选择。

请注意，本篇文章特别针对的时间是 **2022年**，因为谷歌在2021年曾对政策进行了较大的改动，很多文章都没有对这些改动作出更新。（这着实让我吃了很大的苦头，不止有精神层面，更有经济层面）

与 iOS 开发者账号所需的 99USD 年费相比，Android 的注册可就亲民太多了，仅需一次性支付 25USD 的费用，后续无论是发布应用还是获取收益都无需再支付任何费用。但由于谷歌仅支持 Visa，Master 等信用卡支付方式，支付这笔费用也就成为国内开发者们最大的门槛。
>如果你还没有合适的支付方式，推荐办理一张中国银行的跨境通借记卡。具体操作可以参阅这篇博客 [poplite's blog 跨境通VISA/万事达借记卡介绍与网上支付体验](https://poplite.xyz/post/2018/03/05/boc-debit-card-guide-for-online-payment.html)。

![成功注册示例](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/14.png)

### 建立付款资料（重要）

登录 [Google Pay](https://pay.google.com/)，建立付款资料，确定国家/地区选项为**中国（CN）**。然后添加支付方式。如果先前已设置好非中国地区的付款资料，你需要再重新创建一个。请放心，这不会对你旧有的付款资料产生任何影响。创建好之后，在 `用于 Google Pay 的付款资料` 中选择正确的资料。

![更改国家/地区](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/1.png)

![选择正确的付款资料](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/2.png)

**重要！** 根据谷歌的政策，你创建的开发者账户所属国家/地区将与付款资料中的信息绑定，且不允许再修改。因此，如果你支付注册费用时选择了错误的付款资料，你的开发者账户就无法使用了，这笔费用原则上也无法退还（至少也需要与客服一番艰苦辩论才能退还）。当然，在与客服的交涉中我也拿到了请求退款的[表单填写入口](https://support.google.com/googleplay/android-developer/contact/idv_form?hl=en)，有需要可以前往，使用英语填写。

或许有同学动起了他的小脑筋：那索性就用非中国地区的账号呗，反正也不影响我发布应用，说不定收款时还能更方便呢？

**错啦！** 根据谷歌在去年的政策更新，每一个开发者账户都需要提交能够证明 **当地** 身份信息的资料才能发布应用。也就是说，如果你错误选择了区域，无法通过身份验证，你**不仅不能发布应用，甚至不能切换地区，也不能删除账号**！也就是说，你必须重新创建一个谷歌账号，再支付一笔费用，来将新的开发者账号与你的新谷歌账号绑定。接下来我会再详细说说这种情况。

### 付款并创建账户

准备好这一切，你就可以前往 [Play Console](https://play.google.com/console/signup) 创建账户了。

接下来会要求你填写一个表单。其中的大部分信息日后都可以修改，所以不必过于在意。电话验证可以填写 +86 的手机号。

之后就到了关键的支付阶段了。必须确认选择了正确的付款资料。如果不太确定，你也可以在支付时点击右上角的`x`，会弹出选项供你更改资料，再选择一下就OK。

![支付前选择付款资料](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/3.png)

支付时先确认下卡里的余额。有的卡会要求收取实际102%左右的款项，多出的部分用于验证。个人建议卡里至少留有 26 美元，避免各种原因导致扣款失败。

### 账号验证

截止文章发布，中国（CN）区域的账号尚无需身份验证，可以直接使用。而如果你选择了其他常用区（如美国），根据政策，系统会提示您进行身份验证。

以美国为例，身份验证需要提供以下证明之一：

- 驾照
- 州身份证明
- 美国护照
- 绿卡

蒙混过关是不存在的，一切审核都由人工进行。并且每个账号的验证次数是有限的，如果验证次数被耗尽，账号还会被直接停用。

![身份验证要求](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/4.png)

### 如果支付失败

如果账号创建成功，恭喜你，你可以略过这部分的内容；而如果你不幸遭遇各种原因导致的支付失败，下面的小提示或许会十分有用。

你可能会收到一封来自 Google Payments 的邮件，提示《您的订单已暂停处理》。访问 [Google Pay](https://pay.google.com/) 页面，你会发现多出 `需要采取措施` 的项目，提示您 `修正付款方式` ，就像下图展示的一样。

![修正付款方式](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/5.png)

关键提醒！如果已经往卡内转账补足了款项，并试图重新支付继续注册流程，那么你来错地方了！你应该做的是重新前往 [Play Console](https://play.google.com/console/signup)，重头走一次注册流程。如果你听信了谷歌的蛊惑，点击了那罪恶的 `修正付款方式` 按钮，款项成功扣除，订单消失，注册流程中断，25$ 顷刻间石沉大海。

这个漏洞似乎来自系统缺陷，且长期未被修复；客服的权限也很有限，对于这个问题也无能为力。一代又一代可悲的独立开发者们，前仆后继地往同一个坑中跳（当然也包括我）；早在 19 年，外国友人已在论坛上发起[讨论](https://support.google.com/googleplay/thread/17196697?hl=en)，但最终也是不了了之。如果有兴趣旁观我与客服的聊天记录，可以接着向下看。

![部分论坛文章截图](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/15.png)

### 彩蛋
以下是我尝试更换地区时与客服的邮件交流记录。

![退款](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/6.png)

![退款](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/7.png)

以下是我与 Google Play Console 客服的对话记录。（英语拙劣，见谅）

![对话记录](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/8.png)

![对话记录](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/9.png)

![对话记录](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/10.png)

以下是我与 Google Pay India 客服的对话记录。

![对话记录](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/11.png)

![对话记录](https://ojhdt-1257115336.cos.ap-guangzhou.myqcloud.com/img/20220410/13.png)