---
id: 20230805182307
tags: [aws-saa-c03, ml]
---

# Machine Learning

## Amazon Comprehend

* Amazon Comprehend uses natural language processing (NLP) to extract
  insights about the content of documents. It develops insights by
  recognizing the entities, key phrases, language, sentiments, and other
  common elements in a document
* Use cases:
  * Analysing customer experience with call centre staff - it can be
    used in conjunction with Amazon Transcribe
  * Index and automate product reviews to see whether customers are
    happy with your products
  * Automatically search through contracts and recent court case
    decisions

## Amazon Kendra

* Amazon Kendra is an intelligent search service that uses natural
  language processing and advanced machine learning algorithms to return
  specific answers to search questions from your data
* Use cases:
  * Accelerating research and development by consolidating data from
    various sources (S3 buckets, databases, text files etc.)
  * Improve customer experience by better understanding customer needs
    and returning relevant information
  * Minimising regulatory and compliance risks by automating the
    research of new regulations e.g. HIPAA
  * Increase employee productivity by centralising data into one
    searchable location

## Amazon Textract

* Amazon Textract uses machine learning to automatically extract text,
  handwriting, and data from scanned documents
* Uses machine learning and OCR, it can process text, handwriting,
  tables and more automatically
* Can convert text into data that can be stored in AWS (S3 buckets,
  databases etc.)
* Main use case is converting hand written documents into computer
  readable formats e.g. mortgage application

## Amazon Forecast

* Amazon Forecast is a fully managed service that uses statistical and
  machine learning algorithms to deliver highly accurate time-series
  forecasts
* Users send data in and it automatically learns the data, selects the
  correct machine learning algorithm, and forecasts the data

## Amazon Fraud Detector

* Amazon Fraud Detector is a fully managed fraud detection service that
  automates the detection of potentially fraudulent activities online
* Create a fraud detection machine learning model based on your data -
  this process can be automated
* Use cases:
  * Identifying suspicious online payments by training it against
    previous cases of fraud
  * Detect whether new accounts or users are fraudulent
  * Prevent free trial abuse
  * Detect when accounts are hijacked by fraudulent users

## Amazon Transcribe

* Amazon Transcribe is an automatic speech recognition service that uses
  machine learning models to convert audio to text
* One use case is generating subtitles for video content

## Amazon Lex

* Amazon Lex is an AWS service for building conversational interfaces
  for applications using voice and text
* Use cases:
  * Virtual agents / voice assistants - reduces burden on employees
  * Automate FAQ on websites

## Amazon Polly

* Amazon Polly is a cloud service that converts text into lifelike
  speech
* Create applications that talk and interact with customers using a
  range of languages and accents
* Use cases:
  * Creating applications that speak, improving accessbility of content

## Transribe > Lex > Polly

* This is the how data flows when talking to Alexa

## Amazon Rekognition

* Amazon Rekognition makes it easy to add image and video analysis to
  your applications
* Rekoginition uses deep learning and neural networks to recognise
  pictures and videos
* Use cases:
  * Content moderation e.g. ensuring that all content is family friendly
  * Face detection and analysis - e.g. the clothes a person is wearing
  * Celebrity recognition
  * Recognising objects in live video e.g. smart doorbells

## Amazon SageMaker

* Amazon SageMaker is a fully managed machine learning service. With
  Amazon SageMaker, data scientists and developers can quickly build and
  train machine learning models, and then deploy them into a
  production-ready hosted environment
* Sections:
  * Ground Truth - set up and manage labeling jobs for training datasets
    using active learning and human labeling
  * Notebook - access managed Jupyter Notebook environment
  * Training - train and tune models
  * Inference - Package and deploy ML models at scale
* Offline vs. Online usage
  * Async or batch vs. sync or real-time
  * Generate predicitions for entire dataset in one go vs. at low
    latency
  * Uses SageMaker batch transform vs. SageMaker hosting services
  * Input format varies based on algorithm for both
  * Ouput format depends on algorithm vs. JSON string
* Stages:
  1. Create a model
  1. Create an endpoint configuration
  1. Create an endpoint
* SageMaker Neo
  * Allows customisation of hardware for specific CPU architectures e.g.
    ARM, Intel and Nvidia
  * Provides a compiler to convert ML model to an environment that is
    optimised to execute on the target architecture
  * Models can be created using tools like TensorFlow or PyTorch
* Elastic inference speeds up throughput and decreases latency of real
  time inferences using CPU-based instances - more cost effective than
  the faster, full GPU instance - it must be configured when you create
  a deployable model
* SageMaker supports autoscaling
* Amazon recommends using SageMaker in a HA configuration

## Amazon Translate

* Amazon Translate is a text translation service that uses advanced
  machine learning technologies to provide high-quality translation on
  demand
* Uses deep learning and neural networks to translate between languages
* Use cases:
  * When highly accurate translation is required
  * Integrating translation services into an application
  * When needing a cost-effective translation service
  * Scalable translation services
