<!-- This is the markdown template for the final project of the Building AI course, 
created by Reaktor Innovations and University of Helsinki. 
Copy the template, paste it to your GitHub README and edit! -->

# Scam Call Buster

Final project for the [Building AI course](https://buildingai.elementsofai.com/).\
[Elements of AI](https://www.elementsofai.com/), [University of Helsinki](https://www.helsinki.fi), Finland.

## Summary

This project aims to apply what we learn't in the Building AI course to real life needs.\
In the course, we understood concepts of modeling an AI which can flag potential spam emails.\
We can extend the same idea to flag potential scam telephone calls.\
We will develop this project as a **Proof-Of-Concept (POC)**, and later in the **What next?** section, see how we can grow it into a stronger implementation.

## Background

Cyber theft has been a major issue in this age of advancing technology.

Sr. Citizens and people who are not tech-savvy, have been particularly vulnerable to it. Many loosing not only a substantial amount, but some even loosing all of their life savings. In extreme cases, some becoming homeless or even committing suicide, due to mental and emotional, shock and trauma.

If they would have a "friend in AI" which would warn them in time, they could avoid becoming victims of such crimes. We will focus on identifying such frauds at the initial phase itself i.e. a phone call.

All scams over phone calls follow a predetermined theme, e.g. Gift Cards, Grand Parents, Remote Access, Digital Arrest, etc. Our app will try to check, if what the speaker at the other end is speaking about, falls under such fraud themes. 

## How is it used?

The app will be installed on a personal computer.\
On first install, the user will be prompted for a sample speech in his / her voice for the AI to learn how the user sounds.\
During a call, the user puts the phone on speaker and starts the AI app.\
The app, listens to the conversation, distinguishes the user's voice vs the other person's voice and transcribes what the person at the other end is saying.\
Simultaneously, it keeps analysing the content for a potential fraud theme, as the conversation progresses.\
If it finds a matching theme, it flags it to the user.

## Data sources and AI methods

Selecting Python for our code implementation, at each step below, related Python libraries are suggested.

The app is working on live audio stream which is captured using the microphone on the PC. Python library **pyaudio**.

However, there is a complexity here - it needs to distinguish between the 2 speakers on the call. This is called **Speaker Diarization**.  Python library **pyannote.audio**.

It further needs to recognise the user's voice so that it can ignore it and focus on the other speaker. This is called **Speaker Identification**. For this, the app will collect a sample of user's voice during first install (with provision to resample later again if required) and store it. **Gaussian Mixture Model - GMM** could be used to train it to recognise the user's voice. Python library **sklearn**.

The app then keeps listening till stopped by the user. It hears in chunks, e.g. 5 seconds. As audio comes through, it compares with the user's voice model and transcribes the non-matching one, i.e. the other speaker. It keeps appending this transcription to a data structure which forms the content of what the other person is saying. Python library **speechrecognition**.

It keeps analysing the target content for a matching scam theme. Models such as **Naive Bayes Classifier** or **Random Forest** could be used to train it to recognise such themes. Python library **sklearn**.

If it finds a scam theme with a high probability, it flags the same to the user.

## Challenges

* Scam calls come unannounced. Our solution requires a separate computer to hear the conversation, which may not be always available. 
* We could design it to work on a mobile phone device, which may have it's Operating System (OS) related restrictions, integrations and interfaces.
* At current level of hardware used for personal use, it might be difficult to implement advance models or perfect analysis in real time without slippage, e.g. gift cards context spoken by a family member slipping through as potential fraud.
* There is also an **ethical concern** of hearing and transcribing what the other person is saying, without his / her knowledge.

## What next?

- We could design a mobile app where it automatically has access to the ongoing call or can be handily available to analyse landline or other mobile calls on speaker.
- It could speak to the scammer on behalf of the user using Text-To-Speech (TTS) and use algorithms to probe more about scammer's modus operandi, also saving user from trauma.
- The app could expand to include other sources of fraud initiation e.g. chats, emails etc.
- It could be trained to understand and work with more languages
- It could partner with government agencies and connect with their servers and APIs for the following:
  - include in it's analysis, a list of known suspect call numbers, IP addresses, etc.
  - add new types of fraud themes in its analysis as they evolve.
  - provide information to user about how and where to report such frauds or can report them to the authorities itself.

## Acknowledgments

* [Online Scams: An overview of 19+ internet scams](https://us.norton.com/blog/emerging-threats/internet-scams) by Oliver Buxton at Norton
* [Economic Impact of Cyber Crime](https://www.csis.org/analysis/economic-impact-cybercrime) by CSIS - Center for Strategic & International Studies
* [What is Automatic Speech Recognition](https://www.assemblyai.com/blog/what-is-asr/) by Kelsey Foster at AssemblyAI
* [Introduction to Speech Processing](https://speechprocessingbook.aalto.fi/index.html) online book hosted by [Aalto University](https://www.aalto.fi), Finland / [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/); Authors: Tom Bäckström and Okko Räsänen and Abraham Zewoudie and Pablo Pérez Zarazaga and Liisa Koivusalo and Sneha Das and Esteban Gómez Mellado and Marieum Bouafif Mansali and Daniel Ramos and Sudarsana Kadiri and Paavo Alku and Mohammad Hassan Vali
* [Daisy the 'AI granny' speaks to scammer](https://youtu.be/bL9iJJICOLc) by Guardian News on YouTube
* Google and Gemini AI for general search and implementation related inputs
