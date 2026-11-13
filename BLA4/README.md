AWS Machine Learning Engineer – Associate: Managed AI Services and SageMaker Algorithms
Technical study notes and reference documentation covering AWS managed AI services, Amazon SageMaker AI, and selected SageMaker built-in algorithms.

Series: AWS Machine Learning Engineer – Associate
Prepared by: RJ Programming
Scope: Three presentations: Managed AI Services — Part 1, Managed AI Services — Part 2, and Amazon SageMaker AI & Built-in Algorithms.

Table of Contents
1. Overview
2. AWS Managed AI Services: Language and Conversational AI
   - Amazon Comprehend
   - Amazon Translate
   - Amazon Polly
   - Amazon Lex
3. AWS Managed AI Services: Vision, Recommendations, Documents, and Analytics
   - Amazon Rekognition
   - Amazon Personalize
   - Amazon Textract
   - AWS Quick and AWS Quick Sight
4. Amazon SageMaker AI
5. SageMaker Built-in Algorithms
   - Supervised Learning
   - Unsupervised Learning
   - Natural Language Processing
   - Forecasting and Computer Vision
6. Service and Algorithm Selection
7. Architecture and Operational Considerations
8. Key Takeaways
9. References
    
Overview
Amazon Web Services (AWS) supports machine learning through two complementary approaches. Managed AI services supply task-specific AI capabilities through APIs; Amazon SageMaker AI provides tools and managed infrastructure to build, train, tune, and deploy machine learning models. The appropriate choice depends on whether an application needs an established capability or a model trained for its own data and objectives.

The topics in this repository emphasize three aspects of the AWS ML ecosystem:
- Language and conversation: understanding, translating, speaking, and interacting with text or voice.
- Vision and business data: interpreting images, extracting documents, generating recommendations, and reporting results.
- Custom machine learning: selecting and training algorithms for classification, regression, clustering, anomaly detection, NLP, forecasting, and computer vision.
A simplified distinction is:
Approach	Primary purpose	Typical input	Typical output
AWS managed AI service	Add an existing AI capability using an API	Text, speech requests, images, documents, or user interactions	Sentiment, translations, audio, labels, extracted fields, or recommendations
SageMaker AI built-in algorithm	Train a task-specific model using an AWS-provided implementation	Training dataset and algorithm configuration	Trained model artifacts, subsequently used for predictions
SageMaker JumpStart pretrained model	Start from an existing trained model	Input data and, when appropriate, fine-tuning data	Predictions from a deployed or adapted pretrained model


Important: Managed does not mean that every service works identically. Services differ in configuration, required data, output formats, and deployment options. Some, including recommendation systems, still learn from customer-provided interaction data.
AWS Managed AI Services: Language and Conversational AI
Amazon Comprehend
Amazon Comprehend is a natural language processing (NLP) service for extracting information from unstructured text. Instead of treating a document as a sequence of unrelated words, NLP examines language patterns and returns structured findings that applications can process.

Core capabilities
- Sentiment analysis: identifies positive, negative, neutral, or mixed sentiment in text.
- Entity recognition: identifies references to people, places, organizations, dates, and other supported entity types.
- Key phrase extraction: finds significant terms and phrases that summarize important aspects of text.
- Language detection: identifies the language of supplied text.
- Personally identifiable information (PII) detection: locates supported types of sensitive personal information.
Example: A retailer receives the review, “Delivery was fast, but the box was damaged.” The message contains both favorable and unfavorable feedback. Comprehend can help classify the sentiment and identify important wording for subsequent analysis. A company might aggregate these results across large volumes of support messages to discover patterns in delivery complaints.

Common applications: review analysis, support-ticket routing, document categorization, and customer-feedback monitoring. Extracted entities and sentiment should be treated as model outputs that may require validation for sensitive or high-impact uses.
Amazon Translate
Amazon Translate provides neural machine translation between supported languages. It enables multilingual interfaces and communication workflows without an organization developing a translation model independently.

For example, a support application can translate the English message “Hello, how can I help?” into Spanish as “Hola, ¿cómo puedo ayudar?” A typical translation workflow supplies the source text, source or detected language, and target language, then receives translated text.

Typical uses include translating product descriptions, making support messages accessible in several languages, localizing application content, and creating multilingual communication tools. Translation is sensitive to context, specialized terminology, and cultural nuance; critical content can benefit from human review.
Amazon Polly
Amazon Polly is a text-to-speech (TTS) service. It synthesizes spoken audio from written text, making it useful when an application must communicate through speech rather than only a visual interface.

Polly supports voices and languages and provides Speech Synthesis Markup Language (SSML) controls for supported aspects of speech rendering, such as pauses and pronunciation. Applications can request audio output to play through an interface or save for later use.

Example: An educational application submits the sentence “Welcome to today's lesson” and receives an audio response. The same approach can support spoken notifications, accessible reading experiences, and interactive voice prompts.

Distinction: Polly converts text to audio; it is not a service for transcribing existing audio into text.
Amazon Lex
Amazon Lex enables developers to create text and voice conversational interfaces. Its purpose is to interpret requests, collect the information required to complete them, and connect the conversation to application logic.

Three foundational concepts are:
Concept	Definition	Appointment-booking example
Intent	The goal the user is attempting to accomplish	BookAppointment
Utterance	A phrase a user says or types	“Book an appointment”
Slot	A piece of information required for a task	Date, time, or service


A Lex bot can interpret a booking request, prompt for missing details, validate responses, and invoke a backend such as AWS Lambda to perform fulfillment. Lex is commonly applied to self-service support, reservation flows, appointment scheduling, and internal help desks.

Design consideration: A chatbot needs more than intent detection. A complete application should account for unclear requests, unavailable options, fallback responses, error handling, and access to backend systems.
Language service comparison
Service	Input	Main capability	Output
Comprehend	Text	Analyze meaning and patterns	Sentiment, entities, phrases, language, or PII findings
Translate	Text	Change languages	Translated text
Polly	Text	Synthesize speech	Audio
Lex	Text or speech interactions	Manage conversational intent and information collection	Interpreted intent, captured slots, and bot responses


AWS Managed AI Services: Vision, Recommendations, Documents, and Analytics
Amazon Rekognition
Amazon Rekognition provides image and video analysis capabilities. It identifies visual features and can return structured results that applications use to categorize or process media.

Key tasks discussed in this series include object and scene detection, image labeling, content moderation, video analysis, and text detection in images. For instance, a photo application may upload an image of a dog in a park and receive labels describing the visible objects or environment.

The results can support search, photo categorization, media organization, or workflows that flag content for review. Visual recognition outputs are predictions; their reliability can vary with image quality and context. Human oversight is especially important when outputs affect people.
Amazon Personalize
Amazon Personalize helps build recommendation systems that tailor content or items to individual users. Rather than returning the same list to everyone, a recommendation application can use interaction history and item information to rank options that may be relevant to a particular user.

Data sources may include:
- User interactions, such as clicks, views, or purchases.
- Item attributes, such as category or metadata.
- Additional user information, when available and appropriate.
Example: A streaming platform observes that a viewer frequently watches science-fiction films. Using interactions and available content information, a recommendation system can rank related titles for that viewer. In e-commerce, the same principle supports product discovery, related items, and personalized results.

Recommendation quality depends on the available data and the definition of success. New users, sparse histories, changing interests, and privacy requirements can complicate system design.
Amazon Textract
Amazon Textract extracts text and structured information from scanned documents and document images. Beyond recognizing characters, it can identify supported structures such as forms and tables.

The service can process printed text, handwriting, form key-value pairs, and tabular information. A common use case is invoice processing. Rather than manually entering the invoice date and total, an application can extract recognized values and pass them to an accounting or review workflow.

Example workflow:
Scanned invoice
      |
      v
 Amazon Textract
      |
      v
Text, fields, and table structure
      |
      v
Validation and business processing
Textract is better suited to extracting document structure than a general-purpose image-labeling service. As with other extraction systems, important values should be checked against the source document when accuracy is essential.
AWS Quick and AWS Quick Sight
Naming update (November 2026): The presentation refers to Amazon Quick; AWS renamed it AWS Quick on November 9, 2026. Its business-intelligence component, previously Amazon Quick Sight, is now called AWS Quick Sight. The AWS announcement confirms that existing Quick Sight dashboards, datasets, and analyses remain available. See AWS's naming announcement.

For the analytics portion of this series, AWS Quick Sight is the relevant capability. It helps users explore data, build visualizations, monitor key performance indicators (KPIs), and share dashboards for business decision-making.

Example: A sales dashboard can visualize revenue by period, compare trends, and highlight performance changes. The underlying data may come from business systems or AWS-connected data sources. This differs from image recognition or text extraction: business intelligence focuses on interpreting and communicating metrics rather than training a model to recognize a particular object or phrase.

The broader AWS Quick offering also includes AI-powered capabilities for working with enterprise information and applications. Therefore, Quick and Quick Sight should not be treated as simply interchangeable names.
Vision and business service comparison
Service	Main question it answers	Example
Rekognition	What appears in an image or video?	Label photos or analyze visual content
Personalize	What should this user see next?	Recommend movies or products
Textract	What text and fields are in this document?	Extract invoice details
AWS Quick Sight	What patterns and metrics are in this data?	Display sales trends in a dashboard


Amazon SageMaker AI
Purpose and capabilities
Amazon SageMaker AI is a managed machine learning service for developing, training, tuning, and deploying ML models. It reduces the infrastructure management involved in model experimentation and production inference, while allowing practitioners to choose among different algorithms and frameworks.

The presentation highlights four main capabilities:
1. Managed ML development: build models using AWS-managed resources.
2. Flexible model implementation: select built-in algorithms, supported frameworks, or custom code.
3. Training: run jobs on provisioned compute resources, including suitable CPU or GPU instances, and retain model artifacts.
4. Inference: use trained models for real-time predictions or batch processing.
Typical model lifecycle
Data collection and preparation
             |
             v
      Amazon S3 / dataset
             |
             v
 Select algorithm or framework
             |
             v
  SageMaker training job
             |
             v
 Model evaluation and tuning
             |
             v
       Model artifacts
             |
             v
  Deployment / batch inference
             |
             v
    Predictions and monitoring
Data preparation: Training data must represent the task and should generally be separated into training and evaluation sets. For supervised learning, labels identify the target output the model should learn to predict.

Algorithm selection: The structure of the dataset and the intended prediction determine whether classification, regression, clustering, forecasting, or another approach is appropriate.

Training and evaluation: SageMaker training jobs use data and configuration settings to produce model artifacts. Evaluation metrics depend on the task: classification might use precision, recall, or accuracy; regression and forecasting may use error measures; clustering may require different validation techniques.

Deployment and monitoring: Trained models can be used for real-time or batch inference. Production workflows must consider response time, model drift, operating cost, access controls, and whether predictions continue to meet application requirements.
Built-in algorithms versus pretrained models
A SageMaker built-in algorithm is an AWS-provided implementation of a machine learning method. Typically, the practitioner supplies training data, specifies configuration and hyperparameters, starts a training job, and evaluates the resulting model.

A pretrained model, such as one made available through SageMaker JumpStart, already contains learned parameters from prior training and may be deployed or adapted to another task. Some pretrained models may need fine-tuning for a specific use case.
Feature	Built-in algorithm	Pretrained model
Starting point	Algorithm implementation	Already-trained model weights
Task-specific training	Typically required	May be optional or involve fine-tuning
Primary value	Avoid implementing common algorithms from scratch	Reduce effort needed to start from a capable model
Example	Train XGBoost on labeled tabular data	Adapt a pretrained model for a supported task


The distinction matters because a built-in algorithm does not automatically mean the resulting model is ready to predict without training.
SageMaker Built-in Algorithms
The algorithms below follow the categories in the SageMaker presentation. They are a selected set, not a complete inventory of every algorithm currently listed by AWS.
Supervised learning algorithms
Supervised learning uses examples with known target values. The goal is to learn a mapping between input features and labels or numeric outcomes.
XGBoost
XGBoost uses gradient-boosted decision trees, where successive trees improve an ensemble's predictions. It supports classification and regression and is widely applicable to structured or tabular data.
- Example: Predict customer churn based on usage history and account attributes.
- Best fit: Tabular datasets where relationships among variables may be nonlinear.
- Consideration: Requires careful evaluation and tuning to avoid overfitting and to select useful features.
Linear Learner
Linear Learner fits linear models for regression and classification. It is a practical baseline when inputs can be represented as numeric features and a relatively simple relationship is sufficient.
- Example: Predict a numerical outcome from measurable features, or classify records using a linear decision boundary.
- Best fit: Problems where simplicity, speed, and baseline performance are priorities.
- Consideration: Complex nonlinear relationships may require additional feature engineering or different models.
K-Nearest Neighbors (k-NN)
k-NN predicts using nearby labeled examples in a feature space. In classification, neighbors influence the class assigned to a new record; in regression, nearby target values inform the numeric estimate.
- Example: Classify an item using examples with similar measured features.
- Best fit: Similarity-based predictions when meaningful distances between examples can be calculated.
- Consideration: Feature scaling and the choice of k can significantly affect the results.
Factorization Machines
Factorization Machines model interactions among features efficiently, particularly in high-dimensional sparse data. They are useful when combinations of features carry information that individual features do not fully capture.
- Example: Predict how likely a user is to interact with an item using sparse user/item attributes.
- Best fit: Recommendation-style or other sparse-feature prediction problems.
- Consideration: The quality of the feature representation and interaction data matters.
Unsupervised learning algorithms
Unsupervised learning finds structure or unusual patterns in data without requiring a labeled target for the core task.
K-Means
K-Means partitions observations into K groups based on similarity. Each cluster is represented by a center, and records are assigned to the most appropriate group under the chosen distance measure.
- Example: Segment shoppers using purchasing behavior.
- Best fit: Grouping observations into a specified number of relatively coherent clusters.
- Consideration: The number of clusters and feature scaling affect the output.
Principal Component Analysis (PCA)
PCA transforms the original features into a smaller set of components intended to preserve substantial variation in the data. This can simplify later processing and reduce redundancy.
- Example: Reduce dozens of correlated measurements into a smaller set of features.
- Best fit: Dimensionality reduction and feature preprocessing.
- Consideration: The resulting components may be less directly interpretable than the original variables.
Random Cut Forest (RCF)
Random Cut Forest is used for anomaly detection. It identifies observations that stand apart from the broader patterns in a dataset.
- Example: Flag an unusual sensor reading or an unexpected system metric.
- Best fit: Discovering unusual observations in numeric data.
- Consideration: An unusual reading is not automatically an error or harmful event; flagged records require context.
IP Insights
IP Insights learns patterns in associations between entities and IP addresses to identify unusual combinations.
- Example: Detect a sign-in coming from an IP address that is atypical for an account's historical activity.
- Best fit: IP-address anomaly detection, including security-oriented monitoring.
- Consideration: An unusual association is only a signal for investigation, not proof of misuse.
Natural language processing algorithms
SageMaker supports NLP tasks through specialized algorithms that operate on text, documents, or representations of textual and other objects.
BlazingText
BlazingText is optimized for text classification and learning word embeddings. Word embeddings map words into numeric representations that help machine learning systems use relationships among terms.
- Example: Assign support tickets to predefined categories.
- Best fit: Text classification and embedding generation.
Latent Dirichlet Allocation (LDA)
LDA is a probabilistic topic-modeling algorithm. It represents documents as mixtures of topics, with topics represented through patterns of words.
- Example: Discover recurring themes in a collection of articles.
- Best fit: Unsupervised topic discovery in document collections.
Neural Topic Model (NTM)
NTM also identifies topics in document collections but uses a neural-network-based method.
- Example: Organize a large collection of unclassified documents by recurring subjects.
- Best fit: Topic modeling with a neural approach.
LDA versus NTM: Both discover themes without requiring preassigned topic labels; they differ in how the topic representations are learned.
Object2Vec
Object2Vec learns dense vector representations of objects, including information about relationships between pairs of objects. In contrast to the unsupervised topic models above, its training uses examples of relationships or labels.
- Example: Produce embeddings for related content or objects to support downstream prediction.
- Best fit: Representation learning and feature engineering.
Sequence-to-Sequence (Seq2Seq)
Sequence-to-Sequence models learn mappings between input and output sequences. A familiar application is machine translation, where a source-language sentence is transformed into a corresponding target-language sentence.
- Example: Train a task-specific sequence translation model.
- Best fit: Problems where the input and desired output are sequences.
- Comparison: Amazon Translate provides a managed translation API; a Seq2Seq training workflow is appropriate when a custom trained model is needed.
Forecasting and computer vision algorithms
DeepAR Forecasting
DeepAR is a supervised forecasting algorithm for scalar time series. It learns from historical sequences and can use patterns across related time series to generate predictions about future values.
- Example: Forecast future demand using historical sales observations.
- Best fit: Time-series forecasting with suitable historical data.
- Consideration: Evaluation should respect temporal order; random shuffling may not represent future forecasting conditions.
Image Classification
Image Classification assigns one or more labels to an image, depending on the model and task. The goal is to identify the category represented by the whole image.
- Example: Classify a picture as containing a dog, car, or flower.
- Best fit: Image-level categorization.
Object Detection
Object Detection identifies object categories and their locations, commonly represented by bounding boxes.
- Example: Locate multiple vehicles in an image.
- Best fit: Tasks that need both object identity and approximate position.
Semantic Segmentation
Semantic Segmentation assigns a class to individual pixels in an image, producing a detailed class map rather than only an image-level label or bounding boxes.
- Example: Mark which pixels belong to a road, vehicle, or background.
- Best fit: Fine-grained image understanding.
Computer vision comparison: Classification answers what category is present? Detection answers what and where? Segmentation answers which pixels belong to each class?
Service and Algorithm Selection
The following mapping connects common project requirements to the corresponding AWS service or SageMaker algorithm.
Requirement	Option to consider	Reason
Analyze sentiment or entities in customer feedback	Amazon Comprehend	NLP analysis of text
Translate text into another language	Amazon Translate	Managed neural translation
Read written text aloud	Amazon Polly	Text-to-speech synthesis
Collect information through a chatbot	Amazon Lex	Intent and slot handling
Recognize objects and scenes in images	Amazon Rekognition	Visual recognition API
Recommend products or content	Amazon Personalize	Personalized ranking/recommendation capabilities
Extract fields from scanned invoices	Amazon Textract	Document text and structure extraction
Build dashboards and analyze trends	AWS Quick Sight	Business intelligence and reporting
Predict churn or a numeric outcome from tabular data	XGBoost / Linear Learner	Supervised classification or regression
Find clusters of similar customers	K-Means	Unsupervised grouping
Reduce the number of input features	PCA	Dimensionality reduction
Identify anomalous numeric measurements	Random Cut Forest	Anomaly detection
Detect atypical account/IP associations	IP Insights	IP-specific anomaly modeling
Classify text	BlazingText	Text classification
Discover topics in documents	LDA / NTM	Topic modeling
Create vector representations of related objects	Object2Vec	Learned embeddings
Train a custom text-to-text sequence model	Sequence-to-Sequence	Sequence mapping
Forecast future demand	DeepAR	Time-series forecasting
Categorize an entire image	Image Classification	Image-level prediction
Locate multiple items in an image	Object Detection	Bounding boxes and class labels
Label individual image pixels	Semantic Segmentation	Pixel-level prediction


These are starting points, not universal rules. Accuracy, data preparation, supported formats, cost, latency, governance, and operational constraints should also influence the final selection.
Architecture and Operational Considerations
Integrating managed services
A typical service integration includes an application, API or SDK request, AWS service response, and business logic that consumes the result.
Client / business application
            |
            v
      Application logic
            |
            v
       AWS AI service
            |
            v
   Structured result or media
            |
            v
Validation, storage, or next action
For instance, a document-processing workflow might store an uploaded file, send it to Textract, validate extracted fields, and then save approved results in a business database. A multilingual chatbot could use Lex for conversation management while integrating translation or speech capabilities where appropriate.
Practical considerations
- Data security and permissions: Use appropriately scoped AWS Identity and Access Management (IAM) permissions and secure the data passed into service APIs.
- Data quality: Incorrect, incomplete, or poorly formatted inputs can limit ML performance regardless of the service used.
- Evaluation: Assess classification quality, extraction accuracy, recommendation relevance, or forecasting error using metrics appropriate to the task.
- Cost and resource management: Review request volumes, training compute, endpoint usage, and storage. SageMaker resources such as provisioned inference endpoints may incur charges while running.
- Monitoring: Track failures, changing inputs, degraded prediction performance, and application-level outcomes.
- Responsible application design: Use review processes when outputs are uncertain or potentially consequential. Protect sensitive personal information.
Certification study emphasis
For the AWS Machine Learning Engineer – Associate exam, understanding which service fits which requirement is as important as memorizing definitions. In particular, distinguish:
1. Comprehend vs. Translate vs. Polly vs. Lex: text understanding, translation, audio synthesis, and conversation management.
2. Rekognition vs. Textract: general media analysis versus structured document extraction.
3. Personalize vs. SageMaker recommendation modeling: managed personalized recommendations versus building a more custom model or feature pipeline.
4. Built-in algorithm vs. pretrained model: AWS-provided training implementation versus an already trained model.
5. Classification vs. regression vs. clustering vs. anomaly detection: different objectives require different learning strategies and evaluation methods.
6. Image classification vs. object detection vs. segmentation: labels for whole images, bounding-box locations, or pixel-level regions.
Key Takeaways
AWS offers both task-specific managed AI services and general-purpose machine learning development capabilities. Managed services can simplify text analysis, translation, speech generation, chatbots, image understanding, recommendations, document extraction, and analytics. SageMaker AI provides more control over training data, algorithm selection, model evaluation, and deployment.

SageMaker built-in algorithms cover a broad variety of problems: XGBoost and Linear Learner for supervised prediction; K-Means and PCA for clustering and dimensionality reduction; Random Cut Forest and IP Insights for anomaly detection; BlazingText, LDA, NTM, Object2Vec, and Seq2Seq for language and representation tasks; DeepAR for forecasting; and classification, detection, and segmentation algorithms for vision tasks.

The central design principle is to start with the problem, identify the data and required output, and then choose the managed service or trainable algorithm whose capabilities match the task.


References
Official AWS resources used for technical terminology, algorithm categories, and service positioning:
1. AWS Decision Guide — Choosing an AWS machine learning service
2. Amazon SageMaker AI — Built-in algorithms and pretrained models
3. Amazon SageMaker AI — Parameters for built-in algorithms
4. Amazon SageMaker AI — Types of algorithms and implementation approaches
5. AWS — Amazon Quick is now AWS Quick (November 9, 2026)
6. AWS — Amazon Comprehend
7. AWS — Amazon Translate
8. AWS — Amazon Polly
9. AWS — Amazon Lex
10. AWS — Amazon Rekognition
11. AWS — Amazon Personalize
12. AWS — Amazon Textract
13. AWS — Amazon SageMaker AI
Documentation note: This README expands the three presentation topics into a structured study reference. The example scenarios are illustrative rather than results from tested AWS deployments. AWS service names, features, supported regions, and algorithms can change; consult the linked documentation when implementing a solution.

RJ Programming | AWS Machine Learning Engineer – Associate Learning Series
