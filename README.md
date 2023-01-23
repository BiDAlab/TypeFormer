# TypeFormer: Transformers for Mobile Keystroke Biometrics

Welcome! 

In this page we provide all the necessary information to replicate the experimental protocol of the benchmark evaluation of TypeFormer, a novel Transformer-based mobile keystroke verification system proposed in [\[1\]](https://arxiv.org/abs/2212.13075). The model development and evaluation described is carried out over the Aalto Mobile Keystroke Database [\[2\]](https://userinterfaces.aalto.fi/typing37k/resources/Mobile_typing_study.pdf). 
The followed experimental protocol is also adopted in [\[3\]](https://arxiv.org/abs/2212.13075), [\[4\]](https://ieeexplore.ieee.org/document/9539873). 


# Introductory Description of the Raw Data

The database is available for download [here](https://userinterfaces.aalto.fi/typing37k/). We selected the following option for download:

"-	CSV versions of the raw and processed data as a .zip file (5.6GB zipped)."

In the .zip file downloaded, we have considered the files “keystrokes.csv” and “test_sections.csv” inside the “Data_Raw” folder:
-	“keystrokes.csv” contains each single key pressed included in the database, linking it to the specific acquisition session through the ‘TEST_SECTION_ID’ field.
-	“test_sections.csv” contains information about each single acquisition session in the database, linking it to the specific subject through the ‘PARTICIPANT_ID’ field.


# Benchmark Evaluation of TypeFormer

We analyse the performance of TypeFormer over an evaluation set of *U* = 1000 subjects unseen in the training and validation phases. The metric chosen for evaluation is the Equal Error Rate (EER). 

We consider a fixed number of 15 acquisition sessions per subject. Out of these, we use a variable number of enrolment sessions (*E* = 1, 2, 5, 7, 10) in order to assess the performance adaptation of the system to reduced availability of enrolment data. Additionally, also the experiments are repeated changing the input sequence length, *L* = 30, 50, 70, 100, to evaluate the optimal keystroke sequence length.

The table below reports the results obtained by TypeFormer in comparison with two recently proposed keystroke verification studies. In [\[3\]](https://arxiv.org/abs/2212.13075), a different Transformer-based architecture was proposed as a preliminary version of the current work. In [\[4\]](https://ieeexplore.ieee.org/document/9539873), TypeNet, a Long Short Term Memory Recurrent Neural Network, was proposed.

The results contained in the table are expressed in terms of EER (%), and obtained according to the same experimental protocol, data subjects, and data acquisition sessions (corresponding to Table 2 in [\[1\]](https://arxiv.org/abs/2212.13075)). 

| Sequence Lenght *L* | Model | *E* = 1 | *E* = 2 | *E* = 5 | *E* = 7 | *E* = 10 |
| ---| --- | --- | --- | --- | --- | --- |
| 30 | TypeNet [\[4\]](https://ieeexplore.ieee.org/document/9539873) | 14.20 | 12.50 | 11.30 | 10.90 | 10.50 |
| 30 | **TypeFormer** [\[1\]](https://arxiv.org/abs/2212.13075) | **9.48** | **7.48** | **5.78** | **5.40** | **4.94** |
| 50 | TypeNet [\[4\]](https://ieeexplore.ieee.org/document/9539873) | 12.60 | 10.70 | 9.20 | 8.50 | 8.00 |
| 50 | Preliminary Transformer [\[3\]](https://arxiv.org/abs/2212.13075) | 6.99 | - | 3.84 | - | 3.15 |
| 50 | **TypeFormer** [\[1\]](https://arxiv.org/abs/2212.13075) | **6.17** | **4.57** | **3.25** | **2.86** | **2.54** |
| 70 | TypeNet [\[4\]](https://ieeexplore.ieee.org/document/9539873) | 11.30 | 9.50 | 7.80 | 7.20 | 6.80 |
| 70 | **TypeFormer** [\[1\]](https://arxiv.org/abs/2212.13075) | **6.44** | **5.08** | **3.72** | **3.30** | **2.96** |
| 100 | TypeNet [\[4\]](https://ieeexplore.ieee.org/document/9539873) | 10.70 | 8.90 | 7.30 | 6.60 | 6.30 |
| 100 | **TypeFormer** [\[1\]](https://arxiv.org/abs/2212.13075) | **8.00** | **6.29** | **4.79** | **4.40** | **3.90** |


# Experimental Protocol
The genuine and impostor score distributions are subject-specific. 

For each subject, genuine scores are obtained comparing the number enrolment sessions (*E*) with 5 verification sessions. The Euclidean distances are computed for each of the verification sessions with each of the *E* enrolment sessions, and then values are averaged over the enrolment sessions. Therefore, for each subject there are 5 genuine scores, one for each verification session. 

Concerning the impostor score distribution, for every other subject in the evaluation set, the averaged Euclidean distance value is obtained considering 1 verification session and the above-mentioned 5 enrolment sessions. Consequently, for each subject, there are 999 impostor scores. Based on such distributions, the EER score is calculated per subject, and all EER values are averaged across the entire evaluation set. 

# Data Subjects and Data Acquisition Sessions Used for Evaluation

For each subject, the enrolment sessions are the chosen in a orderly fashion from the first 10 sessions. For *E* = 1, the enrolment session chosen will be the first one. For *E* = 2, the enrolment sessions will be the first two, and so on. The verification sessions selected are always the last 5 sessions out of the 15 sessions per subject considered. 

All data sessions used for evaluation, separated by subject, are reported in the file section of this repository.


# References

[\[1\] *Giuseppe Stragapede, Paula Delgado-Santos, Ruben Tolosana, Ruben Vera-Rodriguez, Richard Guest, and Aythami Morales, “TypeFormer: Transformers for Mobile Keystroke Biometrics”, arXiv:2207.07596, 2023.*](https://arxiv.org/abs/2212.13075)

[\[2\] *Kseniia Palin, Anna Feit, Sunjun Kim, Per Ola Kristensson, and Antti Oulasvirta, "How do people type on mobile devices? Observations from a study with 37,000 volunteers", Proc. of the 21st
Int. Conf. on Human-Computer Interaction with Mobile Devices and Services, 2019.*](https://userinterfaces.aalto.fi/typing37k/resources/Mobile_typing_study.pdf)

[\[3\] *Giuseppe Stragapede, Paula Delgado-Santos, Ruben Tolosana, Ruben Vera-Rodriguez, Richard Guest, and Aythami Morales, “Mobile Keystroke Biometrics Using Transformers”, Proc. of the Int. Conf. on Face and Gesture Recognition (FG), 2023.*](https://arxiv.org/abs/2212.13075) 

[\[4\] *Alejandro Acien, Aythami Morales, John V. Monaco, Ruben Vera-Rodriguez, and Julian Fierrez, "TypeNet: Deep learning keystroke biometrics." IEEE Transactions on Biometrics, Behavior, and Identity Science (TBIOM), 4.1 (2021): 57-70, 2021.*](https://ieeexplore.ieee.org/document/9539873)




**Contact: [giuseppe.stragapede@uam.es](mailto:giuseppe.stragapede@uam.es)**
