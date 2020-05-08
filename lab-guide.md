# Lab Center – Hands-On Lab 
## Session 6117<br/>Hands-on Speech to Text Customization and Speech Grammar


**Abhishek Shrivastava**<br/>
Digital Technical Engagement - Data Science and AI<br/>
abhia@ibm.com

**Bijo Thomas**<br/>
Digital Technical Engagement - Data Science and AI<br/>
bijo.thomas1@ibm.com

**Jason Brown**<br/>
Digital Technical Engagement - Data Science and AI<br/>
jasonbro@us.ibm.com

# 1 Introduction

Watson Speech to Text service is part of AI services available in IBM Cloud.

The service provides speech transcription capabilities for your applications. The service leverages machine learning to combine knowledge of grammar, language structure, and the composition of audio and voice signals to accurately transcribe the human voice. It continuously updates and refines its transcription as it receives more speech.

The service provides various interfaces that make it suitable for any application where speech is the input and a textual transcript is the output. Example applications include

* Voice control of applications, embedded devices, and vehicle accessories
* Transcribing meetings and conference calls
* Dictating email messages and notes

The service is ideal for clients who need to extract high-quality speech transcripts from call center audio. Clients in industries such as financial services, healthcare, insurance, and telecommunication can develop cloud-native applications for customer care, customer voice, agent assistance, and other solutions.

## 1.1 Key Capabilities

Watson Speech to Text provides out of the box speech to text capability in several languages such as English, Spanish, German, Chinese, Japanese, Korean etc. using audio in most common audio formats. Audio files are broadly classified as Broadband and Narrowband. Audio that are sampled at 16 kHz or higher are supported using Broadband models and audio that are sampled at 8 kHz are supported using Narrowband models.

The service provides significant additional data about the transcription and provides powerful customization capabilities that could be leveraged for domain specific audio.

* **Language Model Customization**<br/>
Customize the machine learning models to speak the terminology of your business.
* **Acoustic Model Customization**<br/>
Use domain specific audio to customize the acoustic models
* **Speech Grammar**<br/>
Greatly increase the accuracy of speech in situations where speech follows specific pattern or narrow selection of words.
* **Speaker Diarization**<br/>
Service can segment and tag transcriptions based on speakers identified in the audio.
* **Word Alternatives, Confidence and Timestamp**<br/>
Response includes alternate words that are acoustically similar to the primary word detected, confidence level of each word detected and the timestamps in the audio input at which the words were detected.

This lab explores the customization capabilities and grammar support in Watson Speech to Text service.

## 1.2 High Level Runtime Architecture

Speech to Text deployments can have varied architecture. The following diagram illustrates an example in which audio input from user is transcribed using Speech to Text service. The audio can be from various channels such as mobile devices, internet browser, live microphone, stored audio files etc. The application logic layer can be used invoke the speech to text service and process the transcription response.

![Architecture](./images/architecture.png)

This lab uses a much simplified architecture, which can be outlined as the following diagram.

![Lab Architecture](./images/lab-architecture.png)

Speech to Text is powered by several machine learning models that are provided out of the box and are customizable. The models are provided for several natural languages.

## 1.3 Customization

The IBM Speech to Text service offers a customization interface that you can use to augment its speech recognition capabilities. You can use customization to improve the accuracy of speech recognition requests by customizing a base model for your domain and audio. Customization is available for only some languages and at different levels of support for different languages.

The customization interface supports both custom language models and custom acoustic models. The interfaces for both types of custom model are similar and straightforward to use. Using either type of custom model with a recognition request is also straightforward: You specify the customization ID of the model with the request.

Speech recognition works the same with or without a custom model. When you use a custom model for speech recognition, you can use all of the input and output parameters that are normally available with a recognition request.

### 1.3.1 Language Customization

The service was developed with a broad, general audience in mind. The service's base vocabulary contains many words that are used in everyday conversation. Its models provide sufficiently accurate recognition for many applications. But they can lack knowledge of specific terms that are associated with particular domains.

The language model customization interface can improve the accuracy of speech recognition for domains such as medicine, law, information technology, and others. By using language model customization, you can expand and tailor the vocabulary of a base model to include domain-specific terminology.

You can create a custom language model and add corpora and words specific to your domain. Once you train the custom language model on your enhanced vocabulary, you can use it for customized speech recognition. The service can typically train any custom model in a matter of minutes. The level of effort that it takes to create a model depends on the data that you have available for the model.

### 1.3.2 Acoustic Customization

Similarly, the service was developed with base acoustic models that work well for various audio characteristics. But in cases like the following, adapting a base model to suit your audio can improve speech recognition:

* Your acoustic channel environment is unique. For example, the environment is noisy, microphone quality or positioning are suboptimal, or the audio suffers from far-field effects.
* Your speakers' speech patterns are atypical. For example, a speaker talks abnormally fast or the audio includes casual conversations.
* Your speakers' accents are pronounced. For example, the audio includes speakers who are talking in a non-native or second language.

The acoustic model customization interface can adapt a base model to your environment and speakers. You create a custom acoustic model and add audio data (audio resources) that closely match the acoustic signature of the audio that you want to transcribe. Once you train the custom acoustic model with your audio resources, you can use it for customized speech recognition.

The length of time that it takes the service to train the custom model depends on how much audio data the model contains. In general, training takes twice the length of the cumulative audio. The level of effort that it takes to create a model depends on the audio data that you have available for the model. It also depends on whether you use transcriptions of the audio.

### 1.3.3 Grammars

Custom language models allow you to expand the service's base vocabulary. Grammars enable you to restrict the words that the service can recognize from that vocabulary. When you use a grammar with a custom language model for speech recognition, the service can recognize only words, phrases, and strings that are recognized by the grammar. Because the grammar defines a limited search space for valid matches, the service can deliver results faster and more accurately.

You add a grammar to a custom language model and train the model just as you do for a corpus. Unlike a corpus, however, you must explicitly specify that a grammar is to be used with a custom model during speech recognition.

# 2 Getting Started

This lab is based on Watson Speech to Text service available in IBM public cloud. You need a Standard plan instance of Speech to Text to perform customizations. For the purpose of this lab, each of you will get following from the instructor, which will allow you access to a pre-provisioned Standard plan instance of the service in IBM Cloud.

1. API Key – Access key to use the API
2. URL – Service location

> For you to work on Speech to Text customization after this lab on your own, you will need to create your Standard plan Speech to Text instance in IBM Cloud. You will need an IBM Cloud account to create a service instance. Creating account and service instance is not within the scope of this lab, but you can refer to Appendix I of this lab guide for some quick guide on doing it.

This lab guide refers to the directory **C:\Lab** as your **work directory**. If you don't have that directory in your VM, please create it.

All terminal commands listed in this lab are defined to be executed using the **cmd** terminal available in the Windows 10 VM that you have access to as part of this lab. Also, they are defined to be executed from the work directory. If you execute from a different directory, you will need to make necessary changes to the commands.

![Blank cmd Window](./images/cmd.png)

Since API Key and URL are part of almost all commands you use this lab, for convenience, we store them as environment variables and the commands refer to them as variables. If you open a new terminal window, you will need to set them again in the new window.

```batch
C:\Lab> set APIKEY=[Your API Key with Double Quotes]
C:\Lab> set URL=[Your Service URL without Double Quotes]
```

For example, if your API Key is `b1DzrXLeZWnuRdylhacJTA4e-_Y4Vk_2bZoO5TEDErt1` and URL is `https://api.us-south.speech-to-text.watson.cloud.ibm.com/instances/cb07aa2a-e12e-4ae3-a8e1-6c2b31ef385e`, the commands will be

```batch
C:\Lab> set APIKEY="b1DzrXLeZWnuRdylhacJTA4e-_Y4Vk_2bZoO5TEDErt1"
C:\Lab> set URL=https://api.us-south.speech-to-text.watson.cloud.ibm.com/instances/cb07aa2a-e12e-4ae3-a8e1-6c2b31ef385e
```

Most commands use **curl** to execute. So, let's make sure you have curl in your Window 10 VM. Run following command in your terminal

```batch
C:\Lab> curl
```

![Test curl Presence](./images/curl.png)

If you see the same response as in the above screenshot, you have curl installed and proceed.


