---
title: "ChatGPT常用提示词😊"
date: 2023-07-28
description: "本文介绍使用ChatGPT等AI聊天机器人时一些常用的提示词."
tags: ["AI", "ChatGPT", "Prompt"]
type: post
---

# 翻译文本
> Translate the following to xxx. 

## 输入
`Translate the following to Chinese.`

1. How likely are you to recommend our product to others? 
2. What is your favorite feature of our product?

## 输出

1. 你有多大可能会向他人推荐我们的产品？
2. 你最喜欢我们产品的哪个特点？


# 从文本中提取实体
> Extract xxx from the text below.

## 输入

`Extract the person name, company name, location and phone number from the text below.`

Hello. My name is Robert Smith. I’m calling from Contoso Insurance, Delaware. My colleague mentioned that you are interested in learning about our comprehensive benefits policy. Could you give me a call back at (555) 346-9322 when you get a chance so we can go over the benefits? Thank you.

## 输出
Person name: Robert Smith

Company name: Contoso Insurance

Location: Delaware

Phone number: (555) 346-9322

# 写电子邮件

## 输入
`Write a product launch email for new AI-powered headphones that are priced at $79.99 and available at Best Buy, Target and Amazon.com. The target audience is tech-savvy music lovers and the tone is friendly and exciting and the language is chinese.`

## 输出
亲爱的音乐爱好者们，

我们很高兴向您宣布，我们的全新智能耳机已经上市了！这款耳机不仅外观时尚，而且还搭载了最新的人工智能技术，让您可以在享受音乐的同时获得更多的智能体验。

这款智能耳机的售价为 $79.99，您可以在Best Buy，Target和Amazon.com购买到。我们相信，这款耳机不仅会成为您的音乐伴侣，更会成为您生活中必不可少的智能设备。

我们的智能耳机配备了先进的语音识别技术，您可以通过语音指令控制播放音乐、接听电话等功能，让您的生活更加便捷。此外，我们的耳机还配备了高质量的音响系统，让您可以享受更加震撼的音乐体验。

我们的目标受众是技术精通的音乐爱好者，我们相信您会喜欢这款智能耳机。如果您对这款耳机有任何问题或建议，请与我们联系。谢谢！

祝好，

您的团队

# 问题推理
## 输入
Q: Contoso made a sale for 50. The raw materials cost 10 and the labor was 20. What was the profit on the sale?

## 输出
The profit on the sale was 20.

## 输入
Q:Fabrikam sold 100 widgets for $10 each. However, 30 of the widgets were returned for a full refund. How much money did Fabrikam make?

## 输出
A: Fabrikam made $700 from the sale of 70 widgets after deducting the cost of the returned widgets.

# 对意向进行分类和检测
## 输入
For the below text, provide two labels one each from the following categories:

- Department: “Books”, “Home”, “Fashion”, “Electronics”, “Grocery”, “Others”

- Order intent


Subject: Request for Refund of Recent Book Purchase

Dear [Business Name],

I am writing to request a refund for the books I purchased from your store last week. Unfortunately, the books did not meet my expectations, and I would like to return them for a full refund.

I have attached a copy of the purchase receipt to this email as proof of purchase. The books are in their original packaging and have not been used, so I hope that the refund process will be straightforward.

Please let me know what steps I need to take to return the books and receive a refund. I look forward to hearing back from you soon.

Thank you for your attention to this matter.

Sincerely,

[Your Name]

## 输出
Department: Books

Order intent: Refund
