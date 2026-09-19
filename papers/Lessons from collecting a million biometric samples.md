# Lessons from collecting a million biometric samples 

P. Jonathon Phillips ${ }^{\text {a,* }}$, Patrick J. Flynn ${ }^{\text {b }}$, Kevin W. Bowyer ${ }^{\text {b }}$<br>${ }^{\mathrm{a}}$ National Institute of Standards and Technology, 100 Bureau Drive MS 8490, Gaithersburg, MD 20899, USA<br>${ }^{\mathrm{b}}$ Computer Science and Engineering University of Notre Dame Notre Dame, IN 46556, USA

## ARTICLE INFO

Article history:
Received 18 October 2015
Received in revised form 11 August 2016
Accepted 16 August 2016
Available online 25 August 2016

Keywords:
Face recognition
Algorithm performance
Human performance
Challenge problem


#### Abstract

Over the past decade, independent evaluations have become commonplace in many areas of experimental computer science, including face and gesture recognition. A key attribute of many successful independent evaluations is a curated data set. Desired aspects associated with these data sets include appropriateness to the experimental design, a corpus size large enough to allow statistically rigorous characterization of results, and the availability of comprehensive metadata that allow inferences to be made on various data set attributes. In this paper, we review a ten-year biometric sampling effort that enabled the creation of several key biometrics challenge problems. We summarize the design and execution of data collections, identify key challenges, and convey some lessons learned.


© 2016 Elsevier B.V. All rights reserved.

## 1. Introduction

The creation of designed and curated data sets for grand challenges and independent evaluations has been an important driving force behind progress in biometrics over the last two decades [1-9]. Data sets distributed to the research community foster the development of new algorithms and technologies, and they allow independent evaluations of the state-of-the-art. Data sets also contribute to the identification of future research directions, especially if the data is available to the research community with minimal restrictions on its use. This paper describes a decade-long data collection effort that collected approximately 1 million biometric samples. The biometrics data collected supported seminal grand challenges in still and 3D face recognition and iris recognition that were key steps in fielding face and iris recognition systems.

Much of the collected data is available by license to the research community, and some data set components have been downloaded hundreds of times. The collection team continues to receive many requests per month. These data sets can serve as an "on-ramp" for new research groups entering the field. Since data sets are associated with experimental designs, new algorithms can be evaluated in a context that is well established and considered canonical by

[^0]the research community. However, research groups can also identify new biometrics problems by examining data sets and experimental results using them.

The focus of this paper is the design and execution of biometric data collection. Our goals are: (i) to provide guidance to prospective collectors; (ii) to highlight the key challenges that arise when planning and executing such an activity; and (iii) to highlight the research advances that resulted from our work.

## 2. Motivation

Before telling a story of sustained large-scale data collection and curated data set assembly, we provide the motivation for undertaking this task and highlight the key issue of metadata collection and management.

The notion of replicability is foundational to almost every field that employs experimental/empirical research. Scholarly communities tend to prize research that is disseminated in papers with a level of detail sufficient to enable replication, with confidence that the follow-on experiments are faithful copies of the original experiment. Conversely, research papers that omit key experimental details or provide vague descriptions that allow multiple interpretations are not as highly prized. We consider the organized collection of data using an explicit plan, followed by comprehensive curation efforts, followed by distribution to the teams conducting experiments, culminating in public release of results and licensed distribution of data, as a gold standard for management of experimental data.

The broad usefulness of a data set is strongly dependent on the amount, type, and quality of metadata accompanying the data itself. In the context of biometrics experiments, the most important item of metadata is the identity tag. Other items of metadata in common use for face recognition include gender, age, appearance characteristics (e.g., hair color, eye color), face pose, expression, light sources in use, and others. Metadata management and, in particular, error detection/correction are key challenges in data collection at scale, as metadata errors are unavoidable in most circumstances.

## 3. Related biometric data collections

The Face Recognition Technology (FERET) evaluation [1,10] was the first significant effort in face recognition to distribute a common data set along with an established standard protocol. Since then a variety of data sets, competitions, evaluations, and challenge problems have contributed to the face recognition field. Here we highlight a few.

The Carnegie Mellon University (CMU) Pose Illumination and Expression (PIE) face database [11] was collected in such a way as to support excellent empirical explorations of controlled interactions between illumination and pose. The Extended Multimodal Face Database (XM2VTS) and Banca Databases [12] were each released with associated evaluation protocols and competitions were organized around each [13,14]. The European BioSecure project represents a major coordinated effort to advance multi-modal biometrics, including face [15].

The Labeled Faces in the Wild (LFW) data set consists of images downloaded from the web, along with a website that curates current performance results [16]. The YouTube ${ }^{1}$ Faces data set consists of videos of people collected in the spirit of LFW [17].

A number of iris image data sets are available from research groups across the world. The Institute for Automation at the Chinese Academy of Sciences (CASIA) distributes the CASIA-IRIS-V4 data set ${ }^{2}$. The components of this data set include iris-at-a-distance images, handheld sensor images, images acquired using a novel illuminator design, and synthetic iris images.

The University of Beira Interior Iris (UBIRIS) database consists of two distinctive data sets containing noisy images of the iris captured in the visible wavelengths [18]. Smart Sensors, a United Kingdom corporation, distributes a set of near infrared (NIR)-illuminated iris images collected with a high quality sensor ${ }^{3}$.

## 4. Overview of data collection

For convenience, we will discuss our data collection activities as a set of three epochs, each of which aligns roughly to a group of U.S. Government sponsored evaluation activities. The first epoch is from 2002 through 2006; the data collected in this period supported the Face Recognition Grand Challenge (FRGC) in 2004, Face Recognition Vendor Test (FRVT) 2006, and Iris Challenge Evaluations (ICE) 2005 and 2006 [4-6]. The second epoch ran from 2007 through 2010 and included the Multiple Biometrics Grand Challenge (MBGC) in 2008 [7] and the Multiple Biometric Evaluation (MBE) 2010 [19]. The third epoch ran from 2010 through 2012, and data collected in this period supported the Intelligence Advanced Research Projects Activity's (IARPA) Biometrics Exploitation Science and Technology (BEST)

[^1]Program; data from this epoch also supported the Point and Shoot Face Recognition Challenge (PaSC) in 2013 [9,20].

This decade long effort collected data from nine individual modalities (excluding a few modalities from boutique collections). The overall collection protocol was organized by academic year or semester, during which it changed minimally if at all. During a semester or academic year, the same core biometric modalities were collected. The stability of the core modalities collected resulted in multi-modal biometric collections, including identity-linked multimodal collections.

Subjects were generally allowed to participate in the data collection once in each week of data collection operations. Each week of acquisition was considered a session of collection, and the biometric samples of a subject collected in his or her weekly appearance are referred to as a subject session. Upon reporting to the collection site, a subject would proceed through a set of stations. At each station, a set of biometric samples were collected. For example, a session could consist of four stations, the first collecting three-dimensional (3D) scans of the face, the second collecting iris images, the third collecting still images of the face in a studio environment, and the fourth station collecting face and body imagery (video and stills) outdoors. The number of stations and the set of biometric samples collected at each station varied over the decade but was fixed within a semester of collection. A set of biometric samples from a person is considered to be multi-modal if all the samples were collected in the same session. A collection is multi-modal if all the subject sessions are multi-modal and each subject session has samples of the same modes.

With the exception of one small collection, all still images and videos in the visible spectrum were taken with consumer cameras. The 3D face images consist of both range and texture images and the iris images were collected in the NIR. The nine modalities collected are

- still images of the face,
- still images of the face and body,
- videos of the face and body,
- 3D scans of the face,
- long wave infrared (thermal) imagery of the face,
- iris images collected with an iris sensor designed for cooperative subjects,
- iris images as people walked through a portal or following a walk, stop, and walk protocol (referred to as iris at a distance),
- still images with a profile view of the face and ear, and
- 3D scans that contained the ear and a profile image of the face.

The three epochs resulted in three large multi-modal collections. The modes in each of the multi-modal collections are

- still face, 3D face, and iris (FRGC/FRVT/ICE),
- still face, video face and body, iris, and iris at a distance (MBGC), and
- still face, still face and body, video face and body, iris, and iris at a distance (BEST).

Acronyms in parentheses identify the U.S. Government efforts that each multi-modal collection supported.

There is one special collection that does not neatly fit into the modality nomenclature, which is the Twins data set. The Twins data set was acquired at the Twins Days Festivals in Twinsburg, Ohio in 2009 and 2010. The twins data set contains both face and iris images and a small collection of 3D face scans.

Face imagery was collected under a diverse set of conditions. These conditions reflect the wide range of potential applications for automated face recognition. We modeled this range of applications

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-03.jpg?height=668&width=1422&top_left_y=198&top_left_x=306)
Fig. 1. An example of the types of images used in the FRGC and FRVT 2006 and the ICE 2005 and 2006. The two left frontal images in the top row were taken under controlled illumination with neutral and smiling expressions. The two left images in the bottom row were taken under uncontrolled illumination with neutral and smiling expressions. The two right images in the top row show the shape channel and texture channel pasted on the shape channel for a 3D facial image. The two right images in the bottom row show right and left iris images. All samples are from the multi-biometric dataset. Courtesy of Phillips et al. [6].

by five collection scenarios. In all conditions, both frontal and nonfrontal faces were collected. The scenarios are

- still images taken in a studio environment with a digital single lens reflex (DSLR) camera,
- still images taken under ambient lighting in hallways, atriums, and outdoors with a DSLR camera,
- still images taken under ambient lighting in hallways, atriums, and outdoors with handheld digital point and shoot cameras (e.g., cell phones),
- videos taken under ambient lighting in hallways, atriums, and outdoors with a tripod mounted video camera, and
- videos taken under ambient lighting in hallways, atriums, and outdoors with handheld digital point and shoot cameras.

Fig. 1 shows samples used in the FRGC, FRVT 2006, and ICE 2005 and 2006. Figs. 3 and 4 show samples from the MBGC. Figs. 5, 6, 7, and 8 show samples collected in the BEST epoch.

To answer specific questions or investigate special topics, we conducted smaller 'boutique' collections. One strength of maintaining the large collection infrastructure was that the marginal cost of collecting the boutique data sets was minimal.

Over the decade, we collected and enrolled in our data management system 986,246 samples, which do not include samples from a limited number of boutique collections. Therefore, the actual total number of samples collected was approximately 1 million. Fig. 2 breaks out number of biometric samples collected and enrolled in our data management system by academic year. From the start of the effort in 2002 through June 2005, we collected 284,401 samples. At the time this was the largest laboratory data collection activity by over an order of magnitude. From November 2010 through May 2012, 423,587 samples were collected. This data was collected three days a week for 20 weeks. On average 20,648 samples per week, 6882 per day, were collected. This increase in the number of biometric samples that could be collected and processed reflected improvements in our collection infrastructure. The infrastructure included management of hardware, software, and laboratory personnel.

The data set consists of biometric samples from 3145 subjects. The demographics of the subjects are females 49\% and males 51\%; the self declared race is Caucasian 77\%, Asian 14\%, and other or unknown 9\%. The majority of the subjects were undergraduate students.

One of the overarching design goals of the data collection effort was measuring the impact of time lapse between acquisitions. Because of the continual change in the student population, there are constraints on the size of longitudinal studies readily supported [21-23]. The longest time lapse between a subject's first and last acquisition was 3666 days (10 years). The mean time lapse was 266 days and the median was 87 days.

## 5. Purpose for data collection activities

The data collection effort was not a monolithic activity directed to a single long-term goal. The motivation and goals of the collection activities changed over time. The changes were driven by multiple factors.

- As research in biometrics continues, performance improves, performance goals increase, and the amount of data needed to estimate performance changes.
- As research in biometrics continues, knowledge of the conditions where techniques perform poorly becomes more detailed, sophisticated, and nuanced. As a result, data collection

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-03.jpg?height=610&width=599&top_left_y=1915&top_left_x=1185)
Fig. 2. Number of biometric samples collected broken out by academic year.

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-04.jpg?height=355&width=1226&top_left_y=196&top_left_x=439)
Fig. 3. Example of imagery collected as a subject walks through the portal. The image in (a) is a full 2000 by 2000 pixel NIR frame acquired by the IoM and (b) is the left ocular region from the frame in (a). There are approximately 120 pixels across the iris in (a) and (b). The images in (c) are three frames from a high definition video sequence of a subject walking through the portal. Courtesy of Phillips et al. [7].

plans can begin to target challenging conditions revealed by new experiments.
- Few research groups had any experience in large-scale biometric data collection in 2001, especially involving a large number of human subjects. As collection activity continued, a base of experience and mature supporting infrastructure was developed and led to a number of efficiencies in later years.
- Improvements in sensing, storage, distribution, and computation technology as well as process improvements allowed data collection scale to increase over time without a corresponding scale-up in personnel and cost.

The start-up or scale-up of a data collection activity followed a pattern that was executed many times over the years. The initial collection effort mounted in support of the FRGC and FRVT 2006 specified the collection of high-resolution facial images from 200 subjects once per week for an academic year, with repeat visits by the same subjects encouraged. The corresponding research study enabled by this collection was investigation of short-term time lapse effects on face recognition. Subsequent sponsor interest in 3D face scans and iris images triggered a sensor/vendor selection process, a protocol modification, and a pilot collection focused on sensor usability and post-collection data management workflow, to provide a base of experience for subsequent large-scale collections with the new sensors. By defining a process for collection operations changes, the amount and types of data collected, and types of sensors used, and the sophistication and capability of our data management system matured fairly smoothly over the years.

## 6. Organizing the data collection

Our team collected, processed, ground-truthed, and prepared for distribution an average of 100,000 biometric samples per year. Since the daily average collection load increased over the years of collection in response to programmatic commitments, we evolved the key resources needed to operate this collection activity without being overwhelmed by complexity and scale at its inception. These key resources include the following items.

At all times, there was a key person responsible for planning the collection, scheduling the collection events, procuring necessary sensors and supplies, delegating collection tasks, and verifying that post-collection activities were done, including the final delivery of data and packaging of data sets for distribution. A characteristic property of this role is the need for a person with strong organizational skills including management of many details and unanticipated matters. The key person in this role, and the exact scope of the role changed over the years: initially, one of the Notre Dame principal investigators (PIs) was the organizer. For a few years, a talented graduate student performed some of the tactical components of the role while a PI was responsible for more strategic elements of the impending collection. During the 2008-2012 collection interval, a broadly-skilled staff member was placed in charge of data collections, overseeing everything except initial collection design. This staff member was aided by a second staff member for the final two years of the project; this second person oversaw the ingestion of collected data into the Biometric Research Grid (BXGrid) system [24]. Our experience is that the choice of a good collection manager and the specification of very detailed and clear plans is the key to success of sustained large-scale data collection.

For all years of our large-scale collection activity, the collection venues were staffed primarily by students, usually undergraduates. There were many reasons for this initial design decision and our experiences have amply justified the choice. Undergraduates readily absorbed the necessary task-specific training (camera operation, use of the BXGrid system for ground truth recording, data subsetting for specific research tasks, etc.). We were able to employ some of our most talented undergraduates for multiple years in

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-04.jpg?height=435&width=1342&top_left_y=2063&top_left_x=377)
Fig. 4. Example frames from video sequences. The image in (a) is from a video sequence of a subject walking towards the cameras in an atrium and (b) is a subject performing a non-frontal activity outdoors.

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-05.jpg?height=1049&width=1570&top_left_y=196&top_left_x=230)
Fig. 5. Examples of images in the PaSC taken during four sessions. Note that locations were varied between sessions, while sensor, distance to camera and pose were varied within sessions. Courtesy of Beveridge et al. [9].

roles with increasing amounts of responsibility, providing continuity to operations. Some of these students initiated original research projects and some of those led to publications in the refereed literature.

Although the majority of our operators were undergraduates, we did assign some collection activity to graduate students from 2002 through 2008, considering it one of the mandatory duties of membership in the PIs' research group. However, as collection activity scaled up in its final years, we were confident in our ability to recruit a large number (approximately fifty) of undergraduates to assume all sensor operator roles, and graduate student labor was not needed except in exceptional circumstances.

Data management infrastructure, both software and hardware, is critical. Accurate collection of large data sets at scale is only possible if there are systems that support and facilitate the collection and curation workflow. The sophistication of such systems scales in some sense with the size and complexity of the data corpus. This was a hard-won lesson for the collection team. The initial days of collection employed a simplistic manual data management system with metadata stored in simple text files along with data organized in

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-05.jpg?height=566&width=1146&top_left_y=1904&top_left_x=444)
Fig. 6. Cropped face images extracted from still images in the PaSC. These images demonstrate some of the complications that arise in point-and-shoot images, lighting, motion blur and poor focus. Courtesy of Beveridge et al. [9].

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-06.jpg?height=648&width=1144&top_left_y=198&top_left_x=478)
Fig. 7. Four snapshots from one video showing a subject carrying out an action, in this case blowing bubbles. Courtesy of Beveridge et al. [9].

directories named for the collection date. A National Science Foundation (NSF) funded research project in large-scale data management systems led to the development of BXGrid [24], a database-backed and web-enabled data ingestion and management portal with redundant file storage affording robustness to disk and server failures. BXGrid is a key part of our ongoing research, as it allows subsets of our data corpus to be selected using database queries, which facilitates construction of targeted data sets for experiments.

One key to success in the large-scale data collections was conducting pilot studies and having a process for adding new sensors. Prior to starting large data collections, it is usually necessary to have a pilot data collection. The first stage in adding a new sensor is to conduct a pilot study to understand the sensor and the data it collects. After the initial pilot study, the sensor was integrated into an ongoing large-scale collection activity.

Collecting large amounts of data purely for the sake of collecting data will likely lead to wasted effort and resources. Design of a data collection needs to be motivated by a goal, or limited number of goals. Further, the goals need to be articulated in the experiment design.

Anecdotal evidence suggests that an initial raw labeling error rate of around 1 in 3000 can occur, and that incorporating an explicit data curation stage can reduce the labeling error rate to below 1 in 25,000. This was possible in our collection for four reasons. The first two concern the ability to detect suspected errors. The large number of samples per subject in each mode and results from multiple algorithms made it easy to detect suspected labeling errors. Third, there were researchers that examined every single sample and provided feedback when suspected errors were found. Fourth, the audit trail in the acquisition process made it possible to retrospectively confirm suspected errors.

In the U.S., collecting biometric samples for research needs review by an Institutional Review Board (IRB) for human subjects approval. There are issues beyond human subjects that include legal, ethical, copyright, and institutional risk. In evaluating these issues, it is good to remember the phrase "Just because it is legal, does not mean it is a good idea." In addition, human subjects, legal, and ethical standards vary by country. Before using data for an experiment, one needs to consider the following questions: Was the data collected with appropriate human subjects approval? Is the data allowed to be

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-06.jpg?height=668&width=1191&top_left_y=1837&top_left_x=454)
Fig. 8. Sampled portions of video frames from PaSC videos indicating some of the situations that make recognition challenging. Courtesy of Beveridge et al. [20].

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-07.jpg?height=877&width=1154&top_left_y=194&top_left_x=439)
Fig. 9. Examples of face-pairs of the same person from each of the GBU partitions: (a) good, (b) challenging, and (c) very challenging.

distributed? Is the use of the data consistent with the human subjects approval and consent form?

## 7. Accomplishments

### 7.1. Grand challenges and evaluations

The key novel accomplishments of the FRGC, FRVT 2006 and ICE 2005 and 2006 are:

- One key goal of the FRGC was an order-of-magnitude decrease in the error rate on frontal still face images taken under controlled illumination conditions over performance reported in the FRVT 2002 [3]. The FRVT 2006 documented that this goal was achieved [6].
- The FRGC and FRVT 2006 established the first independent performance benchmarks for 3D face recognition technology.
- The ICE 2005 and 2006 were the first grand challenge and independent evaluation for iris recognition matching technology.
- The FRVT 2006 and the ICE 2006 are the first technology evaluations that compared iris recognition, high-resolution still frontal face recognition, and 3D face recognition performance.
- The FRGC and FRVT 2006 were the first competitions that systematically compared human and machine face recognition performance.
- Results from the FRVT 2006 formed the basis for the Good, Bad, and Ugly challenge problem [8].

The goal of the MBGC was to improve the performance of face and iris recognition technology from biometric samples acquired under unconstrained conditions. The MBGC is organized into three challenge problems. Each challenge problem relaxes the acquisition constraints in different directions. The Portal Challenge focused on iris recognition on the move. The goal of the Still Face Challenge was to improve accuracy from frontal and off angle still face images taken in ambient lighting indoors and outdoors. In the Video Challenge, the goal was to recognize people from video in unconstrained environments. The data collected under the BEST program was the basis for the Point and Shoot Face Recognition Challenge (PaSC) [9]. Section 8.1.2 provides a more detail overview of the PaSC.

### 7.2. Scientific knowledge and technical advancement

The large and diverse data collection enabled scientific investigation into fundamental properties of biometrics. Below is a sampling of five key scientific discoveries that the data collections supported. Four additional scientific experiments are presented in Section 8.2 as case studies.

There are fundamental variations in face appearance in longwave infrared (LWIR) over time [25]. These variations are as prominent as region A being brighter than region B in an image taken at one time, but region A being darker than region B in another image of the same face taken at another time.

The twins data collected allowed for both face and iris recognition studies. For faces, when images are taken in mobile studios in the same collection session, it is possible to distinguish twins; however, when face images are taken a year apart, it is an extremely challenging problem [26]. Twins do have similarity of iris texture, but it is not a similarity that is seen in matching iris codes. This is one way in which iris codes are not the same as the texture of the iris [27].

In forensic comparison of iris images, humans can match iris images with substantial accuracy, though well below the accuracy on average and automated algorithms [28].

Starting with the FRGC, comparing human and algorithm performance has been systematically included into challenges and evaluations. These studies show that for frontal face images taken with DSLRs, algorithm performance is superior [29]. Human performance is superior when recognition requires fusing all identity cues present in an image or video [30,31]. In addition, fusing human and algorithm matching score improves performance [32]. The observation that algorithms developed by research groups in Asia are better at recognizing Asian faces and algorithms developed by groups
in the West are better at recognizing Caucasian faces has practical implications [33].

Quantifying the effect of factors, covariates, and quality measures on algorithm performance is essential for understanding biometric and face recognition algorithms. A series of covariate analyses of face recognition algorithms showed that simple measures can characterize algorithm performance on a data set [34,35]. Unfortunately, characterizations do not generalize to new algorithms and data sets. Phillips et al. [36] developed a technique for quantifying the existence of and the best case effectiveness of quality measures.

## 8. Case studies

To provide greater insight into the impact of this data collection, we provide brief summaries as six case studies. Two case studies are challenges and four are scientific results that were observed on this data collection.

### 8.1. Challenges

Challenge problems are difficult for two reasons. The majority of challenge problems are difficult because they introduce a new problem. The primary challenge is to develop new algorithms that solve the new problem. Examples are FRGC, LFW and PaSC. The second type is difficult because they characterize problems that are intrinsically hard. The GBU is in this class and studies on the GBU have provided new insights into face recognition precisely because it is intrinsically hard.

### 8.1.1. The Good, Bad, and \& Ugly challenge problem

To understand the range of performance under general illumination conditions, the GBU consists of three partitions that were created based on difficulty of matching ${ }^{4}$. To arrive at the performancebased partitions, three top-performing face recognition algorithms from the FRVT 2006 evaluation were fused to produce a single algorithm. Based on performance of the fusion algorithm, images were divided into three partitions with high (the Good), challenging (the Bad), and very challenging (the Ugly) accuracy. Fig. 9 shows three face-pairs of the same person, sampled from the good (left column), challenging (middle column), and very challenging (right column) performance strata. This figure illustrates the wide variation in the appearance of a person across frontal images. It also highlights the difficulties that may occur when recognizing faces that are taken in different environments that include variations in expression and appearance-based features such as hairstyle. These factors become even more salient in combination (cf., Fig. 9 right column).

In the GBU, the effects of natural variations in a person's dayto-day appearance (hair, facial expression, etc.) and variations in illumination across both indoor and outdoor environments were considered. All of these images were nominally frontal. Because all images were collected between August 2004 and May 2005, aging cannot be a factor. There are the same number of images of each person in all three partitions. Thus, only the images, not the individual identities, changed across the three partitions. This provides an assurance that the accuracy differences were due to factors other than the particular set of face identities tested.

On the Good partition, the base verification rate (VR) is 0.98 at a false accept rate (FAR) of 0.001. For the Bad partition, the VR was measured at 0.80 at a FAR of 0.001 , and on the Ugly partition the VR was measured at 0.15 at a FAR of 0.001 . In the peer reviewed literature, higher accuracy on the Ugly challenge has not been reported.

[^2]Human performance on the GBU is reported in O'Toole et al. [37], Rice et al. [30,38]. These papers looked at human performance for the original images, the interior of the face only, and with the interior face masked. The results show that human performance is best for the original image and human accuracy is highest on the Good partition, followed by the Bad and then the Ugly partitions. For all three partitions, algorithm performance is superior to untrained humans. Images from the GBU were incorporated into an experiment to measure the perceptual performance of facial forensic examiners [39]. The experiments showed that facial forensic examiners are better than untrained humans and the GBU baseline algorithm. The accuracy of humans was measured by the area under the ROC (AUC). For the Good partition, for humans the AUC was 0.96 and for algorithm the AUC was 0.99; for the Bad partitions the AUCs were 0.91 for humans and . 99 for algorithms; and for the Ugly partitions the AUCs were 0.89 for humans and . 94 for algorithms.

### 8.1.2. The point and shoot face recognition challenge

To spur advancement in face and person recognition the PaSC focuses on still images and video taken with handheld digital point and shoot cameras. The challenge includes 9376 still images of 293 people balanced with respect to distance to the camera, alternative sensors, frontal versus not-frontal views, and varying location. There are 2802 videos for 265 people: a subset of the 293. Videos were acquired at six locations, representing a mix of indoor and outdoor settings. Videos were acquired with both tripod and handheld video cameras. The handheld video portion consists of 1401 videos of 265 people acquired using five different handheld video cameras. A Pittsburgh Pattern Recognition (PittPatt) SDK 5.2.2-based face recognition algorithm provided baseline performance.

The PaSC was the bases for the Handheld Video Face and Person Recognition Competition held in conjunction with the International Joint Conference on Biometrics (IJCB) 2014 [20], and the Video Person Recognition Evaluation held in conjunction with the 11th IEEE International Conference on Automatic Face and Gesture Recognition (FG 2015) [40]. All participants in these competition submit raw results to the organizers for scoring and analysis.

Performance on the handheld video challenge is reported in Fig. 10. This includes performance for the PittPatt baseline algorithm, ICJB and FG 2015 competition, and result reported in the literature. The participants in the competitions were Chinese Academy of Sciences (CAS) [41], Stevens Institute of Technology (Stevens) [42,43],

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-08.jpg?height=584&width=823&top_left_y=1792&top_left_x=1107)
Fig. 10. Performance on the PaSC handheld video challenge from its release in 2013 through September 2015. The verification rate at a false accept rate (FAR) of 1 in 100 is reported. For performance with solid black bars, participants submitted raw scores to the PaSC organizers for scoring analysis. For the result with diagonal hashes, performance was reported in the literature. The date under the participant names is when the raw scores were submitted or results reported in the literature.

University of Ljubljana (Ljub) [44], and University of Technology, Sydney, (UTS) [45]. The results from IIIT-Delhi were reported outside the PaSC compeitions [46]. Human performance on the PaSC is reported in Phillips et al. [47].

### 8.2. Scientific results

The scientific case studies highlight progress in understanding iris recognition from experiments in three studies. The fourth study looks at methodologies for designing multi-sample and multibiometrics experiments.

### 8.2.1. Iris dilations

Hollingsworth, Bowyer, and Flynn [48] conducted an analysis of the impact of pupil dilation on iris matching performance. The unwrapping of the iris annulus to a standardized cylinder indexed by radius and angle involves interpolation and implicit subsampling and/or supersampling, depending on the radial and angular resolution of the cylindrical output. Intuition suggests that if undersampling dominates the transformation, then there is a risk of content loss, and thus accuracy impairment. To explore this question, a data set of 1263 images collected from 18 human subjects ( 36 irises) was collected. During the collection activity, room lights were extinguished for part of the time, to allow pupils to complete the reflexive dilation process associated with low light. The collection team's knowledge of the iris response and the proper configuration of facilities allowed this data set to be collected with minimal disruption. An alternative approach to forcing pupil dilation would involve the administration of penylephrine or cyclopentonate drops or both to the subjects. This was ruled out because of the elevated discomfort associated with eyedrop administration, the complexity of securing the medications, and the elevated level of scrutiny associated with this more invasive procedure.

Fig. 11 depicts the shift in genuine match score distributions for pairs of matching iris images with a difference in dilation ratio of [0, 0.1 )(red), [0.1, 0.2) (blue), and [0.2, 0.3) (green). The mode and mean of the distribution increases as the dilation difference increases. Since larger scores indicate a poorer degree of match, the conclusion is that dilation difference between the members of a match pair degrades the match score. In isolation, this would tend to drive up the false nonmatch rate of the system, which would potentially present a usability challenge. This result has since been replicated by various research groups.

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-09.jpg?height=704&width=864&top_left_y=1792&top_left_x=118)
Fig. 11. The effect of iris dilation on the match distribution. Courtesy of Hollingsworth, Bowyer, and Flynn [48].

### 8.2.2. Contact lenses

A large percentage of the population in the developed and developing world wears contact lenses of various types (e.g., rigid, rigid gas-permeable, soft, toric) to correct common vision defects such as myopia (nearsightedness), hyperopia (farsightedness), astigmatism, and the age-related inability to see close up (presbyopia) caused by increasing lens rigidity. Baker et al. [49] characterize the effect of refractive contact lenses on iris recognition performance. The iris data set at Notre Dame was searched to identify 12,003 images from 87 subjects wearing contact lenses and 9697 images from 124 subjects not wearing contact lenses. The images of irises with contact lenses were divided into four categories by appearance, ranging from soft lenses which manifest only as a boundary on the sclera, to rigid lenses, which generally cover only a portion of the iris and induce a noticeable refractive artifact into the iris texture. Given the relative stability of the impostor score distribution for iris images, the authors focused on the changes in the genuine score distribution for different types of contact lenses, along with a baseline "no lenses" comparison. The results are shown in Fig. 12, which reveals degradation from the baseline distribution for any type, and catastrophic degradation for category 4, which includes lenses that obscure or distort large amounts of the iris texture. These results suggested that iris based authentication of individuals wearing lenses of this latter type may suffer an elevated false reject rate, which presents a challenge to usability. Yadav [50] have also documented the effect of wearing contact lenses on iris recognition accuracy.

### 8.2.3. Multi-sample and multi-biometrics

Bowyer et al. [51] provide an overview of "multi-X" biometrics of various sorts, defining and explaining multisample, multi-algorithm, and various multimodal subtypes. The paper also motivates the need for properly collected, curated, and ground-truthed data sets to enable fair comparisons of various techniques. Fig. 13 provides a high-level overview of the "multimodal versus multisample" problem in biometric systems design. It illustrates a number of performance cases for 2D and 3D face recognition using data collected at Notre Dame: single-sample isolated-mode recognition rates (rank1 identification rate) were 90.9\% for 2D face and 88.9\% for 3D face; fusion of one 3D and one 3D yielded a recognition rate of 95\% and fusion of two 2D samples sample yielded 92.9\%; and fusion of four intensity samples yielded a rate of 96\%. The point of the illustration is not to definitively rule out a strategy, but to highlight the need to adequately explore the design space (e.g., number and type of cameras) when assessing performance and the suitability of a fusion strategy.

### 8.2.4. Iris template aging

Currently, one of the most debated topics in biometrics is iris template aging. Iris template aging occurs if the accuracy of iris recognition decreases as the amount of time between the acquisition of two iris images increases. One of the overarching design principles of the data collection was to collect samples of each subject at regular intervals during an academic year, which made it possible to conduct longitudinal studies in biometrics.

Baker et al. [52] was the first paper to study iris template aging and Baker et al. [21] ${ }^{5}$ repeated the study on state-of-the-art iris recognition algorithms. The experiment in Baker et al. [21] compared performance for a short- and long-time-lapses. The short-time-lapse was less than 6 months between acquisition for each iris; the long time lapse was greater than 1200 days (3.3 years). The iris images in the short and long were from the same people. The longest-timelapse was 3.9 years. The data set consisted of 6797 iris images from

[^3]![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-10.jpg?height=672&width=1126&top_left_y=192&top_left_x=485)
Fig. 12. The effect of contract lenses on the match distribution. Courtesy of Baker et al. [49].

23 subjects. To rule out other possible explanations for the observed the increase in FRR, the study controlled for pupil dilation, sensor aging, sensor illumination, contact lenses, and portion of the iris visible.

The study found no substantial difference in the non-match, or impostor, distribution between the short-time-lapse and the long-time-lapse data. Fig. 14 reports on the difference found for the match, or authentic, distributions. The effect of iris template aging is reported for Neurotechnology's VeriEye 2.2 Iris SDK, circa 2008, and the Cam-2 submission to the ICE 2006 from the University of Cambridge. The graphs show the false reject rate (FRR) as a function of the system threshold $\tau$. At a system threshold of $\tau=50$, the

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-10.jpg?height=1241&width=1103&top_left_y=1279&top_left_x=500)
Fig. 13. Illustrating the differences between multi-sample and multi-biometric fusion. Courtesy of Bowyer et al. [51].

![](https://cdn.mathpix.com/cropped/1049a707-2427-434f-9c99-e43795fa882d-11.jpg?height=696&width=1290&top_left_y=194&top_left_x=373)
Fig. 14. The effect of iris template aging for two algorithms: the Cam-2 submission to the ICE 2006 from the University of Cambridge and a VeriEye system, circa 2008. The graphs show the FRR (Rate on the graph) as a function of the system threshold $\tau$. Courtesy of Baker et al. [21].

FRR changes from 0.006 for short-time-lapse to 0.009 for long-timelapse; for Cam-2 at a $\tau=0.33$ changes from 0.014 to 0.021 (these thresholds roughly correspond to a FAR of 1 in 1000). This shows the FRR increases by about 50\% for the long-time-lapse data relative to the short-time-lapse data. The size of the increase in the FRR varies with changes in the decision threshold, and with different matching algorithms.

Since the publication of these two papers, a literature has emerged studying iris template aging [22,53-61]. Some of the papers reporting results that support an iris template aging effect and others claiming that an iris template aging effect does not exist.

## 9. Conclusion

By collecting a designed and curated data set of 1 million samples, we have enabled the advancement of both the technology and science of biometrics. The resulting understanding provides a solid basis for decisions on when and how to field biometric systems. The resulting datasets continue to be heavily used in research on still, video and 3D face recognition, and iris recognition.

## Acknowledgments

PJF and KWB received support from the following sources for 2002-2012 data collection activities: Defense Advanced Research Project Agency (DARPA), Air Force Office of Scientific Research (AFOSR), National Science Foundation (NSF), Technical Support Working Group (TSWG), Federal Bureau of Investigation (FBI), Intelligence Advanced Research Project Activity (IARPA), Army Research Laboratory (ARL), National Institute of Justice (NIJ), and the United States Government. PJP received support from the FBI and IARPA.

## References

[1] P.J. Phillips, H. Moon, S. Rizvi, P. Rauss, The FERET evaluation methodology for face-recognition algorithms, IEEE Trans. PAMI 22 (2000) 1090-1104.
[2] S. Sarkar, P.J. Phillips, Z. Liu, I. Robledo, P. Grother, K.W. Bowyer, The HumanID gait challenge problem: data sets, performance, and analysis, IEEE Trans. PAMI 27 (2005)
[3] P.J. Phillips, P.J. Grother, R.J. Micheals, D.M. Blackburn, E. Tabassi, J.M. Bone, Face Recognition Vendor Test 2002: Evaluation Report, Technical Report National Institute of Standards and Technology. 2003. Http://www.frvt.org NISTIR 6965.
[4] P.J. Phillips, P.J. Flynn, T. Scruggs, K.W. Bowyer, J. Chang, K. Hoffman, J. Marques, J. Min, W. Worek, Overview of the Face Recognition Grand Challenge, IEEE Computer Society Conference on Computer Vision and Pattern Recognition, 2005. pp. 947-954.
[5] P. Phillips, K.W. Bowyer, P.J. Flynn, X. Liu, W.T. Scruggs, The Iris Challenge Evaluation 2005, Second IEEE International Conference on Biometrics: Theory, Applications, and Systems, 2008.
[6] P.J. Phillips, W.T. Scruggs, A.J. O'Toole, P.J. Flynn, K.W. Bowyer, C.L. Schott, M. Sharpe, FRVT 2006 and ICE 2006 large-scale results, IEEE Trans. PAMI 32 (2010) 831-846.
[7] P.J. Phillips, P.J. Flynn, J.R. Beveridge, W.T. Scruggs, A.J. O'Toole, D. Bolme, K.W. Bowyer, B.A. Draper, G.H. Givens, Y.M. Lui, H. Sahibzada, J.A. Scallan, III, S. Weimer, Overview of the multiple biometrics grand challenge, Proceedings Third IAPR International Conference on Biometrics, 2009.
[8] P.J. Phillips, J.R. Beveridge, B.A. Draper, G. Givens, A.J. O'Toole, D.S. Bolme, J. Dunlop, Y.M. Lui, H. Sahibzada, S. Weimer, An introduction to the Good, the Bad, and the Ugly face recognition challenge problem, Proceedings Ninth IEEE International Conference on Automatic Face and Gesture Recognition, 2011.
[9] J. Beveridge, P. Phillips, D. Bolme, B. Draper, G. Givens, Y.M. Lui, M. Teli, H. Zhang, W. Scruggs, K. Bowyer, P. Flynn, S. Cheng, The challenge of face recognition from digital point-and-shoot cameras, Biometrics: Theory, Applications and Systems (BTAS), 2013 IEEE Sixth International Conference on, 2013.
[10] P.J. Phillips, H. Wechsler, J. Huang, P. Rauss, The FERET database and evaluation procedure for face-recognition algorithms, Image Vis. Comput. J. 16 (1998) 295-306.
[11] R. Gross, S. Baker, I. Matthews, T. Kanade, Face recognition across pose and illumination, in: S.Z. Li, A.K. Jain (Eds.), Handbook of Face Recognition, Springer-Verlag. 2004, pp. 193-216.
[12] E. Bailly-Bailliére, et al. The BANCA database and evaluation protocol., 4th International Conference on Audio- and Video-based Biometric Person Authentication, 2003. pp. 625-638.
[13] J. Matas, et al. Comparison of face verification results on the XM2VTS database, Proceedings of the International Conference on Pattern Recognition, volume 4, Barcelona, Spain,, 2000. pp. 4858-4853.
[14] K. Messer, et al. Face authentication test on the BANCA database, Proceedings of the International Conference on Pattern Recognition, 4, 2004. pp. 523-532.
[15] D. Petrovska-Delacretaz, G. Chollet, B. Dorizzi, Guide to Biometric Reference Systems and Performance Evaluation, Springer, Dordrecht, 2009.
[16] G. Huang, M. Ramesh, T. Berg, E. Learned Miller, Labeled faces in the wild: a database for studying face recognition in unconstrained environments, University of Massachusetts at Amherst. 2007, Technical Report Tech. Rep. 07-49.
[17] L. Wolf, T. Hassner, I. Maoz, Face recognition in unconstrained videos with matched background similarity, Computer Vision and Pattern Recognition (CVPR), 2011 IEEE Conference on, 2011. pp. 529-534.
[18] H. Proença, L.A. Alexandre, UBIRIS: a noisy iris image database, 13th International Conference on Image Analysis and Processing, 2005. pp. 970-977.
[19] P.J. Grother, G.W. Quinn, P.J. Phillips, MBE 2010: report on the evaluation of 2D still-image face recognition algorithms, National Institute of Standards and Technology. 2010, NISTIR 7709.
[20] J.R. Beveridge, H. Zhang, P. Flynn, Y. Lee, V.E. Liong, J. Lu, M. Angeloni, T. Pereira, H. Li, G. Hua, V. Struc, J. Krizaj, P.J. Phillips, The IJCB 2014 PaSC video face and person recognition competition, Proceedings of the International Joint Conference on Biometrics, 2014.

[21] S. Baker, K.W. Bowyer, P.J. Flynn, P.J. Phillips, Template aging in iris biometrics: evidence of increased false reject rate in ICE 2006, in: M. Burge, K.W. Bowyer (Eds.), Handbook of Iris Recognition, Springer-Verlag, New York, NY, USA, 2013, pp. 205-218.
[22] S.P. Fenker, E. Ortiz, K.W. Bowyer, Template aging phenomenon in iris recognition, IEEE Access 1 (2013)
[23] P.J. Flynn, K.W. Bowyer, P.J. Phillips, Assessment of time dependency in face recognition: an initial study, Audio-and Video-Based Biometric Person Authentication, 2003. pp. 44-51.
$[24]$ H. Bui, M. Kelly, C. Lyon, M. Pasquier, D. Thomas, P.J. Flynn, D. Thain, Experience with BXGrid: a data repository and computing grid for biometrics research, Clust. Comput. 12 (2008) 373-386.
[25] X. Chen, P.J. Flynn, K.W. Bowyer, Infra-red and visible-light face recognition, Comput. Vis. Image Underst. 99 (2005) 332-358.
[26] J. Paone, P. Flynn, P.J. Phillips, K. Bowyer, R. Vorder Bruegge, P. Grother, G. Quinn, M. Pruitt, J. Grant, Double trouble: differentiating identical twins by face recognition, IEEE Trans. Inf. Forensics Secur. 9 (2014) 285-295.
[27] P. J. .Flynn, K. Hollingsworth, K.W. Bowyer, S. Lagree, S.P. Fenker, Genetically identical irises have texture similarity that is not detected by iris biometrics, Comput. Vis. Image Underst. 115 (2011) 1493-1502.
[28] K. McGinn, S. Tarin, K.W. Bowyer, Identity verification using iris images: performance of human examiners, IEEE International Conference on Biometrics: Theory, Applications and Systems (BTAS 13), 2013. pp. "".
[29] P.J. Phillips, A.J. O'Toole, Comparison of human and computer performance across face recognition experiments, Image Vis. Comput. 32 (1) (2014) 74-85.
[30] A. Rice, P.J. Phillips, V. Natu, X. An, A.J. O'Toole, Unaware person recognition from the body when face identification fails, Psychol. Sci. 24 (2013) 2235-2243.
[31] A.J. O'Toole, P.J. Phillips, S. Weimer, D.A. Roark, J. Ayyad, R. Barwick, J. Dunlop, Recognizing people from dynamic and stable faces and bodies: dissecting identity with a fusion approach, Vis. Res. 51 (2011) 74-83.
[32] A. O'Toole, H. Abdi, F. Jiang, P.J. Phillips, Fusing face recognition algorithms and humans, IEEE Trans. Syst. Man Cybern. Part B 37 (2007) 1149-1155.
[33] P.J. Phillips, F. Jiang, A. Narvekar, A.J. O'Toole, An other-race effect for face recognition algorithms, ACM Trans. Appl. Perception 8 (2011)
[34] J.R. Beveridge, G.H. Givens, P.J. Phillips, B.A. Draper, Y.M. Lui, Focus on quality, predicting FRVT 2006 performance, Proceeding of the Eighth International Conference on Automatic Face and Gesture Recognition, 2008.
[35] G.H. Givens, J.R. Beveridge, P.J. Phillips, B.A. Draper, Y.M. Lui, D.S. Bolme, Introduction to face recognition and evaluation of algorithm performance, Comput. Stat. Data Anal. 67 (2013) 236-247.
[36] P.J. Phillips, J.R. Beveridge, D.S. Bolme, B.A. Draper, G.H. Given, Y.M. Lui, S. Cheng, M.N. Teli, H. Zhang, On the existence of face quality measures, IEEE Biometrics: Theory, Applications and Systems (BTAS), 2013.
[37] A.J. O'Toole, X. An, J. Dunlop, V. Natu, P.J. Phillips, Comparing face recognition algorithms to humans on challenging tasks, ACM Trans. Appl. Perception 9 (2012)
[38] A. Rice, P.J. Phillips, A.J. O'Toole, The role of the face and body in unfamiliar person identification, Appl. Cogn. Psychol. 27 (2013) 761-768.
[39] D. White, P.J. Phillips, C.A. Hahn, M.Q. Hill, A.J. O'Toole, Perceptual expertise in forensic facial image comparison, Proc. R. Soc. B 282 (2015)
[40] J.R. Beveridge, H. Zhang, B.A. Draper, P.J. Flynn, Z. Feng, P. Huber, J. Kittler, Z. Huang, S. Li, Y. Li, M. Kan, R. Wang, S. Shan, X. Chen, H. Li, G. Hua, V. Štruc, J. Križaj, C. Ding, D. Tao, P.J. Phillips, Report on the FG 2015 video person recognition evaluation, Proceedings Eleventh IEEE International Conference on Automatic Face and Gesture Recognition, 2015.
[41] Z. Huang, R. Wang, S. Shan, X. Chen, Hybrid Euclidean-and-Riemannian metric learning for image set classification, Proceedings of the 12th Asian Conference on Computer Vision, 2014.
[42] H. Li, G. Hua, Z. Lin, J. Brandt, J. Yang, Probabilistic elastic matching for pose variant face verification, Computer Vision and Pattern Recognition (CVPR), 2013 IEEE Conference on, IEEE. 2013, pp. 3499-3506.
[43] H. Li, G. Hua, X. Shen, Z. Lin, J. Brandt, Eigen-Pep for video face recognition, Proceedings of the 12th Asian Conference on Computer Vision (ACCV 2014), 2014.
[44] J.K.V. Štruc, S. Dobrišek, MODEST face recognition, Third International Workshop on Biometrics and Forensics, 2015.
[45] C. Ding, C. Xu, D. Tao, Multi-task pose-invariant face recognition, IEEE Trans. Image Process. (2015)
[46] G. Goswami, R. Bhardwaj, R. Singh, M. Vatsa, Mdlface: memorability augmented deep learning for video face recognition, Biometrics (IJCB), 2014 IEEE International Joint Conference on, IEEE. 2014,
[47] P.J. Phillips, M.Q. Hill, J.A. Swindle, A.J. O'Toole, Human and algorithm performance on the PaSC face recognition challenge, IEEE Conference on Biometrics: Theory, Applications and Systems, 2015.
[48] K. Hollingsworth, K.W. Bowyer, P.J. Flynn, Pupil dilation degrades iris biometric performance, Comput. Vis. Image Underst. 113 (2009) 150-157.
[49] S. Baker, A. Hentz, K.W. Bowyer, P.J. Flynn, Degradation of iris recognition performance due to non-cosmetic prescription contact lenses, Comput. Vis. Image Underst. 14 (2010) 1030-1044.
[50] D. Yadav, N. Kohli, J.S. Doyle, R. Singh, M. Vatsa, K.W. Bowyer, Unraveling the effect of textured contact lenses on iris recognition, IEEE Trans. Inf. Forensics Secur. 9 (2014) 851-862.
[51] K.W. Bowyer, K.I. Chang, P. Yan, P.J. Flynn, E. Hansley, S. Sarkar, Multi-modal biometrics: an overview, Proceedings of Second Workshop on Multimodal User Authentication, 2006.
[52] S. Baker, K.W. Bowyer, P.J. Flynn, Empirical evidence for correct iris match score degradation with increased time-lapse between gallery and probe matches, Proc. International Conference on Biometrics, 2009. pp. 1170-1179.
[53] K.W. Bowyer, E. Ortiz, Making sense of the IREX VI Report, Technical Report U of Notre Dame, Computer Vision Research Lab. 2013.
[54] A. Czajka, Template ageing in iris recognition, BioSignals, 2013.
[55] E. Ellavarason, C. Rathgeb, Template ageing in iris biometrics: an investigation of the ND-iris-template-ageing-2008-2010 database, Technical Report Biometrics and Internet-Security Research Group, Center for Advanced Security Research, Darmstadt, Germany, 2013. HDA-da/sec-2013-001.
[56] S.P. Fenker, K.W. Bowyer, Experimental evidence of a template aging effect in iris biometrics, Proc. IEEE Computer Society Workshop on Applied Computer Vision, 2011. pp. 232-239.
[57] S.P. Fenker, K.W. Bowyer, Analysis of template aging in iris biometrics, Proc. IEEE Computer Society Workshop on Biometrics, 2012. pp. 45-51.
[58] P. Grother, J.R. Matey, E. Tabassi, G.W. Quinn, M. Chumakov, IREX VI: temporal stability of iris recognition accuracy, NIST Interagency Report National Institute of Standards and Technology. 2013. 7948.
[59] H. Mehrotra, M. Vatsa, R. Singh, B. Majhi, Does iris change over time? PLoS ONE 8 (2013) e78333.
[60] N. Sazonova, F. Hua, X. Liu, J. Remus, A. Ross, L. Hornak, S. Schuckers, A study on quality-adjusted impact of time lapse on iris recognition, Proc. SPIE, 8371, 2012. 83711W-1-83711W-9.
[61] E. Ortiz, K.W. Bowyer, Exploratory analysis of an operational iris recognition dataset from a CBSA border-crossing application, The IEEE Conference on Computer Vision and Pattern Recognition (CVPR) Workshops, 2015.

[^0]:    This paper has been recommended for acceptance by Vitomir Štruc.

    * Corresponding author.
    E-mail addresses: jonathon@nist.gov (P.J. Phillips), flynn@nd.edu (P. Flynn), kwd@cse.nd.edu (K. Bowyer).

[^1]:    ${ }^{1}$ The identification of any commercial product or trade name does not imply endorsement or recommendation by NIST.
    ${ }^{2}$ http://www.cbsr.ia.ac.cn/china/Iris\%20Databases\%20CH.asp
    ${ }^{3}$ http://www.smartsensors.co.uk/products/iris-database/

[^2]:    ${ }^{4}$ An overview of the creation of the GBU partitions is presented in this section, details are given in Phillips et al. [8].

[^3]:    ${ }^{5}$ Earlier versions of Baker et al. [21] appeared as NISTIR 7630 in September 2009 and NISTIR 7752 in March 2011.

