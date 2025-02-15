---
title: 'An empirical study of testing machine learning in the wild'
authors: ["Moses Openja", "Foutse Khomh", "Armstrong Foundjem", "Zhen Ming", "Mouna Abidi", "Ahmed E Hassan"]
date: 2024-01-01
publishDate: 2025-02-12T17:08:56.579551Z
publication_types: ['2'] #article-journal
publication: '*ACM Transactions on Software Engineering and Methodology*'
featured: true
abstract: "Background: Recently, machine and deep learning (ML/DL) algorithms have been increasingly adopted in many software systems. Due to their inductive nature, ensuring the quality of these systems remains a significant challenge for the research community. Traditionally, software systems were constructed deductively, by writing explicit rules that govern the behavior of the system as program code. However, ML/DL systems infer rules from training data i.e., they are generated inductively. Recent research in ML/DL quality assurance has adapted concepts from traditional software testing, such as mutation testing, to improve reliability. However, it is unclear if these proposed testing techniques are adopted in practice, or if new testing strategies have emerged from real-world ML deployments. There is little empirical evidence about the testing strategies.
Aims: To fill this gap, we perform the first fine-grained empirical study on ML testing in the wild to identify the ML properties being tested, the testing strategies, and their implementation throughout the ML workflow.
Method: We conducted a mixed-methods study to understand ML software testing practices. We analyzed test files and cases from 11 open-source ML/DL projects on GitHub. Using open coding, we manually examined the testing strategies, tested ML properties, and implemented testing methods to understand their practical application in building and releasing ML/DL software systems.
Results: Our findings reveal several key insights: (1) The most common testing strategies, accounting for less than 40%, are Grey-box and White-box methods, such as Negative Testing, Oracle Approximation, and Statistical Testing. (2) A wide range of
ML properties are tested, out of which only 20% to 30% are frequently tested, including Consistency, Correctness, and Efficiency. (3) Bias and Fairness is more tested in Recommendation (6%) and Computer Vision (CV) (3.9%) systems, while Security and Privacy is tested in CV (2%), Application Platforms (0.9%), and NLP (0.5%). (4) We identified 13 types of testing methods, such as Unit Testing, Input Testing, and Model Testing.
Conclusions: This study sheds light on the current adoption of software testing techniques and highlights gaps and limitations in existing ML testing practices."
url_pdf: "https://arxiv.org/pdf/2312.12604"
links: 
- name: Online Appendix
  url: "https://dl.acm.org/doi/10.1145/3680463"
---
