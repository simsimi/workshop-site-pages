<style
  type="text/css">
style {color:#ffffff;display:hidden}
h1, h2, h3, h4, h5, h6 {color:#333333;}
p, li {color:#333333}
code {color:#000080;}
</style>

# FAQ
Here's a closer look at the SimSimi Workshop Service. This contents will be updated continuously and if you have any questions, please feel free to contact SWS team(api@simsimi.com)!

---

### What is small talk?
Small talks are idle talks, chitchats, jokes and etc that people take in without setting a specific topic.

---

### Does chatbot need small talks?
Many of the conversations people share are casual talk. People tend to think of chatbots as people, so they try to casual conversations with chatbots, but all the current generation chatbots are not very good at it, so people feel very different from them and then only give them some limited work orders. If your chatbot is a little better at small talk, users will feel friendly to it.

---

### Who uses the Smalltalk API?
Approximately 30,000 developers (companies or individuals) have used or are using the Smalltalk API, including the previous generation API (SimSimi Conversation API). Some of them are big companies like Baidu, Sanrio, and some are anonymous developers who use millions of requests steadily.

---

### Can I write small talks for my chatbot myself?
It's a great challenge, but it's hard to come by now. You can tell from the level of casual talks of chatbots from global corporations. Although small talk is not difficult for people, it is a consensus of many researchers that it can not be overcome by the current generation of computers and software. That's why it's hard to find an alternative to SWS's Smalltalk API when you need small talk in your chatbot.

---

### What features and benefits does SWS Smalltalk API have?
SWS's Smalltalk API allows chatbots to have friendly conversations with people based on a large amount of live expressions and a carefully tuned conversation processing engine that have been accumulated over more than 15 years with the chichatting chatbot 'SimSimi'.

---

### How are the sentences provided by the Smalltalk API created?
Sentences submitted by some of the SimSimi users using the 'Teach' function. SimSimi is a small talk dedicated chatbot, with hundreds of millions of users around the world having conversations with it. Of these, tens of millions of anonymous users voluntarily submitted their own inspirational sentences.

---

### Does the Smalltalk API provide all of the sentences that the SimSimi service has accumulated?
Basically yes. Unlike the SimSimi chatbot service, which excludes sentences that have a certain level of bad word probability according to the content policy, the Smalltalk API does not have this restriction. You can control the bad word probability of sentences from the Smalltalk API to your service. There are a few exceptions, for example, sentences with the risk of personal information leakage may be excluded.

---

### How do I control the bad word probability level of sentences provided by the Smalltalk API?
Set the atext_bad_prob_max parameter when requesting an API. The Smalltalk API returns sentences with a bad word probability of 0% in the answer text(atext) if this value is 0.0, and sentences with a bad word probability of 70% or less if this value is 0.7.

[Details and example](https://workshop.simsimi.com/document#st_filter)

---

### What is the principle of determining whether a particular sentence is a bad word?
Based on the content policy of the SimSimi service. A Badword probability is used to represent the probability that a sentence might violate this policy by several techniques.

[SimSimi Content Policy](http://blog.simsimi.com/2017/04/simsimi-terms-and-conditions.html)

---

### Please let me know the content policy of the SimSimi service.
The SimSimi service prohibits the following content.

- Content that depicts explicit sex acts.
- Content that depicts or encourages excessive violence or other dangerous conduct.
- Content that includes or encourages threats, harassment, or bullying.
- Content that includes or encourages sexual abuse of children.
- Content that promotes hatred of a particular group based on race, ethnicity, color, national origin, religion, age, sex, sexual orientation, gender identity, family status, disability, medical or genetic condition.
- Content that is improperly depicted in a natural disaster, cruel act, physical conflict, death, or other tragedy.
- Content promoting illegal activities.

You can see the Terms of Service at the link below.

[SimSimi Terms and Conditions](https://workshop.simsimi.com/policy/terms)

---

### How does bad word probability determine?
The probability of bad word of the sentences provided by the Smalltalk API is determined by combining the following classification methods also utilized by the SimSimi service. You can find descriptions of each classification techniques in the links below.

[Malcious Sentence Classification Techniques in the SimSimi Service (written in Korean)](http://blog.simsimi.com/2019/03/blog-post.html)

1) Stochastic approximation (STAPX)
2) Deep neural network discrimination (DPD)
3) Word and phrase filter (WPF)
4) Crowdsourced classification (HB10)

---

### Is the bad word probability of the Smalltalk API reliable?
Although the bad word probability decision technique used by the Smalltalk API is achieving unprecedented high performance worldwide, it is still not perfect. If your main chatbot customer is a sensitive group, do not use the sentences provided by the Smalltalk API as it is, but get additional safeguards.

---

### I want to pay in advance.
You can only pay prepaid by wire transfer. Please send the following information to api@simsimi.com, we will send you an invoice and account information to deposit.

1. Email address associated with your account:
2. Name of your project to use API:
3. Volume of APIs you want to purchase:
4. Email address to be invoiced:

---

### How is pricing structured for the API.
For each successful request, there is a per-request cost, which varies depending on whether it has filtering options. For more information, see the Pricing page.

[Pricing](https://workshop.simsimi.com/pricing#pricing_policy)

---

### I need only one language out of the many languages that you support. Can I get a discount?
No. The charges are the same regardless of the range of languages you use.

---

### I cannot sign up for a new account.
In China, you can not sign up because of an issue known as "The Great Firewall of China". If you have problems outside of China, please contact us at api@simsimi.com

---

### Can I try APIs before deciding to purchase?
Yes. We provide new users with a demonstration project which is capable of 100 requests.

---

### Do I need a credit card to use the service?
Yes. We certify that you are a valid user, not a robot, with your credit card authorization.

---

### How many projects can I create?
You are allowed 5 projects. The restriction may be mitigated by the SWS team's judgment. Please contact us at api@simsimi.com.

---

### What languages does Simsimi Workshop support?
Consult the Supported Language List for the latest coverage information.

[Supported Language List](https://workshop.simsimi.com/document#st_lang_code)

---

### Why are there limits to how many projects I can create?
Quotas protect SimSimi Workshop from unforeseen spikes in usage. However, as your usage of SimSimi Workshop increases, you can request an increase in your quota. When SimSimi Workshop allocates resources to customers, we consider a variety of factors, including resources that most legitimate customers use, customer’s previous usage and history, and previous abuse penalties. Customers might have different quota based on these and other factors.

---

### How do I request more projects?
If you attempt to exceed your project limit, the console will prompt you to fill out a request form. This happens when you try to create a project but you have already reached your quota. The form will require you to specify the number of additional projects you need, along with their corresponding email accounts, and intended uses.

