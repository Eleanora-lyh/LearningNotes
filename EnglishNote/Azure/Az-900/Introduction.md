## Introduction

I currently manage the support and **proactive** services experience for a **portfolio** of Microsoft customers, many of whom have either already made a significant transition from **on-premises** to Azure or are <u>in the process of</u> evaluating a move to Azure. I field questions daily about Azure services, deployment strategies, and proactive services designed to not only educate our customers on Azure and Microsoft 365, but also assist them in planning, deploying, and supporting their Azure and M365 **workloads**.

Continuing technical training is one of the **commitments** that most Microsoft employees <u>make</u> <u>in addition to</u> the core responsibilities of their roles. <u>As part of</u> that commitment, I completed the AZ-900 Microsoft Azure Fundamentals Certification. The certification helped broaden my background across the entire Azure service portfolio. It also **reinforced** my understanding that not only highly technical roles benefit from the training and certification—less technical roles benefit from the certification <u>as well</u>.

That's <u>the approach</u> we've <u>taken</u> for this book. The content is intended to help you understand the requirements of the AZ-900 Fundamentals exam and prepare to successfully pass the exam. The book does not go deep into Azure but <u>rather</u> focuses on core concepts, services, and resources in Azure that are <u>covered by</u> the exam **objectives**. The goal of the AZ-900 exam is not to give you a technical depth in Azure, but rather to give you a broad understanding that will enable you to understand the benefits that Azure offers and begin to <u>integrate</u> Azure <u>into</u> your role, whether technical or not.



**Vocabulary Extraction**

| Word/Phrase                    | English Definition                                                                    | 中文解释          | 词性                   |
| ------------------------------ | ------------------------------------------------------------------------------------- | ------------- | -------------------- |
| proactive                      | Acting in advance to prevent problems                                                 | 积极主动的         | adjective            |
| portfolio                      | A collection of investments or projects managed together                              | 投资组合；项目组合     | noun                 |
| on-premises                    | Located on the company's own property and infrastructure rather than in the cloud     | 本地部署的；内部部署的   | adjective            |
| make commitments               | To pledge or promise to do something; to dedicate oneself to a goal or responsibility | 做出承诺；承担责任     | verb phrase          |
| As part of that                | As one component or element of that thing; in connection with that                    | 作为其中的一部分      | prepositional phrase |
| take approach for              | To adopt or use a particular method or strategy for something                         | 采取某种方法        | verb phrase          |
| covered by                     | Included in or dealt with by something; under the scope of                            | 涵盖；包含在内       | verb phrase          |
| objectives                     | Goals or aims that one works to achieve                                               | 目标；目的         | noun                 |
| integrate Azure into your role | To incorporate or blend Azure services and tools into one's job responsibilities      | 将Azure融入你的工作中 | verb phrase          |

**Example sentences:**

- As part of that proactive strategy, we manage a portfolio of cloud migration projects for customers transitioning from on-premises to Azure.
- The certification objectives are covered by the exam, which helps you integrate Azure into your role and make commitments to continuous learning.
- We take approach for Azure deployment that enables teams to achieve their objectives effectively.

---

## Microsoft AZ-900 Certification Exam

Microsoft currently offers 17 **certifications** at many levels across the Azure cloud offering, ranging from fundamental to very technical. The AZ-900 exam and certification should be the first certification step in your Azure certification path if you do not yet have a fundamental understanding of cloud offerings and Azure <u>in particular</u>. So, whether you are interested in certification in Azure solutions, data, AI, or other areas, your certification path often <u>begins with</u> AZ-900.

The following section explores the certification paths and process <u>in more detail</u>.

### How Do You Become Certified in Azure?

As explained earlier, Microsoft currently offers 17 certifications for Azure. Obviously, fundamentals is one certification area, but there are multiple certification paths for Azure administration, app development, data, AI, security, DevOps, IoT, and Azure Stack. These certifications are currently supported by 39 exams. Even if you plan to pursue certification in, for example, Azure IoT development, you should consider AZ-900 Fundamentals to give you a broader understanding of Azure; the knowledge you gain will supplement your understanding of your selected certification. It will also help you leverage and integrate additional Azure workloads in your area of specialization.

Becoming certified in Azure is relatively simple. Choose the certification you want to achieve, work through the prescribed learning path for the certification, prepare for the exam, and pass it. Preparation can take many forms, and this book is intended to be your primary one. People have different learning styles, varying backgrounds and experiences, differing amounts of time to study, and so on. So, this book might be one of a handful of resources you use to prepare for the exam. To begin, work through the chapters of this book and develop a strong understanding
of the questions and answers offered in each one. Practice does make perfect, so consider working through additional practice test options before taking the exam. Microsoft offers some knowledge checks online within the content at the following URL: docs.microsoft.com/en-us/learn/certifications/azure-fundamentals

You will also find other sample test options online, some for free and some for a fee. All of them provide good additional preparation for the exam. The more questions you work through before taking the exam, the more likely you are to be successful on your first attempt.

## Types of Exam Questions

We have tried to model the sample questions in this book on the types of questions you will see in the official AZ-900 exam. Because the test is online, however, some types of questions are difficult to model in print. The following sections explore the types of questions you will experience in the official, online AZ-900 exam.

### Multiple Choice

These are generally straightforward and come in two variants. The first is a simple question followed by a selection of possible answers. The test question indicates whether there is a single answer or multiple correct answers. Each correct response counts toward your point total. Example (you would choose one answer):

1. Which one of the following provides container orchestration services for containers in Azure?
       A. Azure Container Instances (ACI)
       B.Azure Kubernetes
       C.Azure Logic Apps
       D. Azure Container Orchestration Services
   Many multiple-choice questions are scenario based, describing a planning, deployment, ormanagement scenario, followed by a question about the scenario. Example:

2. You are the IT director for Contoso Corporation. Your CIO has asked you to recommend asolution that will enable the development team to quickly deploy VMs for testing applications. The solution must provide flexibility but also result in the lowest cost. Which of the following solutions meets these requirements? (You would choose one or more correct solutions.)

### Drag-and-Drop and Select Questions

Drag-and-drop questions provide a list of answers that you must match with a corresponding description. For example, the answers might include Disaster Recovery, Fault Tolerance, Low Latency, and Dynamic Scalability. You would drag each of these answersinto a box beside the correct description of each. Select questions describe a scenario and you must choose the correct answer from a dropdown list that typically offers three possible answers. Example:

3. Which cloud deployment model is used for Azure VMs and Azure SQL Database instances?(You would choose Infrastructure-as-a-Service from a drop-down list beside Azure VMs and choose Platform-as-a-Service from the drop-down list beside Azure SQL Database.)

### Yes/No Questions

These questions typically include three questions related to a specific topic. You answer by selecting either Yes or No beside each one. Example (for each you would select either Yes or No):

4. Azure resources can access other resources only in the resource group in which theyreside. Yes No
   Deleting a resource group also deletes all resources in the group. Yes No
   A resource group can include resources from multiple Azure regions. Yes No

### Text Replacement Questions

These questions offer a statement with part of the statement underlined. The statements sometimes include leading sentences providing additional information. The question offers four options, A through D. Three offer alternative text that you would use in place of the underlined text to make it correct. Or, you choose the answer No change is needed if the underlined text is correct. Example:

5. Azure Data Lake Analytics is a PaaS solution that enables you to query data in a data lake and build visualizations without deploying hardware or supporting services.
   A. is built on SQL Managed Service to provide analytics for large SQL implementations.
   B.is a component of Azure IoT Central that provides deep analysis of IoT telemetry.
   C.integrates with Azure DevTest Labs to provide code analysis capabilities.
   D. No change is needed.

In this example, the underlined text makes the statement correct, so the appropriate answer is D (no change is needed). But, if Azure Data Lake Analytics were instead a component of Azure IoT that provided deep analysis of IoT telemetry (it is not), then you would choose B.
