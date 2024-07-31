<style
  type="text/css">
style {color:#ffffff;display:hidden}
h1, h2, h3, h4, h5, h6 {color:#333333;}
p, li {color:#333333}
code {color:#000080;}
</style>

# SmallTalk API
SimSimi Workshop Services (SWS) provides a service based on 'SimSimi', a small talk chatbot that has enjoyed over 400 million users around the world. SimSimi's steadfast success lies in its more than 150 million lively, dedicated-to-use scenarios written by twenty-two million panelists from diverse backgrounds around the world. The SmallTalk API leverages these scenarios and the conversation engine AICR to help your chatbot provide laughter and healing to users.


## Concept
A ‘talkset’ consists of a pair of question-answer sentences(`qtext`-`atext`). SWS has more than 100 million scenarios repository.

<img src="https://workshop.simsimi.com/images/smalltalk_diagram_01e.png" width="300px" alt="SmallTalk API talkset concept diagram">

When a request is received through the SmallTalk API, SWS’s conversation engine(AICR) finds the relevant question sentences(`qtext`) in the talkset repository considering the similarities with a user’s request sentence(`utext`) and some other factors, creates a candidate talksets, and selects the most appropriate talkset filtering/weighing the parameters included in the request and other conditions.

The answer sentence provided by the SmallTalk API is the atext of the talkset selected through this process. If a requested utext is “Have you eaten lunch?”, the SmallTalk API returns an atext through the process like below.

<img src="https://workshop.simsimi.com/images/smalltalk_diagram_02e.png" width="600px" alt="SmallTalk API flow diagram">


## Basic Request
You can receive a response by requesting to the SmallTalk API endpoint(`https://wsapi.simsimi.com/{VERSION}/talk`) with the appropriate method(POST), project key, and required parameters(`utext`, `lang`).

#### Example Request
``` bash
curl -X POST https://wsapi.simsimi.com/190410/talk \
     -H "Content-Type: application/json" \
     -H "x-api-key: PASTE_YOUR_PROJECT_KEY_HERE" \
     -d '{
            "utext": "hello", 
            "lang": "en" 
     }'                     
```
- `utext` : Sentence that a user entered in your chatbot(100 characters max.)
- `lang` : Language code ( [language-language code table](#SmallTalk-Supported-Languages) )

#### Example Response
``` json
{
  "status":200,
  "statusMessage":"Ok",
  "atext":"Hello it is a pleasure to meet you!",
  "lang":"en",
  "request":{
    "utext":"hello",
    "lang":"en"
    }
}    
```
- `atext` : answer sentence 
- `request` : request body
- `status`, `statusMessage` : status information ([Status Code List](#SmallTalk-Status-Code))

## Response Control
SmallTalk API provides options for controlling response. For example, if you want your bot to answer sentences(`atext`) with a [Badword Probability](#badword-probability) of 70% or less among the talksets generated in the United States, you can request by adding the following two options.

#### Example Request
``` bash
curl -X POST https://wsapi.simsimi.com/190410/talk \
     -H "Content-Type: application/json" \
     -H "x-api-key: PASTE_YOUR_PROJECT_KEY_HERE" \
     -d '{
            "utext":"hello",
            "lang": "en",
            "country" : ["US"],
            "atext_bad_prob_max": 0.7
     }'  
 ```
#### Response Control Options

- `country` : Specifies the countries of the talkset. You can specify this value when you are requesting SmallTalk API with a language that is used in multiple countries to filter the talksets created in the desired countries. The format is an array of [country codes](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements) (up to 10, if not specified, all countries are set.).

- `atext_bad_prob_max`, `qtext_bad_prob_max`, `talkset_bad_prob_max` : Limit the maximum of Badword Probability in the sentence (`atext`, `qtext`, `talkset`). In many cases, it is sufficient to adjust the value of the answer(`atext`), and you can also specify the value of the question(`qtext`) or `talkset` for more conservative operation. Badword Probability of a talkset combines question and answer(`qtext` + `atext`) into a single sentence. Specifies one of the values from 0.0 to 1.0 with the first decimal place. Defaults to 0.0.
　
- `atext_bad_prob_min` : Sets the minimum of Badword Probability . Setting this value to a high number will exclude sentences with low Badword Probability. You can use it to make your chatbot speak bad words. Please note that many chatbot platforms have limitations related to the health of the content. Specifies one of the values from 0.0 to 1.0 with the first decimal place. Defaults to 0.0.
　
- `atext_length_max`, `atext_length_min` : Specify the length range of the answer sentence(`atext`). You can control it depending on the chatbot's personality and the context of the conversation. (Integer from 1 to 256; default if not specified: `atext_length_max` is 256,` atext_length_min` is 1)
　
- `regist_date_max`, `regist_date_min` : Specify the range of the talkset registration date. You can use it to implement chatbots that are sensitive to the latest trends or chatbots that have stayed in the past.(Use in the foramt `yyyy-MM-dd HH:mm:ss`, default if not specified: `regist_date_max` is now, `regist_date_min` is date of the first talkset registration)　　

- `Deprecated` ~~`ko_polite_converter` : Convert Korean response into polite word. This is only usable when `lang` is `ko`. (`true|false`, default if not specified: `false`)~~

- `suppress_ko_person_name` : Control the exposure of a Korean person's name in response. This is only usable when `lang` is `ko`. (`R`: Filters out most common names)
　  
   
#### Utilize Teach API

- `teach_api_key` : Enter the API key of the Teach API project you want to utilize, and then taught talksets will be answered first. If there is no talksets related to the utext, you will get the same result as you didn't include `teach_api_key` parameter. If the taught talkset is answered, it does not work with other response control and additional information parameters.

- `teach_key` : Only talksets correspond to the teach_key you entered when you used Teach API can be answered. If you want answers regardless of the teach_key, you don't have to include the parameter. If none of the talksets correspond to the teach_key entered, you will get the same result as you didn't include `teach_api_key` parameter.


## Request Additional Information 
The SmallTalk API provides a way to get more detailed information about responses. Define `cf_info` in the request body for the additional information you want to receive.
#### Example Request
``` bash
curl -X POST https://wsapi.simsimi.com/190410/talk \
     -H "Content-Type: application/json" \
     -H "x-api-key: PASTE_YOUR_PROJECT_KEY_HERE" \
     -d '{
            "utext":"hello",
            "lang": "en",
            "cf_info" : [
                  "qtext",
                  "country",
                  "atext_bad_prob",
                  "atext_bad_type",
                  "regist_date"
            ],
     }'         
```
#### Example Response
``` json
{
    "status" : 200,
    "statusMessage" : "OK",
    "atext" : "Hello it is a pleasure to meet you!",
    "lang" : "en",
    "utext" : "hello",
    "qtext" : "hello~~",
    "country" : "US",
    "atext_bad_prob" : 0.0,
    "atext_bad_type" : "dpd",
    "regist_date" : "2017-07-08 08:24:37"
}                           
  
```
#### Additional Information Details
- `qtext` : The question sentence(`qtext`) that is a pair of the answer sentence(`atext`) in the talkset.
- `country` : ISO-3166-1 alpha-2 country code for the talkset. ([See the country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements))
- `atext_bad_prob` : The Badword Probability of the answer sentence(`atext`).
- `atext_bad_type` : The distinguishing technique used to estimate Badword Probability for the answer sentence(`atext`). It is one of `STAPX`, `DPD`, `WPF` and `HB10A` (See the [Badword Classification Techniques (Korean)](http://blog.simsimi.com/2019/03/blog-post.html) )
- `regist_date` : The creation time of the talkset.


## SmallTalk Supported Languages
Most language codes are the same as ISO-639-1, but note that there are other cases(*).

|Language Name		|	 Name	|	 Language Code|
| --- | --- | --- |
|Afrikaans	 |Afrikaans	 |af|
|Albanian	 |Shqip	 |al*|
|Arabic	 |العربية	 |ar|
|Armenian	 |հայերեն	 |hy|
|Azerbaijani	 |Azərbaycanca	 |az|
|Basque	 |Euskara	 |eu|
|Belarusian	 |беларуская	 |be|
|Bengali	 |বাংলা	 |bn|
|Bosnian	 |Bosanski	 |bs|
|Bulgarian	 |български	 |bg|
|Catalan	 |Català	 |ca|
|Cebuano	 |Cebuano	 |cx*|
|Chinese	 |中文	 |ch*|
|Croatian	 |Hrvatski	 |hr|
|Czech	 |čeština	 |cs|
|Danish	 |Dansk	 |da|
|Dutch	 |Nederlands	 |nl|
|English	 |English	 |en|
|Estonian	 |Eesti	 |et|
|Filipino	 |Filipino	 |ph*|
|Finnish	 |Suomi	 |fi|
|French	 |Français	 |fr|
|Frisian	 |Frysk	 |fy|
|Galician	 |Galego	 |gl|
|Georgian	 |ქართული	 |ka|
|German	 |Deutsch	 |de|
|Greek	 |Ελληνικά	 |el|
|Gujarati	 |ગુજરાતી	 |gu|
|Hebrew	 |עברית	 |he|
|Hindi	 |हिन्दी	 |hi|
|Hungarian	 |Magyar	 |hu|
|Icelandic	 |íslenska	 |is|
|Indonesian	 |Bahasa Indonesia	 |id|
|Italian	 |Italiano	 |it|
|Japanese	 |日本語	 |ja|
|Kannada	 |ಕನ್ನಡ	 |kn|
|Kazakh	 |қазақ	 |kk|
|Khmer	 |ភាសាខ្មែរ	 |kh*|
|Korean	 |한국어	 |ko|
|Kurdish (Kurmanji)	 |Kurdî (Kurmancî)	 |ku|
|Latvian	 |Latviešu	 |lv|
|Lithuanian	 |Lietuvių	 |lt|
|Macedonian	 |македонски	 |mk|
|Malay	 |Melayu	 |ms|
|Malayalam	 |മലയാളം	 |ml|
|Marathi	 |मराठी	 |mr|
|Mongolian	 |Монгол	 |mn|
|Myanmar (Burmese)	 |မြန်မာဘာသာ	 |my|
|Nepali	 |नेपाली	 |ne|
|Norwegian	 |Norsk	 |nb|
|Assamese	 |অসমীয়া	 |as|
|Breton	 |Brezhoneg	 |br|
|Guaraní	 |Guarani	 |gn|
|Javanese	 |Basa Jawa	 |jv|
|Oriya	 |ଓଡ଼ିଆ	 |or|
|Kinyarwanda	 |Ikinyarwanda	 |rw|
|Chinese – Traditional	 |繁體中文	 |zh*|
|Pashto	 |پښتو	 |ps|
|Persian	 |فارسی	 |fa|
|Polish	 |Polski	 |pl|
|Portuguese	 |Português	 |pt|
|Punjabi	 |ਪੰਜਾਬੀ	 |pa|
|Romanian	 |Română	 |ro|
|Russian	 |русский	 |ru|
|Serbian	 |српски	 |rs*|
|Sinhala	 |සිංහල	 |si|
|Slovak	 |Slovenčina	 |sk|
|Slovenian	 |Slovenščina	 |sl|
|Spanish	 |Español	 |es|
|Swahili	 |Kiswahili	 |sw|
|Swedish	 |Svenska	 |sv|
|Tajik	 |Тоҷикӣ	 |tg|
|Tamil	 |தமிழ்	 |ta|
|Telugu	 |తెలుగు	 |te|
|Thai	 |ภาษาไทย	 |th|
|Turkish	 |Türkçe	 |tr|
|Ukrainian	 |українська	 |uk|
|Urdu	 |Урду	 |ur|
|Uzbek	 |O‘zbek	 |uz|
|Vietnamese	 |Tiếng Việt	 |vn*|
|Welsh	 |Cymraeg	 |cy|

## SmallTalk Status Code

|`status` | `statusMessage` | Description | 
| --- | --- | --- |
|200 | 	OK | Normal |
|227 | 	Parameter Required | You have not entered required parameters |
|228 |	Do Not Understand | There is no proper answer to the question you asked |
|403 |	Unauthorized | Invalid API Key |
|429 |	Limit Exceeded | - |
|500 |	Server error | - |

## Badword Probability
The Badword Probability is an index developed by the SimSimi team to identify how unhealthy/malicious a sentence is, and there are some distinguishing techniques for index calculation including advanced deep learning with superior performance. For more information, please see the blog post, [Malcious Sentence Classification Techniques in the SimSimi Service (Korean)](http://blog.simsimi.com/2019/03/blog-post.html).

&nbsp;

&nbsp;

# Bad Score API

With the world's best conversational sentence classification technology, you can accurately and flexibly identify abusive or sensational sentences in in-game chat, real-time broadcast chat, bulletin board comments, and multilingual communication. Using this API, you can also get a variety of options in the traditional word and phrase filter method (WPF), and cover most languages with statistical-based probabilistic similarity-based classification techniques (STAPX). Our deep neural network model-based sentence classification technique (DPD) scored more than 99.3% of F1 score (in Korean), and you can utilize even the highest reliability classification technique (HB10A) verified by 10 panels in a short time by crowdsourcing. can.

## Scoring and Scope

-The more a given sentence violates the SimSimi content rules, the higher the score.
[SimSimi content rules](https://workshop.simsimi.com/en/support#Please%20let%20me%20know%20the%20content%20policy%20of%20the%20SimSimi%20service)

-The Bad Score API determines the expressions in which the sentence itself directly violates the content regulation for dialogue sentences mainly used for chatting. However, it is excluded from the scope of discrimination in the context of the previous dialogue or the meaning and multi-semantic expression formed in response to the utterance of the counterpart.

## Request
You can receive a response by requesting to the Bad-Score API endpoint(`https://wsapi.simsimi.com/{VERSION}/classify/bad`) with the appropriate method(POST), project key, and required parameters(`sentence`, `lang`, `type`).

#### Example Request
``` bash
curl -X POST https://wsapi.simsimi.com/190410/classify/bad \
     -H "Content-Type: application/json" \
     -H "x-api-key: PASTE_YOUR_PROJECT_KEY_HERE" \
     -d '{
            "sentence": "fuck", 
            "lang": "en",
            "type": "DPD"
     }'                     
```
- `sentence` : Sentence for badword classification
- `lang` : Language code ([language-language code table](#BadScore-Supported-Languages))
- `type` : A method for badword classification. Currently only DPD is supported.

#### Example Response
``` json
{
  "status":200,
  "statusMessage":"Ok",
  "bad":"0.985149",
  "request":{
    "sentence":"fuck",
    "lang":"en"
    }
} 
```
- `bad` : Badword probability
- `request` : Request body
- `status`, `statusMessage` : Status information ([Status Code List](#BadScore-Status-Code))

## BadScore Supported Languages
Most language codes are the same as ISO-639-1, but note that there are other cases(*).

|Language Name		|	 Name	|	 Language Code| Performance(F1 Score) |
| --- | --- | --- | --- |
|Arabic	 |العربية	 |ar| 0.9432 |
|English	 |English	 |en| 0.9847 |
|French	 |Français	 |fr| 0.9376 |
|Indonesian	 |Bahasa Indonesia	 |id| 0.9497 |
|Korean	 |한국어	 |ko| 0.9930 |
|Malay	 |Melayu	 |ms| 0.8984 |
|Portuguese	 |Português	 |pt| 0.9836 |
|Turkish	 |Türkçe	 |tr| 0.9502 |
|Vietnamese	 |Tiếng Việt	 |vn*| 0.9132 |

## BadScore Status Code

|`status` | `statusMessage` | Description | 
| --- | --- | --- |
|200 | 	OK | Normal |
|403 |	Unauthorized | Invalid API Key |
|429 |	Limit Exceeded | - |
|500 |	Server error | - |

&nbsp;

&nbsp;

# Teach API

When using the SmallTalk API, you can give priority to talksets taught by Teach API.
<span style="color:red;">If you want to use the features of the Teach API, you need the standard version of the SmallTalk API.</span>

<img src="https://workshop.simsimi.com/images/teach_diagram_01e.png" width="600px" alt="Teach API diagram01">
<img src="https://workshop.simsimi.com/images/teach_diagram_02e.png" width="600px" alt="Teach API diagram02">
<img src="https://workshop.simsimi.com/images/teach_diagram_03e.png" width="600px" alt="Teach API diagram03">

## Teach

You can teach a talkset by requesting to the Teach API endpoint(`https://wsapi.simsimi.com/{VERSION}/teach`) with the appropriate method(POST), project key, and required parameters(`qtext`, `atext`, `lang`, `teach_key`). The talkset will be saved on corresponding project. The teach_key value can be used for classifying talksets.

#### Example Request
``` bash
curl -X POST https://wsapi.simsimi.com/190410/teach \
     -H "Content-Type: application/json" \
     -H "x-api-key: PASTE_YOUR_PROJECT_KEY_HERE" \
     -d '{
            "qtext": "Hello",
            "atext": "Hi, nice to meet you",
            "lang": "ko",
            "teach_key": "example"
     }'                     
```
- `qtext` : Sentence entered
- `atext` : Answer sentence
- `lang` : Language code
- `teach_key` : Value for classfication

#### Example Response
``` json
{
  "status":200,
  "statusMessage":"Ok",
  "request":{
    "qtext": "Hello",
    "atext": "Hi, nice to meet you",
    "lang": "ko",
    "teach_key": "example"
  }
}    
```
- `request` : request body
- `status`, `statusMessage` : status information ([Status Code List](#Teach-Status-Code))

## SmallTalk API

You can utilize taught talksets by SmallTalk API with project's API key and teach_key. The talksets taught by Teach API can be answered first in SmallTalk API. See the ([Response Control](#Response%20Control)) for instructions on how to use it.

## Talksets Manager

You can access the administration page through the project dashboard. The current administration page allows you to view and delete the talksets you taught.

## Teach Status Code

|`status` | `statusMessage` | Description | 
| --- | --- | --- |
|200 | 	OK | Normal |
|403 |	Unauthorized | Invalid API Key |
|500 |	Server error | - |
