# On the Reliability of Biometric Datasets: How Much Test Data Ensures Reliability? 

Matin Fallahi ${ }^{1}$, Ragini Ramesh ${ }^{2}$, Pankaja Priya Ramasamy ${ }^{2}$, Patricia Arias Cabarcos ${ }^{1,2}$, Thorsten Strufe ${ }^{1}$, Philipp Terhörst ${ }^{2}$<br>${ }^{1}$ KASTEL Security Research Labs - KIT, Karlsruhe, Germany<br>${ }^{2}$ University of Paderborn, Paderborn, Germany


#### Abstract

Biometric authentication is increasingly popular for its convenience and accuracy. However, while recent advancements focus on reducing errors and expanding modalities, the reliability of reported performance metrics often remains overlooked. Understanding reliability is critical, as it communicates how accurately reported error rates represent a system's actual performance, considering the uncertainty in error-rate estimates from test data. Currently, there is no widely accepted standard for reporting these uncertainties and indeed biometric studies rarely provide reliability estimates, limiting comparability and interpretation. To address this gap, we introduce BioQuake-a measure to estimate uncertainty in biometric verification systems-and empirically validate it on four systems and three datasets. Based on BioQuake, we provide simple guidelines for estimating performance uncertainty and facilitating reliable reporting. Additionally, we apply BioQuake to analyze biometric recognition performance on 62 biometric datasets used in research across eight modalities: face, fingerprint, gait, iris, keystroke, eye movement, Electroencephalogram (EEG), and Electrocardiogram (ECG). Our analysis shows that reported state-of-the-art performance often deviates significantly from actual error rates, potentially leading to inaccurate conclusions. To support researchers and foster the development of more reliable biometric systems and datasets, we release BioQuake as an easy-to-use web tool for reliability calculations.


Index Terms-Biometrics, Biometric Recognition, Uncertainty Quantification, Reliability

## I. Introduction

Biometric verification allows for the automatic verification of a person's identity based on their biological (e.g., face, fingerprint) or behavioral characteristics (e.g., keystroke dynamics) [1]. This type of user authentication plays a key role in providing secure access to our devices, as well as to the many physical and digital environments we navigate daily [2]. Indeed, rapid advances in the accuracy and processing speed of biometric systems have facilitated their widespread adoption across a range of high-security applications, such as border control, forensics, and financial transactions, as well as their integration into smartphones and other consumer devices. This trend is expected to grow building on the increased research in the area. State-of-the-art literature is intensive on exploring new, potentially more usable and robust, biometric modalities [3]-[8] that can be incorporated in current systems or tailored to emerging technology, such as extended reality [9], [10]. Another branch of research focuses on improving the performance of well-established biometrics in different environmental conditions [11]-[15].

Whether developing new biometric systems or improving existing techniques, there is a critical need for comprehensive and reliable testing. However, most of the proposed solutions are tested on small datasets and/or provide insufficient information about performance and reliability of the reported results [16]. These issues hinder rapid advance in biometric research, as it is not clear how to compare the performance of different systems to verify if there is a true improvement. To better understand the problem, let's examine the common reporting practice. Since biometric matching is probabilistic, the ISO standard on "Biometric performance testing and reporting" [17] recommends using error rates: (1) for incorrect matches where impostors are identified as genuine users (False Match Rate, FMR), and (2) for incorrect rejections where genuine users are identified as impostors (False NonMatch Rate, FNMR). Although insightful, these metrics do not account for how closely the observed error rates reflect true error rates, due to testing data limitations (e.g., insufficient size or diversity). For example, take two systems that report the same False Match Rate (FMR) of $0.1 \%$. If one system consistently performs near this rate while the other fluctuates significantly, the latter could pose major security risks. This is because such variability increases the likelihood of unexpected impostor acceptances.

Uncertainty estimations are needed to quantify how much the observed error rate might deviate from the true one, and should be reported for a more accurate representation of the results [18], [19]. Several studies [20]-[24] provided approaches to quantify the relationship between uncertainty and biometric verification performance (§ II). However, these works have two main limitations. First, they rely on strong assumptions about the data, such as that the samples follow a normal distribution and are uniform across subjects, which may not hold in real-world scenarios. Second, these methods are challenging to implement in practice due to their complexity and the need for specialized statistical expertise, making them less accessible for practical application. Indeed, despite these uncertainty quantification approaches exist, biometric research very rarely reports uncertainties. In this paper, we bridge these gaps through the following contributions:

1) We formalize BioQuake ${ }^{1}$, a new uncertainty metric

[^0]

for biometric systems. BioQuake (§ III-A) describes how much the true error rate might deviate from the observed error (FMR, FNMR), given a specified confidence level and the number of genuine/impostor comparisons. To validate the metric, we conduct experiments on three biometric datasets for face recognition [25]-[27], each containing over ten thousand images. These datasets are frequently used in state-of-the-art research and were captured under varying conditions. We apply four face recognition systems to these datasets and demonstrate that BioQuake is an accurate estimator of empirical uncertainty by measuring the correlation between empirical measurements and theoretical uncertainty (§ IV-A, § V-A). BioQuake treats sample-pairs as independent and identically distributed and models uncertainty using a binomial distribution of these pairs, which is less restrictive than existing metrics that assume a normal distribution of the individual samples. While its accuracy may be influenced by factors such as a small number of subjects relative to the total samples, or an uneven distribution of samples among subjects, BioQuake provides a reliable lower bound on uncertainty. We further discuss these considerations and its applicability in real-world scenarios in § VI.
2) We introduce easy-to-apply uncertainty estimation rules and a user-friendly calculation tool. Based on the theoretical definition of BioQuake, we derive three heuristics that are helpful for conveniently estimating the uncertainty of a biometric system's performance or the number of comparisons needed to achieve a specific reliability (§ III-C). These rules are derived for a confidence level of 95\% and ensure that the true error only deviates by either 1\%, 6\%, or 10\%. Additionally, we implemetned and released an online too. ${ }^{2}$ to conveniently calculate biometric uncertainty beyond the heuristic cases, based on BioQuake. With these tools, we aim at promoting widespread use of uncertainty reporting and thus, comparable research.
3) We conduct a comprehensive analysis of the uncertainty in biometric research. (§ IV-B. § V-B.) We analyzed the uncertainty in the reported performance of state-of-the-art biometric solutions across 62 biometric datasets spanning 8 modalities (face, fingerprint, gait, iris, keystroke, eye movement, EEG, ECG). Our findings show that the performance of many systems might significantly deviate from actual results, highlighting the urgency of reporting error uncertainties in biometric research.


## II. Related Work

In biometric recognition, research results are commonly reported either solely by error rates [3], [5], [28], [29] or, occasionally, including the standard error to indicate variations [6], [7]. However, confidence intervals ensure a more reliable quantification of performance. For error rates, a confidence interval provides an error range that likely contains the true

[^1] error with a specific probability. Therefore, the size of the confidence range reflects the uncertainty given a predefined confidence level. Despite the importance of uncertainty estimation, the process of calculating confidence intervals can be challenging [18], and reporting uncertainty is rarely considered a mandatory step for publishing research in biometrics.

## A. Confidence Estimation For Biometric Recognition

Approximating confidence intervals is typically achieved through two main approaches: Distribution-based methods [30], [31] and the Bootstrap method [32], [33]. Distribution-based methods require assumptions about the data, such as sample size, population variance (known or unknown), or the underlying distribution. In contrast, the Bootstrap method is a computational technique that operates without these assumptions. It estimates confidence intervals by repeatedly sampling from the data with replacement, facilitating the direct calculation of intervals from the sample itself. Although not as robust as distribution-based methods, the Bootstrap method is often advantageous when the data distribution is unknown and computational overhead is negligible.

For biometric verification tasks, several works have explored quantifying uncertainty by adapting confidence intervals. Predominantly, these works employ a distribution-based approach due to their reliability and lower computational demands. Initial research by Shen et al. [23] focused on parameter estimation from repeated Bernoulli experiments to establish confidence intervals, simplifying the approximation of the binomial distribution to a normal distribution. Following this methodology, Veres et al. [21] utilized the Chernoff bound to approximate the binomial distribution with a normal distribution. Moreover, Li et al. [22] introduced confidence elasticity as a metric to evaluate the trade-off between sample size and the precision of evaluation metrics again under the assumption of normal distribution. On the other hand, employing the bootstrap approach, Bolle et al. [24] developed the subsets bootstrap method to calculate the confidence intervals for the Receiver Operating Characteristic (ROC) curves in biometric recognition systems. Additionally, Dass et al. (2006) [20] merged both methodologies, utilizing a multivariate joint distribution through a parametric family of Gaussian copulas and the bootstrap method to estimate confidence intervals for ROC curves.

## B. Limitations of Previous Works

Studies on estimating confidence intervals for biometric verification results have primarily two limitations. First, the proposed methods are complicated to apply without specialized statistical knowledge, creating a burden to use these methods in practice. Secondly, many confidence estimation methods make strong assumptions regarding their error distribution, such as assuming a normal distribution of the samples and uniform sample sizes across subjects, which are not given in real systems and thus, are mostly not valid. To address these issues, we introduce an uncertainty estimation framework that builds on more realistic assumptions and is easy to apply to
arbitrary biometric verification tasks. This aims to encourage the use of uncertainties in biometrics and thus, to promote the development of more reliable biometric solutions and datasets.

## III. Methodology

Uncertainty estimation is important to quantify the reliability of a biometric verification system. To quantify the uncertainty, we initially formulate a confidence interval in the context of biometric verification, named BioQuake, and establish straightforward rules that researchers can easily apply to calculate the required number of comparisons to reach a desired uncertainty or to estimate the uncertainty based on the number of comparison scores. We then define uncertainty classes to facilitate easy comparison of the uncertainty between biometric solutions and finally, we discuss the upper and lower bounds of BioQuake.

## A. Introducing BioQuake ( $\delta$ )

Evaluating biometric verification systems requires the computation of comparison scores of genuine and imposter pairs to calculate FMR and FNMR. To formulate the FMR and FNMR based on the underlying distributions of comparison scores, the distributions of genuine and imposter comparison scores are denoted as $P_{G}$ and $P_{I}$, respectively. Assuming a decision threshold of $t$, the FMR and FNMR are defined as

$$
\begin{gathered}
F M R=\int_{t}^{\infty} P_{I}(s) d s=: p_{F M} \\
F N M R=\int_{-\infty}^{t} P_{G}(s) d s=: p_{F N M}
\end{gathered}
$$

The FMR can be described as the probability $p_{F M}$ that an imposter comparison is falsely matched as a genuine comparison. Similarly, the FNMR can be defined as the probability $p_{F N M}$ that a genuine comparison is falsely considered as a non-match (imposter).

In the following, we assume drawing $N$ samples independently from a score distribution $P_{O}$, where $O \in I, G$ is either an imposter $(I)$ or genuine $(G)$ score distribution. The probability of a faulty decision based on a score $s$ drawn from this distribution is denoted as $p$. For $O=I$ imposter, this happens for $s \geq t$ (a false match) and for $O=G$ genuine, this happens for $s<t$ (a false non-match). Consequently, the probability of observing $n$ wrong matching decisions from the $N$ i.i.d. samples drawn from $P_{O}$ can be modeled by a binomial distribution:

$$
p(X=n)=\binom{N}{n} p^{n}(1-p)^{N-n}
$$

To calculate the acceptance region that the observed error rate $p$ is reasonable with confidence of $1-\alpha$, we can compute the lower and higher boundary $\left[n_{L}, n_{H}\right]$ by finding the highest $n_{L}$ and the lowest $n_{H}$ that fullfills

$$
\begin{aligned}
P\left(X<n_{L}\right) & =\sum_{n=0}^{n_{L}} p(X=n) \leq \frac{\alpha}{2} \\
P\left(X>n_{H}\right) & =1-\sum_{n=0}^{n_{H}} p(X=n) \leq \frac{\alpha}{2} .
\end{aligned}
$$

By setting the acceptance region $\left[n_{L}, n_{H}\right]$ in relation to the number of observed samples $N$, we can derive an uncertainty range of the error rates

$$
\left[\frac{n_{L}}{N}, \frac{n_{H}}{N}\right] \hat{=}\left[F M R_{L}, F M R_{H}\right] \hat{=}\left[F N M R_{L}, F N M R_{H}\right],
$$

i.e. FMR if $O=I$ or FNMR if $O=G$. Assuming that the observed error rate $\frac{n}{N}$ is centered in this region, we can compute the uncertainty $\Delta$ of the error rate as

$$
\Delta=\frac{n_{H}-n_{L}}{2 N} .
$$

This means if we observe, an FNMR = 2\% and a $\Delta=1 \%$, the true FNMR value might lay within the region of 2\% ± 1\% with a probability of $1-\alpha$.

To make the comparison of the uncertainties comparable for different error rates, we further introduce the term BioQuake $(\delta)$ which is defined as

$$
\delta=\frac{\Delta}{p} .
$$

BioQuake is defined as the ratio of the uncertainty $\Delta$ and the observed error rate $p$, and it describes the uncertainty with respect to the verification error. For instance, $\delta=0.1$ means that the uncertainty is 10\% of the observed error rate, indicating a more precise estimate. In contrast, $\delta=1$ refers to an uncertainty as large as the error rate itself, suggesting a much less reliable estimate. This will allow us later to comprehensively compare the uncertainties across different biometric algorithms and modalities.

## B. Determining BioQuake Visually

To provide better intuition, we visualize the relationship between error rate, and the minimum number of comparisons required to achieve a specific BioQuake uncertainty for three different confidence levels of 90\% $(\alpha=10 \%)$, 95\% $(\alpha=5 \%)$, and $99 \%(\alpha=1 \%)$. These figures demonstrate that a lower error rate requires a larger number of samples to maintain a specific BioQuake rate, and achieving a higher confidence level requires a larger sample size (Figure 1). Given the number of comparisons and an observed error rate, these figures allow for determining the uncertainty of the reported error rate observation.

For a confidence level of 95\% $(\alpha=5 \%)$, Figure 2 illustrates the relationship between the observed error rate and the required number of comparisons to achieve a specific BioQuake uncertainty. This figure enables estimation of the required number of comparisons to reach a desired uncertainty level and indicates the error rate range within which reporting remains reliable.

## C. BioQuake Rules

Next, we want to define some easily applicable rules for estimating the uncertainty of biometric verification tasks and the number of comparisons needed for significant performance reporting. These rules rely on the linear relationship between the error rate $p$ and the number of comparisons $N$ for a fixed BioQuake uncertainty ( $\delta$ ) level seen in Figure 2 . Based on this,

![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-04.jpg?height=490&width=1747&top_left_y=236&top_left_x=196)
Fig. 1. Visualization of Bioquake Uncertainty at Different Confidence Levels - The relationship between the observed error rate (FMR/FNMR) and the required number of comparisons to achieve a specific BioQuake uncertainty is displayed for the confidence levels of 90\% ( $\alpha=10 \%$ ), 95\% ( $\alpha=5 \%$ ), and $99 \%(\alpha=1 \%)$.

![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-04.jpg?height=619&width=840&top_left_y=915&top_left_x=187)
Fig. 2. Visualization of BioQuake Principles - The relationship between the observed error rate (FMR/FNMR) and the required number of comparisons to achieve a specific BioQuake uncertainty $\delta$ is displayed (for $\alpha=0.05$ ). Based on this, the required number of comparisons for a specific uncertainty, as well as the significance of measurement, could be determined.

we define some straightforward rules of thumb to can be easily applied. The 1\% and 10\% rules ensure that the measured error only differs by 1\% and 10\% from the true error. We included a 6\% rule since it leads to an easy-to-remember rule of thumb.

The 1\% Rule ( $\delta=0.01$ ) - To measure an Error Rate (ER), such as the False Match Rate (FMR) or False Non-Match Rate (FNMR), and ensure with 95\% confidence that the true error differs by no more than 1\% from the measured error, a minimum of $R C=\frac{3.83 \times 10^{4}}{E R}$ comparisons is required.

The 6\% Rule $(\delta=0.061)$ - To measure an Error Rate (ER), such as the False Match Rate (FMR) or False Non-Match Rate (FNMR), and ensure with 95\% confidence that the true error differs by no more than
$6.1 \%$ from the measured error, a minimum of $R C=\frac{10^{3}}{E R}$ comparisons is required.

The $\mathbf{1 0 \%}$ Rule ( $\delta=0.1$ ) - To measure an Error Rate (ER), such as the False Match Rate (FMR) or False Non-Match Rate (FNMR), and ensure with 95\% confidence that the true error differs by no more than 10\% from the measured error, a minimum of $R C=\frac{3.7 \times 10^{2}}{E R}$ comparisons is required.

For dealing with FMR, the Required Comparisons (RC) reflect the number of imposter comparisons needed. For FNMR, the RC indicates the number of genuine comparisons.

For example, if an error for a FMR of $10^{-3}$ should be measured, according to the 6\% - Rule, you need at least $10^{6}$ imposter comparisons to ensure that the measured error only differs by around 6\% of the true one. Similarly, the 10\% rule states that to measure an error for an FNMR of $10^{-3}$, at least $3.7 \times 10^{5}$ genuine samples are needed to ensure that the measured error deviates by no more than 10\% from the true error. Additionally, to achieve an error measurement with a 1\% uncertainty for the same FNMR, the number of genuine comparisons must increase by a factor of 100, requiring at least $3.83 \times 10^{7}$ comparisons.

## D. Certainty Classes

To facilitate understanding and comparison of reported uncertainty across different biometric solutions and modalities, we introduce an uncertainty classification as follows:

- Class A+ (Optimal): $\delta<0.01$
- Class A (Excellent): $0.01 \leq \delta<0.05$
- Class B (Very Good): $0.05 \leq \delta<0.10$
- Class C (Good): $0.10 \leq \delta<0.30$
- Class D (Fair): $0.30 \leq \delta<0.50$
- Class E (Poor): $0.50 \leq \delta<1.00$
- Class F (Unacceptable): $\delta>1$

Classes A+ represent cases with minimal uncertainty, indicating high reliability in the reported results, with a drift potential of less than 1\% for true error. Classes A and B
represent low uncertainty, showing only minor variability that does not substantially impact the trustworthiness of the results. Classes C and D denote moderate uncertainty, where the results have reduced reliability but remain within acceptable limits for most applications. Class E signifies significant risk, with uncertainty approaching or equaling the magnitude of the reported result, necessitating caution in data interpretation. Class F is designated for extreme cases where the uncertainty exceeds the reported result, indicating highly unreliable data that could mislead decision-making processes.

## E. Upper and Lower Bounds of Uncertainty

Since it is important to understand the range of possible BioQuake values when evaluating biometric solutions, we define the upper and lower bounds of uncertainty $(\Delta)$ based on Equation 7. Given $n_{L / H} \in\{0,1, \ldots, N\}$, the bounds for the error rate uncertainty are:

$$
\Delta_{\max }=\frac{1}{2}, \quad \Delta_{\min }=\frac{1}{2 N}
$$

The upper limit $\Delta_{\text {max }}=\frac{1}{2}$ is logical, as it accounts for the full range of potential error rates in both directions. The lower limit $\Delta_{\text {min }}=\frac{1}{2 N}$ represents the smallest uncertainty measurable with this approach. Given these bounds for $\Delta$, we can determine the bounds for BioQuake $(\delta)$

$$
\delta_{\max }=\infty, \quad \delta_{\min }=\frac{1}{2 N} .
$$

The upper limit $\left(\delta_{\text {max }}\right)$ occurs under conditions of minimal error $p$ combined with $\Delta_{\text {max }}$, and the lower limit $\left(\delta_{\text {min }}\right)$ corresponds to $\Delta_{\text {min }}$ with an error equal to 100\%. This means that, with a very low error rate based on a small number of observations, the relative uncertainty can become extremely large, potentially approaching infinity. In contrast, if an error rate of 1 is observed, the uncertainty decreases proportionally with the number of evaluations. In practice, most situations lie between these extremes, indicating that increasing the number of observations reduces uncertainty. However, reporting a very low error rate with reasonable certainty requires a much larger sample size. This is because accurately estimating a small error rate demands enough observations for the error to occur sufficiently for a reliable estimate. This issue becomes even more critical in the context of the FMR, where minimizing the probability of attacker access necessitates reporting a very low error rate to ensure system robustness.

## IV. Experimental setup

To validate the effectiveness and relevance of the BioQuake metric, we conducted two experiments. First, we demonstrate the correctness of our approach empirically. Second, we applied our metric to assess the uncertainty of errors in state-ofthe-art biometric solutions on various benchmarks and datasets to investigate the significance of the solutions tested on this data.

## A. Setup A: Empirical Correctness Analysis of BioQuake

To empirically evaluate the theoretical uncertainty calculated by the proposed BioQuake approach, we design an experiment including three large facial datasets and four wellknown face recognition models. These datasets and models were selected due to their extensive development, rigorous testing, and significant representation in the literature. Below, we provide a detailed description of the experimental setup.

Datasets: We utilized three facial recognition datasets to assess the uncertainty of FMR and FNMR empirically: the ColorFERET dataset [25], [34], the Labeled Faces in the Wild (LFW) dataset [26], and the Adience dataset [27]. The ColorFERET dataset consists of over 11,000 images captured under controlled conditions, featuring systematic variations in pose, expression, and lighting to maintain consistent testing environments. In contrast, the LFW dataset comprises over 13,000 faces sourced from the web under less controlled but high-quality images. While LFW often refers to a benchmark based on these images with only 6k predefined comparisons, we utilize LFW (full), referring to the usage of all images against each other. The Adience dataset contains over 26,000 everyday images and focuses on unconstrained images with often low image quality. Collectively, these datasets facilitate comprehensive testing of our uncertainty assessment algorithm across various facial recognition scenarios.

Metrics: Following the ISO standard [35] for measuring biometric system performance, the primary metrics discussed are the False Non-Match Rate (FNMR) and the False Match Rate (FMR). The FNMR quantifies the likelihood that the biometric system will incorrectly reject an attempt by an authorized user to gain access. Conversely, the FMR measures the probability that the system will incorrectly accept an unauthorized user.

Utilized Models: To extract face templates and thus, calculate comparison scores and FMR/FNMR, we employed four well-known pre-trained face recognition models. Each model offers unique features and methodologies for vector representation essential for our analysis. FaceNet [36], pioneered by Google, employs a triplet loss function, which trains the network to map facial images into Euclidean space where the distances equate to facial similarity. This technique enhances face recognition by reducing distances between similar faces and increasing those between dissimilar ones, thus improving accuracy in identity verification. ArcFace [37] builds upon FaceNet's methodology by incorporating an additive angular margin loss, which increases the geometric margin, improving the model's discriminative capacity. This adjustment aids in achieving tighter intra-class compactness and enhanced interclass separability. MagFace [13] introduces a magnitude-aware loss function that varies the loss contribution according to the embedding's magnitude, which correlates with the facial image's quality; higher-quality images result in larger magnitudes. This strategy encourages the model to prioritize higher-quality images while continuing to learn from those of lower quality. Finally, QMagFace [12] integrates the quality information of the face samples in the comparison process to enhance its recognition performance under unconstrained
circumstances. For the experiments, we used the (ResNet100/iResNet-101) models from the official repositories of the authors to extract the face templates. Comparing the two templates was done based on the standard cosine similarity.

Method: To investigate empirical uncertainty, extracted face templates from each face image and computed the cosine similarity between every distinct pair of images within each dataset, generating genuine scores for images from the same subject and impostor scores for pairs from different subjects. Then, for each dataset and model, the comparisons are randomly sampled with sizes of 0.1, 0.01, and 0.001 of the overall sample size (denoted as frac), ten times, and then computed the FMR and FNMR. The standard deviation of these sample means was calculated to estimate the Standard Error of the Mean (SEM). This estimated SEM was then multiplied by 1.96 to determine the margin of error at a 95\% confidence level [38], [39], representing the empirical uncertainty. Finally, BioQuake, with the same 95\% confidence level, was calculated as the theoretical uncertainty predicted by our method to assess the similarity between empirical and theoretical uncertainty.

## B. Setup B: Uncertainty Analysis of Existing Datasets

To explore uncertainty issues in current biometric verification research, we investigated 62 biometric datasets and benchmarks by analyzing state-of-the-art performances reported from works in leading conferences and journals in the field. Our review covered a range of eight biometric modalities, including facial recognition and fingerprints as widely used physical biometrics, as well as gait, iris, Electrocardiogram (ECG), Electroencephalogram (EEG), eye-tracking analysis, and keystroke dynamics as emerging behavioral biometrics. We selected papers only from Q1 and Q2 journals and A+ and A conferences. Although, IJCB is not ranked in the Scientific Journal Rankings ${ }^{3}$ and Core ranking ${ }^{4}$ in the community it is considered as one of the three top biometric conferences along IAPR ICB and IEEE BTAS.

For each paper, we extracted the number of impostor and genuine comparisons used to evaluate error rates. Then, we calculated the BioQuake for each error type with a 95\% confidence interval. Additionally, we estimated the minimum reportable error rate, setting the delta value at 6.1\% (calculated using $E R=\frac{10^{3}}{N C}$, where NC is the number of available comparisons), to elucidate the limitations of current error reporting methodologies and motivate future studies to improve error reporting via BioQuake.

## V. Results

## A. Empirical Correctness Analysis of BioQuake

In this section, the correctness of the theoretical uncertainty measure BioQuake is analysed empircally on the three described large-scale face recognition datasets on four popular face recognition systems as described in Section IV-A

[^2]Correlation Analysis: To investigate wether the proposed theoretical uncertainty measure BioQuake reflects the empirical uncertainty, the Pearson correlation between the theoretical and empirical uncertainty values are computed over different datasets and face recognition models. In Table II, these correlations are shown by computing the average correlation for each dataset-model combination. The correlation values indicate a strong positive relationship between theoretical and empirical uncertainty across different models. Typically, a Pearson correlation greater than 0.7 indicates a strong positive linear relationship [88]. Thus, the high correlations observed confirms the effectiveness of our approach in estimating uncertainty across diverse datasets.

Comparative Analysis: To further analyse how well BioQuake can estimate the uncertainty for recognition tasks, BioQuake and the empirical uncertainty are calculated for different fractions of the dataset. Figures 3 and 4 show these uncertainties for FMR and FNMR over three datasets and four face recognition models. In most cases, it can be observed that BioQuake closely resembles the empirical uncertainty. However, when only a small fraction of the data is used, in some minor cases, such as in Figure 4 QMagFace-ColorFeret, MagFace-LFW, ArcFace-ColorFeret, and ArcFace-LFW, the prediction deviates from the experimental values. This can be explained by the stochastic nature of the experimental setup as only a small fraction is used and thus, the data characteristics can vary significantly. Generally, the results show a high effectiveness of BioQuake in estimating the uncertainty for recognition tasks.

## B. Uncertainty Analysis of Existing Datasets

To investigate the reliability of existing datasets and benchmarks, we calculate the BioQuake uncertainty on the stateof-the-art verification solutions on various biometric datasets and benchmarks. Table I summarizes this uncertainty analysis. It involves 62 biometric recognition datasets ${ }^{5}$ covering 8 biometric modalities, namely ECG, EEG, eye-tracking, face, fingerprint, gait, iris, and keystroke dynamics. Moreover, it reports the database statistics including the number of captured sessiona (\#S), the number of identities (IDs), and the number of genuine (Gen) and imposter comparisons (Imp) involved in the performance calculation. The last column in Table I shows the minimum reportable errors for datasets according to our 6\% rule.

The analysis shows that 24 out of 62 FNMRs and 16 out of 62 FMRs reported on these dataset instances exhibit a BioQuake exceeding 0.3, indicating that the error might vary by more than 30\% compared to the reported value, which is the threshold we set for a "Good" reliability. More importantly, 18 FNMR (29\%) and 11 FMR (18\%) instances show a BioQuake higher than 0.5, highlighting the need more reliability in biometric verification research.

[^3]![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-07.jpg?height=1977&width=1783&top_left_y=370&top_left_x=172)
Fig. 3. Comparative Analysis between the theoretical BioQuake and empircal Uncertainty for FMRs - For different fractions (frac) of the base datasets, the proposed theoretical BioQuake approach (dashed line) is compared against the empirical uncertainty (solid line) of FMRs on different model-dataset combinations. A high similarity between both approach is seen indicated the strong effectiveness of BioQuake in estimating the uncertainty.

![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-08.jpg?height=1977&width=1781&top_left_y=370&top_left_x=172)
Fig. 4. Comparative Analysis between the theoretical BioQuake and empircal Uncertainty for FNMRs - For different fractions (frac) of the base datasets, the proposed theoretical BioQuake approach (dashed line) is compared against the empirical uncertainty (solid line) of FNMRs on different model-dataset combinations. A high similarity between both approach is seen indicated the strong effectiveness of BioQuake in estimating the uncertainty.

TABLE I
Uncertainty Analysis on Biometric Recognition Datasets－Performance of state－of－the－art biometric systems from top－tier venues using 62 datasets across 8 modalities．For each dataset，we report the number of recorded data collection sessions（＃S）， identities（IDs），imposter（Imp）and genuine（Gen）comparisons，and performance in terms of FNMR and FMR．Datasets marked WITH＊WHERE USED IN DIFFERENT CONFIGURATIONS，DESCRIBED IN THE REFERENCED PUBLICATIONS．FOR EACH PERFORMANCE METRIC，WE computed the BioQuake uncertainty（ $\delta$ ）and the number of minimal errors measured for the $6 \%$ rule．Legend：Uncertainty is color－coded as Optimal，Excellent，Very Good，Good，Fair，Poor，and Unnacceptable；NA＝Not Available，；Private＝ Dataset not Publicly Available（Though information about identity comparisons is contained in the publication）
|  | Dataset |  |  |  |  | Publication |  |  |  | FNMR |  | FMR |  | Min．Error for $\delta=6.1 \%$ |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
|  | Dataset | ＃S | IDs | Imp | Gen | Publ． | Year | Venue | Rank | FNMR［％］ | $\delta_{F N M R}$ | FMR［％］ | $\delta_{F M R}$ | FNMR | FMR |
| ECG | Private［40］ | 1 | 28 | 3．9K | 140 | 40 | 2016 | IEEE SPL | Q1 | 1.90 | 0.93984 | 5.20 | 0.13067 | $\geq 1$ | $3 * 10^{-1}$ |
|  | ECG－ID＊［41］ | ＞1 | 90 | 4M | 45 K | ［8］ | 2019 | IEEE Access | Q1 | 2.00 | 0.06444 | 2.00 | 0.006849 | $2 * 10^{-2}$ | $2 * 10^{-4}$ |
|  | E－HOL［42］ | 1 | 202 | 4．2M | 45．8K | 43 | 2019 | PRL | Q1 | 2.15 | 0.06144 | 2.15 | 0.00644 | $2 * 10^{-2}$ | $2 * 10^{-4}$ |
|  | MIT－BIH［42 | ＞1 | 47 | 1M | 23．5K | ［8］ | 2019 | IEEE Access | Q1 | 4.74 | 0.05688 | 4.74 | 0.00875 | $4 * 10^{-2}$ | $1 * 10^{-3}$ |
|  | PTB＊［44］ | 5 | 52 | 1．3M | 26 K | ［8］ | 2019 | IEEE Access | Q1 | 0.59 | 0.15319 | 0.59 | 0.02229 | $4 * 10^{-2}$ | $8 * 10^{-4}$ |
|  | CYBH1＊［45］ | 2 | 63 | 315 | 63 | ［5］ | 2023 | IEEE Access | Q1 | 6.98 | 0.79592 | 6.98 | 0.36385 | $\geq 1$ | $\geq 1$ |
|  | CYBHi＊［45］ | 1 | 63 | 945 | 189 | ［5］ | 2023 | IEEE Access | Q1 | 5.44 | 0.53493 | 5.44 | 0.2626 | $\geq 1$ | $\geq 1$ |
|  | ECG－ID＊［41］ | 1 | 89 | 1．3K | 267 | ［5］ | 2023 | IEEE Access | Q1 | 1.52 | 0.7392 | 1.52 | 0.40485 | $\geq 1$ | $8 * 10^{-1}$ |
|  | ECG－ID＊［41］ | $>1$ | 89 | 445 | 89 | ［5］ | 2023 | IEEE Access | Q1 | 0.26 | ＞ 1 | 0.26 | ＞ 1 | $\geq 1$ | $\geq 1$ |
|  | In－house＊［5］ | 1 | 55．9K | 77．6K | 15.5 K | ［5］ | 2023 | IEEE Access | Q1 | 1.28 | 0.13608 | 1.28 | 0.06141 | $6 * 10^{-2}$ | $1 * 10^{-2}$ |
|  | In－house＊［5］ | 2 | 26K | 25．8K | 5．1K | ［5］ | 2023 | IEEE Access | Q1 | 1.97 | 0.18413 | 1.97 | 0.08558 | $2 * 10^{-1}$ | $4 * 10^{-2}$ |
|  | PTB＊［44］ | 1 | 113 | 1.7 K | 339 | ［5］ | 2023 | IEEE Access | Q1 | 0.14 | ＞ 1 | 0.14 | ＞ 1 | $\geq 1$ | $6 * 10^{-1}$ |
|  | PTB＊［44］ | 5 | 113 | 565 | 113 | ［5］ | 2023 | IEEE Access | Q1 | 2.06 | ＞ 1 | 2.06 | 0.5155 | $\geq 1$ | $\geq 1$ |
| EEG | Pin Cal | u | 心 | SUGA | J．3．1 | 7 | 00 | PT | 0 | ＋ 40 | O8INE | ＋ 40 | O80，00 | ＊＊＊ | ＊＊＊ |
|  | MOMMODOLO | － | －0 | ● 6.01 S | जु | N | NONN | DF | 0 | 「ol | 0.000 | 「ol | 0％ | ＊＊＊0！ | N＊ 61 ！ |
|  | DINONDED | － | 古 | 十八衣 | DGO | N | NUU N No． | PBOH | ＞ | 01 | DCH | －0 | 0.0000 | ＊＊＊ | N＊ 61 |
|  | PT CO T ST CO T | － | ＋ | wan | ○ 00 | － | POL | ＞31－10 | $\underline{0}$ | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=27&width=51&top_left_y=1085&top_left_x=1260) | DCO | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=27&width=49&top_left_y=1085&top_left_x=1511) | 0.0 ． | IV | U＊Uld |
|  | Pillattetts | － | ur | 「NNON | べ | ＋ | 0000 | C | $\underline{0}$ | ● | ●●○上の | Ón | 0919000 | ＊＊＊ | ＊＊＊ |
| ng | PLADEC | ＋ | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=24&width=32&top_left_y=1151&top_left_x=566) | ن | 可 | 心 | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=22&width=56&top_left_y=1153&top_left_x=897) | DBIODFO | 0 | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=24&width=49&top_left_y=1153&top_left_x=1262) | DC | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=24&width=49&top_left_y=1153&top_left_x=1511) | 00000 | IV | IV |
|  | PLADS | － | மு | 三 | 元 |  | 000 | ＞31－1000 | 0 | － | 04000 | 0.0 | 0.0000 | IV | 「＊／〇। |
|  | PT PC TB | N | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=26&width=32&top_left_y=1215&top_left_x=566) | 元 | 0 | PU N | 00 | B | P | å | 01E1 | oie | DCHJ | IV | IV |
|  | PTIMEDIDED | － | N | ＠ | OW |  | 000 | Cी | ＞ | －$\infty$ | 010 | －$\infty$ | ●1－91 | IV | 「＊／〇！ |
|  | DCROW：－UD | 0 | WN | 「AS | 0° × | 0 | NONN | CPODS | $\underline{0}$ | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=26&width=61&top_left_y=1279&top_left_x=1257) | 0.0000 | ●90 | 0.001 G | －＊ | －＊ |
|  | DACCDOFCHC | 0 | WNN | 0％ | பூ | $v$ | N2NN | CO CO | $\underline{0}$ | uius | － | MU | 0.000 | N＊ 61 | 「＊／〇। |
|  |  | 0 | WN | PO | PO | M | ÕN | FOM－DS | $\underline{0}$ | up | 00.0000 | 0.0 | V | ひ＊UIN | ひ＊UIN |
|  |  | Zim | － | 心 | D | B | 00 | J | ＞ | 0 | UAGA | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=24&width=51&top_left_y=1378&top_left_x=1509) | UADUP | cw lo l | ＊＊＊01 |
|  | 「ருவுவ（जा | Zi | 呟 | Unin | Sox | w | 000 |  | $\underline{0}$ | 00 | － 0000 | 0 | 0.003 | ＊＊＊01 | N＊↓ |
|  | DCSOLESU | Zi | 一分 | 二〇 | 「NOL | U | 000 | FOTITOD－TA | 0 | ペー | 00301 S | 0 | 000000 | ＊＊＊ | ＊＊ |
|  | EUGEUS | Zi | －$\overline{\mathrm{C}}$ 交 | வூ | DCu | w | 00 | CJ | ＞ | USO | O | 0.0 | 00．001 | －＊ 6 | 「＊／〇！ |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  | EUDU | Zi | 心 | जुत्र |  | G | 00 | Juro | ＞ | ＋$\stackrel{\text { }}{\text { 古 }}$ | ÖCHO | 0 | 00000 | び ildin | の＊ |
|  | ELO | Zi | い一خ | www | 三 | w | 00 | Clai | ＞ | 一ക്ക | 0.00121 － | 101－1 | 0.0000 | ＊＊01 | U＊11 |
|  | DTDTDTD | ZI | 二十八 | UON | 一真 | G | POSO | Clard | ＞ | ＋ | 0000 | ＋ | 0.00120 | －＊ 61 | N＊ |
|  | PLITEL | Zi | 一充 | W | W | w | PLOH | PTIDF | ＞ | NU | ●1WIN | NM | ●1NAS | CWH। | U＊U |
|  | EWHOL | Zi | 一串交 | Si | （D） | U | PON | Clard | ＞ | $\omega$ | 0.001 ． | ou | 0.001 | －＊ 61 | 「＊／〇। |
|  | EW）U | Zi | $\omega$ 元 | जUS |  | 9 | NON | CJ | ＞ | へ〇 | 0.0000 | 〇七 | 0.00 × | ひ＊Lí N | の |
|  | 「T N／NJ | Zi | 一六 | W | W | $y$ | PON | CJ | ＞ | i | 09．00％ | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=26&width=51&top_left_y=1703&top_left_x=1509) | 09．00％ | ひ＊ 6. | ש゙＊（I |
|  | ＞ 000000 ． | ZIT | 04．1 | W | い | N | CU | CJ | ＞ | － | DB 000 | － | DC ${ }^{2}$ × ${ }_{3}$ | U＊UI | N＊DI |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  |  | Zi | W | DCulcales | へ〇元 | ＠ | COL | 日切師 |  | 0.0 | DG101101101 | 0.0 | 00000 | ＊＊＊0！ | 「＊／〇। |
|  | 「T1／ADJ．／J |  |  |  |  |  |  |  | $\underline{0}$ |  |  |  |  |  | 「＊／〇！ |
|  | CODEMETI EDE | Zim | 元 | Glan | 口 | Ost | POL | －1 | 0 | － 5 | 0.003 | － 5 | 0.0 | ＊＊＊ | N＊DIM |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  | Deter（＃PE）T VAT | Zi | W | 50 | DCurking | Palaip | COL | H（V） | $\underline{0}$ | NUL | O U U | Nú№ | 0.0010 | ↓ $\stackrel{\text { ↓ }}{\text { ↓ }}$ ！ | ன＊01の |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  | T13001－01 | ZIT V | Б | ↓↓ | へ凶 | 8 | 000 | D | 0 | $\boxed{\boxed{V}_{1}}$ | DNOM | $\boxed{\boxed{V}_{1}}$ | DCUL | ＊＊＊ | N＊ 6 |
|  |  | Zim | 三〇 | 十一分 | へ | 9 | 000 | FTODS |  | 50 | DCHOO | 50 | O | ＊＊＊ |  |
|  | T13C0115 |  |  |  |  | 9 |  |  | $\underline{0}$ |  |  |  |  |  | N＊ 61 |
|  | T1300001 | Zi | 8 | ●●オ | 0000 | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=27&width=34&top_left_y=1931&top_left_x=842) | 00 | CJ |  | ＋ | Ö 2121 J | 0 | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=27&width=96&top_left_y=1931&top_left_x=1608) |  | 「＊／〇！ |
|  |  |  |  |  |  |  |  |  | 0 |  |  |  |  | IV |  |
|  | T1CTOO | ZIT | 「古 | ⊙ | ● | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=29&width=36&top_left_y=1962&top_left_x=841) | NOO | FTFT FIDIE | $\underline{0}$ | 01－1 | DBUD | D | ●●ปฏ○ | 「＊／〇！ | 「＊／〇！ |
|  | T1300E | Zi | 10 | 十一六 | へ凶ス | 9 | CO 1 m．H | O 1 日田再 | Zi | ハーム | DCUDH | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=27&width=53&top_left_y=1996&top_left_x=1509) | 0°c 0000 | ＊＊41－ | N＊ 61 |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  |  | ZI | చు | DCTICS |  |  | POL |  |  | NOS | －00000 | NCN | 08000 | ＊＊＊ | の＊$\stackrel{\text { 〇〇 }}{\text { 是 }}$ |
|  | 「TDニU |  |  |  |  | － |  |  | $\underline{0}$ |  |  |  |  |  |  |
| Gait <br> Gait | PLADS | N | N | 可 | 可 | 8 | 00 | M M 171 | 0 | T™ | 0.0000 | T™ | 09．15．0 | IV | IV |
|  | ait naw ad a | NO | N | 式 | へ入 | ＆ | NO | FABHER | $\underline{0}$ |  | DUU | － | － 1 × | critol | IV |
|  | PLACES | ✓ | w | 元 | 贰 | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=27&width=36&top_left_y=2126&top_left_x=841) | NOSO UCN | NOSO UCN | $\underline{0}$ | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=29&width=51&top_left_y=2122&top_left_x=1260) | 0.00100 | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=26&width=51&top_left_y=2126&top_left_x=1509) | 0.00100 | IV | IV |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  | PLA But | 0 | － | 一十一真 | 一真 | cl | DCUFTITFEDF | DCUFTITFEDF | $\underline{0}$ | NNON | 00000 | Nisi | ![](https://cdn.mathpix.com/cropped/5b0fcfa6-1760-4c5c-ac10-e300f930af31-09.jpg?height=27&width=96&top_left_y=2156&top_left_x=1608) | －＊ | －＊ 1 D |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Iris <br> Iris <br> Iris | （2）521351－1 | Z | －00 | NW | 古克 | N | NOOOCE | COOO | 0 | ÓN | 090961 | ÓN | ÓL ${ }^{\circ} \mathrm{D}$ ， | N＊11 | ＊＊ |
|  | PLDPIEDS（M）DM | ZIT | மீ | べ夕 | WHU | A | PO PD |  | $\underline{0}$ | Puri |  | 044 | ODH＝ | U＊Uld | ＊＊4－1 |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  |  |  |  | 웢 |  |  | DCUMM | DCUMM |  | －0 |  |  | 0＋ | IV |  |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |


TABLE II
Correlation Analysis between the theoretical BioQuake and empirical Uncertainty - Average Pearson correlation BETWEEN THEORETICAL (BIOQUAKE) AND EMPIRICAL UNCERTAINTIES across different models and datasets. The high correlation DEMONSTRATES THAT THE PROPOSED THEORETICAL UNCERTAINTY HIGHLY REFLECTS THE EMPIRICAL ONE.
| Model | Metric | ColorFERET | LFW | Adience |
| :--- | :--- | :--- | :--- | :--- |
| QMagFace [12] | FMR | 0.9864 | 0.9893 | 0.9985 |
|  | FNMR | 0.9878 | 0.9873 | 0.9776 |
| MagFace [13] | FMR | 0.9925 | 0.9847 | 0.9960 |
|  | FNMR | 0.9889 | 0.9905 | 0.9715 |
| ArcFace [37] | FMR | 0.9870 | 0.9884 | 0.9962 |
|  | FNMR | 0.9771 | 0.9808 | 0.9856 |
| FaceNet [36] | FMR | 0.9945 | 0.9828 | 0.9974 |
|  | FNMR | 0.9798 | 0.9845 | 0.9738 |


The last column in Table I shows the minimum reportable errors for the datasets when the confidence level is 95\% and the BioQuake is 0.061 (6\% rule). For 15 reported FNMR and 17 reported FMR results, the minimum reportable error exceeds 10\%, indicating significant uncertainty in these measurements. Furthermore, when adopting an FMR of 0.001 as recommended by NIST 800-63B [89] and the European Border Guard Agency Frontex [90] for biometric authentication, only 23 out of the 62 reported errors meet this criterion based on the lowest reportable FMR and a BioQuake of 6.1\%.

In contrast to the other modalities, the datasets for face verification generally demonstrate superior reliability because of their larger size. Some exceptions are the LFW-driven benchmarks [26], which provide a low number of pairwise (impostor-genuine) comparisons (3000) for both the FNMR and the FMR. Consequently, no low error rates can be reliably achieved on these small benchmark sizes. Similarly, some datasets within each modality may not support the prediction of reliable results, even if the performance reported on them suggests otherwise, due to uncertainty tied to the dataset's limitations.

Another aspect highlighted by Table I is that the same datasets can yield varying comparison scores depending on the evaluation method used. For instance, in the ECG modality, datasets such as ECG-ID [41], PTB [44], CYBHi [45], and Inhouse [5], as well as the FVC2002 [62] in fingerprint analysis, exhibited different comparison scores for the same dataset. In [5], Melzi et al. consider single and multiple session scenarios, leading to varied comparison scores for each scenario or in [5], a dataset containing 25,000 subjects was used but only 5000 genuine pairs were utilized in evaluations. Consequently, possessing a large dataset alone is insufficient as the number of comparisons utilized is a key factor to consider.

Lastly, we want to point out that many biometric datasets for ECG and EEG, were collected in a single session. Consequently, these datasets can only be used for testing purposes but are often used with train-test splits. Future work in this area needs to keep a subject-exclusive train and test data split into account to prevent overfitting as observed in [91].

In summary, Table I shows that many datasets across various biometric modalities are just too small for the high performance current algorithms can achieve, resulting in performance reports of low reliability that are hardly comparable.

## VI. Limitations

Despite the effectiveness of BioQuake in practice, there are some limitations to consider. One key assumption is that the samples are treated as independent and identically distributed (iid). While our empirical analysis shows that this assumption does not significantly impact BioQuake's performance in most cases, issues may arise when the number of subjects is small relative to the number of samples, or when the majority of samples are concentrated on only a few subjects. In such scenarios, BioQuake's uncertainty estimation may be affected, as the number of subjects is not directly considered in the estimation process. However, since BioQuake bases its estimation on the number of comparisons rather than the number of subjects, we avoid the need to explicitly model how samples are compared. This simplifies the uncertainty estimation significantly compared to prior methods, while maintaining accuracy.

## VII. Conclusion

To improve the reliability of biometric verification reporting, we identify two main challenges: first, convincing the research community of the importance of reporting uncertainties, and second, providing an easy-to-use metric for this purpose. This paper introduces and validates BioQuake, a metric for quantifying uncertainty in biometric error rates. Using BioQuake, we analyzed the performance uncertainty of biometric models utilizing 62 different datasets and published in top-tier venues, none of which included reliability information. In up to 29\% of these systems, the reported impostor acceptance rates vary by more than 50\%, underscoring issues with current practices. We conclude with a call to standardize reliability reporting in biometric research to enable more accurate evaluations and faster progress, supported by our BioQuake framework as a practical tool for this purpose.

## Acknowledgement

This work was funded by the Topic Engineering Secure Systems of the Helmholtz Association (HGF) and supported by KASTEL Security Research Labs, Karlsruhe, and Germany's Excellence Strategy (EXC 2050/1 'CeTI'; ID 390696704). Portions of the research in this paper use the FERET database of facial images collected under the FERET program.

## References

[1] "Information technology - Vocabulary - Part 37: Biometrics," International Organization for Standardization and International Electrotechnical Commission, Standard, Mar. 2022.
[2] A. Ometov, S. Bezzateev, N. Mäkitalo, S. Andreev, T. Mikkonen, and Y. Koucheryavy, "Multi-factor authentication: A survey," Cryptography, vol. 2, no. 1, p. 1, 2018.
[3] I. Sluganovic, M. Roeschlin, K. B. Rasmussen, and I. Martinovic, "Analysis of reflexive eye movements for fast replay-resistant biometric authentication," ACM Transactions on Privacy and Security (TOPS), vol. 22, no. 1, pp. 1-30, 2018.

[4] S. Eberz, G. Lovisotto, K. B. Rasmussen, V. Lenders, and I. Martinovic, "28 blinks later: Tackling practical challenges of eye movement biometrics," in Proceedings of the 2019 ACM SIGSAC Conference on Computer and Communications Security, 2019, pp. 1187-1199.
[5] P. Melzi, R. Tolosana, and R. Vera-Rodriguez, "Ecg biometric recognition: Review, system proposal, and benchmark evaluation," IEEE Access, 2023.
[6] P. Arias-Cabarcos, M. Fallahi, T. Habrich, K. Schulze, C. Becker, and T. Strufe, "Performance and usability evaluation of brainwave authentication techniques with consumer devices," ACM Transactions on Privacy and Security, vol. 26, no. 3, pp. 1-36, 2023.
[7] E. Maiorana, "Learning deep features for task-independent eeg-based biometric verification," Pattern Recognition Letters, vol. 143, pp. 122-129, 2021.
[8] Y. Chu, H. Shen, and K. Huang, "Ecg authentication method based on parallel multi-scale one-dimensional residual network with center and margin loss," IEEE Access, vol. 7, pp. 51598-51 607, 2019.
[9] W. Meng, D. S. Wong, S. Furnell, and J. Zhou, "Surveying the development of biometric user authentication on mobile phones," IEEE Communications Surveys \& Tutorials, vol. 17, no. 3, pp. 1268-1293, 2014.
[10] S. Stephenson, B. Pal, S. Fan, E. Fernandes, Y. Zhao, and R. Chatterjee, "Sok: Authentication in augmented and virtual reality," in 2022 IEEE Symposium on Security and Privacy (SP). IEEE, 2022, pp. 267-284.
[11] X. Liu, K. Raja, R. Wang, H. Qiu, H. Wu, D. Sun, Q. Zheng, N. Liu, X. Wang, G. Huang et al., "A latent fingerprint in the wild database," IEEE Transactions on Information Forensics and Security, 2024.
[12] P. Terhörst, M. Ihlefeld, M. Huber, N. Damer, F. Kirchbuchner, K. Raja, and A. Kuijper, "Qmagface: Simple and accurate quality-aware face recognition," in Proceedings of the IEEE/CVF Winter Conference on Applications of Computer Vision, 2023, pp. 3484-3494.
[13] Q. Meng, S. Zhao, Z. Huang, and F. Zhou, "Magface: A universal representation for face recognition and quality assessment," in Proceedings of the IEEE/CVF conference on computer vision and pattern recognition, 2021, pp. 14225-14234.
[14] M. Wang, W. Deng, J. Hu, X. Tao, and Y. Huang, "Racial faces in the wild: Reducing racial bias by information maximization adaptation network," in Proceedings of the ieee/cvf international conference on computer vision, 2019, pp. 692-702.
[15] T. Zheng, W. Deng, and J. Hu, "Cross-age 1fw: A database for studying cross-age face recognition in unconstrained environments," arXiv preprint arXiv:1708.08197, 2017.
[16] S. Sugrim, C. Liu, M. McLean, and J. Lindqvist, "Robust performance metrics for authentication systems," in Network and Distributed Systems Security (NDSS) Symposium 2019, 2019.
[17] International Organization for Standardization, "Iso/iec 19795-1:2021, biometric performance testing and reporting - part 1: Principles and framework," 2021, accessed: 2024-06-11. [Online]. Available: https://www.iso.org/standard/74716.html
[18] I. T. Jolliffe, "Uncertainty and inference for verification measures," Weather and Forecasting, vol. 22, no. 3, pp. 637-650, 2007.
[19] E. Gilleland, "Confidence intervals for forecast verification: Practical considerations," National Center for Atmospheric Research: Boulder, CO, USA, 2010.
[20] S. C. Dass, Y. Zhu, and A. K. Jain, "Validating a biometric authentication system: Sample size requirements," IEEE Transactions on pattern analysis and machine intelligence, vol. 28, no. 12, pp. 1902-1319, 2006.
[21] G. V. Veres, M. S. Nixon, and J. N. Carter, "Is enough enough? what is sufficiency in biometric data?" in Image Analysis and Recognition: Third International Conference, ICIAR 2006, Póvoa de Varzim, Portugal, September 18-20, 2006, Proceedings, Part II 3. Springer, 2006, pp. 262-273.
[22] R. Li, B. Huang, and W. Li, "Test sample size determination for biometric systems based on confidence elasticity," in The 2012 International Joint Conference on Neural Networks (IJCNN). IEEE, 2012, pp. 1-7.
[23] W. Shen, M. Surette, and R. Khanna, "Evaluation of automated biometrics-based identification and verification systems," Proceedings of the IEEE, vol. 85, no. 9, pp. 1464-1478, 1997.
[24] R. M. Bolle, N. K. Ratha, and S. Pankanti, "Error analysis of pattern recognition systems-the subsets bootstrap," Computer Vision and Image Understanding, vol. 93, no. 1, pp. 1-33, 2004.
[25] P. J. Phillips, H. Wechsler, J. Huang, and P. J. Rauss, "The feret database and evaluation procedure for face-recognition algorithms," Image and vision computing, vol. 16, no. 5, pp. 295-306, 1998.
[26] G. B. Huang, M. Mattar, T. Berg, and E. Learned-Miller, "Labeled faces in the wild: A database forstudying face recognition in unconstrainedenvironments," in Workshop on faces in'Real-Life'Images: detection, alignment, and recognition, 2008.
[27] E. Eidinger, R. Enbar, and T. Hassner, "Age and gender estimation of unfiltered faces," IEEE Transactions on information forensics and security, vol. 9, no. 12, pp. 2170-2179, 2014.
[28] M. Fallahi, T. Strufe, and P. Arias-Cabarcos, "Brainnet: Improving brainwave-based biometric recognition with siamese networks," in 2023 IEEE International Conference on Pervasive Computing and Communications (PerCom). IEEE, 2023, pp. 53-60.
[29] A. J. Bidgoly, H. J. Bidgoly, and Z. Arezoumand, "Towards a universal and privacy preserving eeg-based authentication system," Scientific Reports, vol. 12, no. 1, p. 2531, 2022.
[30] A. Agresti, Categorical data analysis. John Wiley \& Sons, 2012, vol. 792.
[31] P. H. Garthwaite, I. T. Jolliffe, and B. Jones, Statistical inference. Oxford University Press, USA, 2002.
[32] T. J. DiCiccio and B. Efron, "Bootstrap confidence intervals," Statistical science, vol. 11, no. 3, pp. 189-228, 1996.
[33] J. Carpenter and J. Bithell, "Bootstrap confidence intervals: when, which, what? a practical guide for medical statisticians," Statistics in medicine, vol. 19, no. 9, pp. 1141-1164, 2000.
[34] P. J. Phillips, H. Moon, S. A. Rizvi, and P. J. Rauss, "The feret evaluation methodology for face-recognition algorithms," IEEE Transactions on pattern analysis and machine intelligence, vol. 22, no. 10, pp. 1090-1104, 2000.
[35] ISO/IEC JTC1 SC37 Biometrics, Information Technology - Biometric Performance Testing and Reporting - Part 1: Principles and Framework, International Organization for Standardization and International Electrotechnical Committee Std. ISO/IEC 19795-1:2021, 2021.
[36] F. Schroff, D. Kalenichenko, and J. Philbin, "Facenet: A unified embedding for face recognition and clustering," in Proceedings of the IEEE conference on computer vision and pattern recognition, 2015, pp. 815-823.
[37] J. Deng, J. Guo, N. Xue, and S. Zafeiriou, "Arcface: Additive angular margin loss for deep face recognition," in Proceedings of the IEEE/CVF conference on computer vision and pattern recognition, 2019, pp. 4690-4699.
[38] D. K. Lee, J. In, and S. Lee, "Standard deviation and standard error of the mean," Korean journal of anesthesiology, vol. 68, no. 3, p. 220, 2015.
[39] D. G. Altman and J. M. Bland, "Standard deviations and standard errors," Bmj, vol. 331, no. 7521, p. 903, 2005.
[40] S. J. Kang, S. Y. Lee, H. I. Cho, and H. Park, "Ecg authentication system design based on signal analysis in mobile and wearable devices," IEEE Signal Processing Letters, vol. 23, no. 6, pp. 805-808, 2016.
[41] T. S. Lugovaya, "Biometric human identification based on electrocardiogram," Master's thesis, Faculty of Computing Technologies and Informatics, Electrotechnical University 'LETI', Saint-Petersburg, Russian Federation, 2005.
[42] G. B. Moody and R. G. Mark, "The impact of the mit-bih arrhythmia database," IEEE engineering in medicine and biology magazine, vol. 20, no. 3, pp. 45-50, 2001.
[43] R. D. Labati, E. Muñoz, V. Piuri, R. Sassi, and F. Scotti, "Deep-ecg: Convolutional neural networks for ecg biometric recognition," Pattern Recognition Letters, vol. 126, pp. 78-85, 2019.
[44] R. Bousseljot, D. Kreiseler, and A. Schnabel, "Nutzung der ekgsignaldatenbank cardiodat der ptb über das internet," 1995.
[45] H. P. Da Silva, A. Lourenço, A. Fred, N. Raposo, and M. Aires-de Sousa, "Check your biosignals here: A new dataset for off-the-person ecg biometrics," Computer methods and programs in biomedicine, vol. 113, no. 2, pp. 503-514, 2014.
[46] A. L. Goldberger, L. A. Amaral, L. Glass, J. M. Hausdorff, P. C. Ivanov, R. G. Mark, J. E. Mietus, G. B. Moody, C.-K. Peng, and H. E. Stanley, "Physiobank, physiotoolkit, and physionet: components of a new research resource for complex physiologic signals," circulation, vol. 101, no. 23, pp. e215-e220, 2000.
[47] L. Korczowski, M. Cederhout, A. Andreev, G. Cattan, P. L. C. Rodrigues, V. Gautheret, and M. Congedo, "Brain invaders calibration-less p300-based bci with modulation of flash duration dataset (bi2015a)," Ph.D. dissertation, GIPSA-lab, 2019.
[48] M. TajDini, V. Sokolov, I. Kuzminykh, and B. Ghita, "Brainwave-based authentication using features fusion," Computers \& Security, vol. 129, p. 103198, 2023.
[49] Y. Zhang, W. Hu, W. Xu, C. T. Chou, and J. Hu, "Continuous authentication using eye movement response of implicit visual stimuli," proceedings of the acm on interactive, mobile, wearable and ubiquitous technologies, vol. 1, no. 4, pp. 1-22, 2018.

[50] H. Griffith, D. Lohr, E. Abdulin, and O. Komogortsev, "Gazebase, a large-scale, multi-stimulus, longitudinal eye movement dataset," Scientific Data, vol. 8, no. 1, p. 184, 2021.
[51] J. Yin, J. Sun, J. Li, and K. Liu, "An effective gaze-based authentication method with the spatiotemporal feature of eye movement," Sensors, vol. 22, no. 8, p. 3002, 2022.
[52] D. Lohr and O. V. Komogortsev, "Eye know you too: Toward viable end-to-end eye movement biometrics for user authentication," IEEE Transactions on Information Forensics and Security, vol. 17, pp. 3151-3164, 2022.
[53] L. Best-Rowden and A. K. Jain, "Longitudinal study of automatic face recognition," IEEE transactions on pattern analysis and machine intelligence, vol. 40, no. 1, pp. 148-162, 2017.
[54] C. Whitelam, E. Taborsky, A. Blanton, B. Maze, J. Adams, T. Miller, N. Kalka, A. K. Jain, J. A. Duncan, K. Allen et al., "Iarpa janus benchmark-b face dataset," in proceedings of the IEEE conference on computer vision and pattern recognition workshops, 2017, pp. 90-98.
[55] B. Maze, J. Adams, J. A. Duncan, N. Kalka, T. Miller, C. Otto, A. K. Jain, W. T. Niggel, J. Anderson, J. Cheney et al., "Iarpa janus benchmark-c: Face dataset and protocol," in 2018 international conference on biometrics (ICB). IEEE, 2018, pp. 158-165.
[56] M. Wang and W. Deng, "Mitigating bias in face recognition using skewness-aware reinforcement learning," in Proceedings of the IEEE/CVF conference on computer vision and pattern recognition, 2020, pp. 9322-9331.
[57] M. Kim, A. K. Jain, and X. Liu, "Adaface: Quality adaptive margin for face recognition," in Proceedings of the IEEE/CVF conference on computer vision and pattern recognition, 2022, pp. 18 750-18759.
[58] S. Moschoglou, A. Papaioannou, C. Sagonas, J. Deng, I. Kotsia, and S. Zafeiriou, "Agedb: the first manually collected, in-the-wild age database," in proceedings of the IEEE conference on computer vision and pattern recognition workshops, 2017, pp. 51-59.
[59] D. Maio, D. Maltoni, R. Cappelli, J. L. Wayman, and A. K. Jain, "Fvc2002: Second fingerprint verification competition," in 2002 International conference on pattern recognition, vol. 3. IEEE, 2002, pp. 811-814.
[60] T.-Y. Jea and V. Govindaraju, "A minutia-based partial fingerprint recognition system," Pattern recognition, vol. 38, no. 10, pp. 1672-1684, 2005.
[61] X. Jiang, "On orientation and anisotropy estimation for online fingerprint authentication," IEEE Transactions on Signal Processing, vol. 53, no. 10, pp. 4038-4049, 2005.
[62] D. Maio, D. Maltoni, R. Cappelli, J. L. Wayman, and A. K. Jain, "Fvc2000: Fingerprint verification competition," IEEE transactions on pattern analysis and machine intelligence, vol. 24, no. 3, pp. 402-412, 2002.
[63] T. Uz, G. Bebis, A. Erol, and S. Prabhakar, "Minutiae-based template synthesis and matching for fingerprint authentication," Computer Vision and Image Understanding, vol. 113, no. 9, pp. 979-992, 2009.
[64] R. Cappelli, M. Ferrara, A. Franco, and D. Maltoni, "Fingerprint verification competition 2006," Biometric Technology Today, vol. 15, no. 7-8, pp. 7-9, 2007.
[65] R. Cappelli, M. Ferrara, and D. Maltoni, "Minutia cylinder-code: A new representation and matching technique for fingerprint recognition," IEEE transactions on pattern analysis and machine intelligence, vol. 32, no. 12, pp. 2128-2141, 2010.
[66] D. Maio, D. Maltoni, R. Cappelli, J. L. Wayman, and A. K. Jain, "Fvc2004: Third fingerprint verification competition," in International conference on biometric authentication. Springer, 2004, pp. 1-7.
[67] K. Cao, E. Liu, L. Pang, J. Liang, and J. Tian, "Fingerprint matching by incorporating minutiae discriminability," in 2011 International Joint Conference on Biometrics (IJCB). IEEE, 2011, pp. 1-6.
[68] W. Xu, G. Lan, Q. Lin, S. Khalifa, M. Hassan, N. Bergmann, and W. Hu, "Keh-gait: Using kinetic energy harvesting for gait-based user authentication systems," IEEE Transactions on Mobile Computing, vol. 18, no. 1, pp. 139-152, 2018.
[69] X. Zhang, L. Yao, C. Huang, T. Gu, Z. Yang, and Y. Liu, "Deepkey: A multimodal biometric authentication system via deep decoding gaits and brainwaves," ACM Transactions on Intelligent Systems and Technology (TIST), vol. 11, no. 4, pp. 1-24, 2020.
[70] H. Ji, C. Hou, Y. Yang, F. Fioranelli, and Y. Lang, "A one-class classification method for human gait authentication using micro-doppler signatures," IEEE Signal Processing Letters, vol. 28, pp. 2182-2186, 2021.
[71] "Specification of casia iris image database (ver 1.0)," http://english. ia.cas.cn/db/201610/t20161026_169399.html Chinese Academy of Sciences, accessed: 2024-10-24.
[72] C. S. Chin, A. T. B. Jin, and D. N. C. Ling, "High security iris verification system based on random secret integration," Computer Vision and Image Understanding, vol. 102, no. 2, pp. 169-177, 2006.
[73] "Specification of casia iris image database (ver 3.0)," http://english. ia.cas.cn/db/201610/t20161026_169399.html Chinese Academy of Sciences, accessed: 2024-10-24.
[74] Y.-L. Lai, Z. Jin, A. B. J. Teoh, B.-M. Goi, W.-S. Yap, T.-Y. Chai, and C. Rathgeb, "Cancellable iris template generation based on indexingfirst-one hashing," Pattern Recognition, vol. 64, pp. 105-117, 2017.
[75] A. A. Asaker, Z. F. Elsharkawy, S. Nassar, N. Ayad, O. Zahran, and F. E. Abd El-Samie, "A novel cancellable iris template generation based on salting approach," Multimedia Tools and Applications, vol. 80, pp. 3703-3727, 2021.
[76] F. Kausar, "Iris based cancelable biometric cryptosystem for secure healthcare smart card," Egyptian Informatics Journal, vol. 22, no. 4, pp. 447-453, 2021.
[77] S.-s. Hwang, S. Cho, and S. Park, "Keystroke dynamics-based authentication for mobile devices," Computers \& Security, vol. 28, no. 1-2, pp. 85-93, 2009.
[78] R. Giot, M. El-Abed, and C. Rosenberger, "Greyc keystroke: a benchmark for keystroke dynamics biometric systems," in 2009 IEEE 3rd International Conference on Biometrics: Theory, Applications, and Systems. IEEE, 2009, pp. 1-6.
[79] R. Giot, M. El-Abed, B. Hemery, and C. Rosenberger, "Unconstrained keystroke dynamics authentication with shared secret," Computers \& security, vol. 30, no. 6-7, pp. 427-445, 2011.
[80] Y. Sheng, V. V. Phoha, and S. M. Rovnyak, "A parallel decision treebased method for user authentication based on keystroke patterns," IEEE Transactions on Systems, Man, and Cybernetics, Part B (Cybernetics), vol. 35, no. 4, pp. 826-833, 2005.
[81] K. S. Balagani, V. V. Phoha, A. Ray, and S. Phoha, "On the discriminability of keystroke feature vectors used in fixed text keystroke authentication," Pattern Recognition Letters, vol. 32, no. 7, pp. 1070-1080, 2011.
[82] H. Locklear, S. Govindarajan, Z. Sitová, A. Goodkind, D. G. Brizan, A. Rosenberg, V. V. Phoha, P. Gasti, and K. S. Balagani, "Continuous authentication with cognition-centric text production and revision features," in Ieee international joint conference on biometrics. IEEE, 2014, pp. 1-8.
[83] Y. Sun, H. Ceker, and S. Upadhyaya, "Shared keystroke dataset for continuous authentication," in 2016 IEEE international workshop on information forensics and security (WIFS). IEEE, 2016, pp. 1-6.
[84] X. Lu, S. Zhang, P. Hui, and P. Lio, "Continuous authentication by freetext keystroke based on cnn and rnn," Computers \& Security, vol. 96, p. 101861, 2020.
[85] C. Murphy, J. Huang, D. Hou, and S. Schuckers, "Shared dataset on natural human-computer interaction to support continuous authentication research," in 2017 IEEE international joint conference on biometrics (IJCB). IEEE, 2017, pp. 525-530.
[86] J. Kim and P. Kang, "Freely typed keystroke dynamics-based user authentication for mobile devices based on heterogeneous features," Pattern Recognition, vol. 108, p. 107556, 2020.
[87] I. Stylios, A. Skalkos, S. Kokolakis, and M. Karyda, "Bioprivacy: Development of a keystroke dynamics continuous authentication system," in European Symposium on Research in Computer Security. Springer, 2021, pp. 158-170.
[88] B. Ratner, "The correlation coefficient: Its values range between+ 1/-1, or do they?" Journal of targeting, measurement and analysis for marketing, vol. 17, no. 2, pp. 139-142, 2009.
[89] P. A. Grassi, J. L. Fenton, E. M. Newton, R. Perlner, A. Regenscheid, W. E. Burr, J. P. Richer, N. Lefkovitz, J. M. Danker, Y.-Y. Choong et al., "Digital identity guidelines: Authentication and lifecycle management [includes updates as of 03-02-2020]," 2020.
[90] Frontex, "Best practice technical guidelines for automated border control (abc) systems," 2017. [Online]. Available: https://frontex.europa.eu/assets/Publications/Research/Best_ Practice_Technical_Guidelines_ABC.pdf
[91] A. K. Chaurasia, M. Fallahi, T. Strufe, P. Terhörst, and P. A. Cabarcos, "Neuroidbench: An open-source benchmark framework for the standardization of methodology in brainwave-based authentication research," J. Inf. Secur. Appl., vol. 85, p. 103832, 2024. [Online]. Available: https://doi.org/10.1016/j.jisa.2024.103832


[^0]:    ${ }^{1}$ The name BioQuake was chosen to reflect the potential 'shaking' or variability (Quake) in the observed performance metrics of biometric systems (Bio) due to uncertainty.

[^1]:    ${ }^{2}$ http://i63fallahi.ps.kastel.kit.edu/uncertainty/

[^2]:    ${ }^{3}$ https://www.scimagojr.com/journalrank.php
    ${ }^{4}$ https://portal.core.edu.au/conf-ranks/

[^3]:    ${ }^{5}$ Note that a dataset may be evaluated differently by various recognition systems. In fact, authors might use all possible genuine-impostor pairs or specific subsets of the dataset depending on the evaluation strategy (e.g., reserving certain subsets for training). We consider each configuration as a dataset instance.

