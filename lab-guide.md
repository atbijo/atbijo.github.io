# Lab Center – Hands-On Lab 
## Session 6117
## Hands-on Speech to Text Customization and Speech Grammar


**Abhishek Shrivastava**<br/>
Digital Technical Engagement - Data Science and AI<br/>
abhia@ibm.com

**Bijo Thomas**
Digital Technical Engagement - Data Science and AI
bijo.thomas1@ibm.com

**Jason Brown**
Digital Technical Engagement - Data Science and AI
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

* **Language Model Customization**
Customize the machine learning models to speak the terminology of your business.
* **Acoustic Model Customization**
Use domain specific audio to customize the acoustic models
* **Speech Grammar**
Greatly increase the accuracy of speech in situations where speech follows specific pattern or narrow selection of words.
* **Speaker Diarization**
Service can segment and tag transcriptions based on speakers identified in the audio.
* **Word Alternatives, Confidence and Timestamp**
Response includes alternate words that are acoustically similar to the primary word detected, confidence level of each word detected and the timestamps in the audio input at which the words were detected.

This lab explores the customization capabilities and grammar support in Watson Speech to Text service.
