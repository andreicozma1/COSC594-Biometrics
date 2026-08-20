# Personal Identification Based on Iris Texture Analysis 

Li Ma, Tieniu Tan, Senior Member, IEEE, Yunhong Wang, Member, IEEE, and Dexin Zhang


#### Abstract

With an increasing emphasis on security, automated personal identification based on biometrics has been receiving extensive attention over the past decade. Iris recognition, as an emerging biometric recognition approach, is becoming a very active topic in both research and practical applications. In general, a typical iris recognition system includes iris imaging, iris liveness detection, and recognition. This paper focuses on the last issue and describes a new scheme for iris recognition from an image sequence. We first assess the quality of each image in the input sequence and select a clear iris image from such a sequence for subsequent recognition. A bank of spatial filters, whose kernels are suitable for iris recognition, is then used to capture local characteristics of the iris so as to produce discriminating texture features. Experimental results show that the proposed method has an encouraging performance. In particular, a comparative study of existing methods for iris recognition is conducted on an iris image database including 2,255 sequences from 213 subjects. Conclusions based on such a comparison using a nonparametric statistical method (the bootstrap) provide useful information for further research.


Index Terms-Iris recognition, image quality assessment, multichannel spatial filters, texture analysis, biometrics.

## 1 Introduction

THE recent advances of information technology and the increasing requirement for security have led to a rapid development of intelligent personal identification systems based on biometrics. Biometrics [1], [2] employs physiological or behavioral characteristics to accurately identify each subject. Commonly used biometric features include face, fingerprints, voice, facial thermograms, iris, retina, gait, palm-prints, hand geometry, etc. [1], [2]. Of all these biometric features, fingerprint verification has received considerable attention and has been successfully used in law enforcement applications. Face recognition and speaker recognition have also been widely studied over the last 25 years, whereas iris recognition is a newly emergent approach to personal identification [1], [2]. It is reported in [3] that iris recognition is one of the most reliable biometrics.

The human iris, an annular part between the pupil (generally, appearing black in an image) and the white sclera as shown in Fig. 8, has an extraordinary structure and provides many interlacing minute characteristics such as freckles, coronas, stripes, etc. These visible characteristics, which are generally called the texture of the iris, are unique to each subject [5], [6], [7], [12], [15], [16], [17], [18], [19], [20], [21]. Individual differences that exist in the development of anatomical structures in the body result in such uniqueness. Compared with other biometric features (such as face,

- The authors are with the National Laboratory of Pattern Recognition, Institute of Automation, Chinese Academy of Sciences, PO Box 2728, Beijing, P.R. China, 100080.
E-mail: \{lma, tnt, wangyh, dxzhang\}@nlpr.ia.ac.cn.

Manuscript received 16 Oct. 2002; revised 31 May 2003; accepted 6 Aug. 2003.
Recommended for acceptance by M. Pietikainen.
For information on obtaining reprints of this article, please send e-mail to: tpami@computer.org, and reference IEEECS Log Number 117595. voice, etc.), the iris is more stable and reliable for identification [1], [2], [3]. Furthermore, since the iris is an externally visible organ, iris-based personal identification systems can be noninvasive to their users [12], [16], [17], [18], [19], [20], [21], which is of great importance for practical applications. All these desirable properties (i.e., uniqueness, stability, and noninvasiveness) make iris recognition a particularly promising solution to security in the near future.

A typical iris recognition system is schematically shown in Fig. 1. It involves three main modules.

- Image acquisition. It is to capture a sequence of iris images from the subject using a specifically designed sensor. Since the iris is fairly small (its diameter is about 1 cm) and exhibits more abundant texture features under infrared lighting, capturing iris images of high quality is one of the major challenges for practical applications. Fortunately, much work has been done on iris image acquisition [9], [10], [11], [12], [20], [21], which has made noninvasive imaging at a distance possible. When designing an image acquisition apparatus, one should consider three main aspects, namely, the lighting system, the positioning system, and the physical capture system [20]. More recent work on iris imaging may be found on an iris recognition Web site [14].
- Iris liveness detection. Being easy to be forged and used illegally is a crucial weakness of traditional personal identification methods. Similarly, it is also possible that biometric features are forged and illegally used. Iris liveness detection aims to ensure that an input image sequence is from a live subject instead of an iris photograph, a video playback, a glass eye, or other artifacts. However, efforts on iris Published by the IEEE Computer Society

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-02.jpg?height=221&width=984&top_left_y=241&top_left_x=492)
Fig. 1. Block diagram of a typical iris recognition system.

liveness detection are still limited, though iris liveness detection is highly desirable. Daugman [1], [19], and Wildes [21] mentioned this topic in their work, but they only described some possible schemes and did not document a specific method. How to utilize the optical and physiological characteristics of the live eye to implement effective liveness detection remains to be an important research topic.
- Recognition. This is the most key component of an iris recognition system and determines the system's performance to a large extent. Iris recognition produces the correct result by extracting features of the input images and matching these features with known patterns in the feature database. Such a process can be divided into four main stages: image quality assessment and selection, preprocessing, feature extraction, and matching. The first stage solves the problem of how to choose a clear and well-focused iris image from an image sequence for recognition. Preprocessing provides an effective iris region in a selected image for subsequent feature extraction and matching.

In addition to recognition, our work on iris-based personal identification also involves iris sensor design [13] and implementation of a specific method for iris liveness detection based on the two schemes described by Daugman [1], [19]. In this paper, we detail a texture analysis-based recognition method. Experimental results on an iris image database including 2,255 image sequences from 213 subjects have demonstrated that the proposed method is highly feasible and effective for personal identification. The novelty of this paper includes the following:

1. In order to select a suitable image from an image sequence for accurate recognition, an effective scheme for image quality assessment is proposed.
2. A bank of spatial filters, whose kernels are suitable for iris recognition, is defined to capture local details of the iris so as to produce discriminating texture features.
3. Using a nonparametric statistical approach, extensive performance comparison of existing schemes for iris recognition is conducted on a reasonably sized iris database (To the best of our knowledge, this is the first comparative study on iris recognition).

The remainder of this paper is organized as follows: Section 2 briefly summarizes related work. A detailed description of the proposed method for iris recognition is given in Section 3. Section 4 reports experiments and results. Section 5 concludes this paper.

## 2 Related Work

Using iris patterns as an approach to personal identification and verification goes back to the late 19th century [8], [21], but most work on iris recognition [9], [10], [11], [12], [13], [14], [15], [16], [17], [18], [19], [20], [21], [22], [23], [24], [25], [26], [28], [29], [30], [31] is done in the last decade. Existing methods for iris recognition mainly concentrate on iris representation and matching which is also one of the focuses of this paper.

Unlike fingerprints, it is difficult to classify and localize semantically meaningful features in an iris image. From the viewpoint of feature extraction, previous iris recognition methods can be roughly divided into three major categories: phase-based methods [16], [17], [18], [19], zero-crossing representation methods [22], [25], and texture-analysisbased methods [20], [23], [28], [29], [30]. Daugman [17], [18], [19] used multiscale quadrature wavelets to extract texture phase structure information of the iris to generate a 2,048-bit iriscode and compared the difference between a pair of iris representations by computing their Hamming distance. In [24], Sanchez-Reillo and Sanchez-Avila provided a partial implementation of the algorithm by Daugman. Boles and Boashash [22] calculated a zero-crossing representation of 1D wavelet transform at various resolution levels of a concentric circle on an iris image to characterize the texture of the iris. Iris matching was based on two dissimilarity functions. Sanchez-Avila and SanchezReillo [25] further developed the method of Boles and Boashash by using different distance measures (such as Euclidean distance and Hamming distance) for matching. Wildes et al. [20] represented the iris texture with a Laplacian pyramid constructed with four different resolution levels and used the normalized correlation to determine whether the input image and the model image are from the same class. Lim et al. [23] decomposed an iris image into four levels using 2D Haar wavelet transform and quantized the fourth-level high frequency information to form an 87-bit code. A modified competitive learning neural network (LVQ) was used for classification. Our previous work [28], [29] adopted a well-known texture analysis method (multichannel Gabor filtering) to capture both global and local details in an iris. More recently, Tisse et al. [26] constructed the analytic image (a combination of the original image and its Hilbert transform) to demodulate the iris texture. Emergent frequency images used for feature extraction are in essence samples of the phase gradient fields of the analytic image's dominant components [27]. Similar to the algorithm by Daugman, they sampled binary emergent frequency images to form a feature vector and used Hamming distance for matching. It should be noted that all these algorithms are based on gray images, and Authorized licensed use limited to: UNIVERSITY OF TENNESSEE. Downloaded on August 18,2026 at 19:50:25 UTC from IEEE Xplore. Restrictions apply.

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-03.jpg?height=202&width=851&top_left_y=238&top_left_x=103)
Fig. 2. The flowchart of our approach.

color information is not used. The main reason is that the most important information in recognition (i.e., texture variations of the iris) is the same in both gray and color images.

A great deal of progress in iris recognition has been made through these efforts, therefore, a detailed performance comparison of these algorithms is not trivial. Such evaluation will be discussed in Section 4. In this paper, we propose a new iris recognition algorithm based on texture analysis. Of particular concern and importance in this method are image quality assessment, feature extraction, and matching. These very key issues will be addressed in the following section.

## 3 Iris Recognition

In our framework, an iris recognition algorithm includes four basic modules: image quality assessment and selection, preprocessing, feature extraction, and matching. Fig. 2 shows how the proposed algorithm works. The solid boxes are the processed data at different stages and the dashed boxes denote four different processing steps, respectively. Detailed descriptions of these steps are introduced as follows.

### 3.1 Image Quality Assessment and Selection

When capturing iris images, one usually obtains a sequence of images rather than a single image. Unfortunately, not all images in the input sequence are clear and sharp enough for recognition. As shown in the top row of Fig. 3, the second image is out of focus, the third one contains many noticeable interlacing lines (especially in regions close to the boundary) caused by eye motion, and the last one is an example of severe occlusions by eyelids and eyelashes. Therefore, it is necessary to select a suitable image of high quality from an input sequence before all other operations. Image quality assessment is an important issue of iris recognition as the quality of an image strongly affects recognition accuracy. However, efforts on image quality assessment are still limited. Daugman [18] measured the total high frequency power in the 2D Fourier spectrum of an image to assess the focus of the image. If an image can pass a minimum focus criterion, it will be used for recognition. However, Daugman did not provide a detailed description of his method. Zhang and Salganicoff [31] analyzed the sharpness of the boundary between the pupil and the iris to determine whether an image is in focus. Both these methods aim to measure the focus of an iris image. The former is a common approach to focus detection able to be used in various applications, whereas the latter considers the specific properties of the iris image. Here, we present an effective scheme to assess image quality by analyzing the frequency distribution of the iris image. Iris images of low quality can be roughly categorized into three classes, namely, out-of-focus images (also called defocused images), motion blurred images, and images severely occluded by eyelids and eyelashes. When the subject is far from the focus plane of the camera, a defocused image like Fig. 3b will form. If the subject moves during imaging, a motion blurred image as shown in Fig. 3c will result. When the subject opens his eye partially, the resulting image as shown in Fig. 3d contains little useful information. These images often occur in a captured sequence since the eye is in the state of continual motion and noninvasive image acquisition also requires users to adjust their position (hence, body motion).

Here, the region of interest in an image is the iris, and we thus focus on only two iris subregions in the horizontal direction as shown in Fig. 3 for further analysis. That is, we will utilize information of the iris image as much as possible. From the viewpoint of frequency analysis, the spectrum of a defocused iris is greatly dominated by low

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-03.jpg?height=565&width=1190&top_left_y=1912&top_left_x=387)
Fig. 3. Differences between high quality images and low quality images. (a) A clear image. (b) A defocused image. (c) A motion blurred image. (d) An occluded image. (e) Fourier spectra of two local iris regions denoted by the white boxes in (a). (f), (g), and (h) are the Fourier spectra corresponding to (b), (c), and (d), respectively. The quality descriptors of (a), (b), (c), and (d) are $\left[1.65 \times 10^{6}, 0.94\right],\left[1.35 \times 10^{6}, 0.63\right],\left[1.62 \times 10^{6}, 0.55\right]$, and [ $2.39 \times 10^{6}$, 0.85], respectively.

frequency components, and an iris image having the eye partially opened contains significant middle and high frequency components resulted from the heavy eyelashes. As far as motion blurred images are concerned, there are two cases. If the iris sensor works in the interlaced scan mode (i.e., a frame is divided into two fields which are captured in an interval of 20 ms or less), the resulting image as shown in Fig. 3c involves obvious interlacing lines (hereinafter, called aliasing) in the horizontal direction in the boundary regions. Such aliasing corresponding to vertical high frequency components in Fourier spectrum is more noticeable in regions close to the pupil and the eyelashes because the pupil and the eyelashes generally stand in high contrast against their surroundings. If the iris sensor works in the progressive scan mode (i.e., a complete frame is generated in one time), smearing along the motion direction instead of serious aliasing will occur in the image. Different from the former, the second kind of motion blurred images lacks middle and high frequency components and has frequency distribution similar to that of defocused images [32]. In our experiments, motion blurred images belong to the former since our iris sensor only works in the interlaced scan mode. In comparison with these images of low quality, a clear and properly focused iris image has relatively uniform frequency distribution. This can be observed in Fig. 3. We thus define the following quality descriptor:

$$
\begin{aligned}
D & =\left[\left(F_{1}+F_{2}+F_{3}\right) ; \frac{F_{2}}{F_{1}+F_{3}}\right] \\
F_{i} & =\iint_{\Omega=\left\{(u, v) \mid f_{1}^{i}<\sqrt{u^{2}+v^{2}}<=f_{2}^{i}\right\}}|F(u, v)| d u d v \quad i=1,2,3,
\end{aligned}
$$

where $F(u, v)$ is the 2D Fourier spectrum of an iris region, $F_{1}, F_{2}$, and $F_{3}$ are the power of low, middle, and high frequency components, respectively, $f_{1}^{i}$ and $f_{2}^{i}$ are the radial frequency pair and bound the range of the corresponding frequency components. In our experiments, three frequency pairs of (0, 6), (6, 22), and $(22,32)$ are used. The quality descriptor D consists of two discriminating frequency features. The first feature is the total spectrum power of an iris region which can effectively discriminate clear iris images from severely occluded iris images. The second feature is the ratio of the middle frequency power to other frequency power. It should be larger for the clear image than for the defocused and motion blurred image since the former has much more middle frequency information. A complete diagram of the proposed algorithm for quality assessment is plotted in Fig. 4. We first locate two $64 \times 64$ iris regions and compute their quality descriptors, respectively. Then, the mean of the resulting two local quality descriptors is regarded as an appropriate quality measure of an iris image. For a given quality descriptor, the SVM method is used to distinguish whether the corresponding iris image is clear. Here, because defocused images, motion blurred images, and occluded images do not form a compact cluster in the feature space defined by the quality descriptor, we use the SVM method to characterize the distribution boundary of the quality descriptor between low quality images and clear images

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-04.jpg?height=354&width=849&top_left_y=243&top_left_x=1018)
Fig. 4. The flowchart of the proposed method for image quality assessment.

(see Fig. 9). Note that the scheme for coarse localization of the pupil is the same as that introduced in Section 3.2.1.

Using the above algorithm, one can accurately assess the quality of an image. Because the input data is an image sequence in our experiments, we adopt a simple selection scheme as follows:

1. Compute the quality descriptor of each image in the input sequence.
2. Generate a candidate image set where each image should successfully pass the above quality assessment (or the quality descriptor of each image is close to the decision boundary).
3. Select the image whose quality descriptor is the farthest to the decision boundary in all quality descriptors of the candidate images.

The combination of the quality assessment algorithm and the image selection scheme makes sure that an iris image of high quality is identified from the input sequence. In the following sections, we will focus on iris representation and matching based on a single image.

### 3.2 Image Preprocessing

An iris image, as shown in Fig. 5a, contains not only the region of interest (iris) but also some "unuseful" parts (e.g., eyelid, pupil, etc.). A change in the camera-to-eye distance may also result in variations in the size of the same iris. Furthermore, the brightness is not uniformly distributed because of nonuniform illumination. Therefore, before feature extraction,the original image needs to be preprocessed to localize iris, normalize iris, and reduce the influence of the factors mentioned above. Such preprocessing is detailed in the following subsections.

### 3.2.1 Iris Localization

The iris is an annular part between the pupil (inner boundary) and the sclera (outer boundary). Both the inner boundary and the outer boundary of a typical iris can approximately be taken as circles. However, the two circles are usually not concentric [17]. We localize the iris using the following simple but effective method.

1. Project the image in the vertical and horizontal direction to approximately estimate the center coordinates ( $X_{p}, Y_{p}$ ) of the pupil. Since the pupil is generally darker than its surroundings, the coordinates corresponding to the minima of the two nates corresponding to the minima of the two

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-05.jpg?height=844&width=769&top_left_y=234&top_left_x=144)
Fig. 5. Image preprocessing. (a) Original image. (b) Localized image. (c) Normalized image. (d) Estimated background illumination. (e) Normalized image after enhancement.

projection profiles are considered as the center coordinates of the pupil.
2. Binarize a $120 \times 120$ region centered at the point $\left(X_{p}, Y_{p}\right)$ by adaptively selecting a reasonable threshold using the gray-level histogram of this region. The centroid of the resulting binary region is considered as a more accurate estimate of the pupil coordinates. In this binary region, we can also roughly compute the radius of the pupil.
3. Calculate the exact parameters of these two circles using edge detection (Canny operator in experiments) and Hough transform in a certain region determined by the center of the pupil.

In the above method, the first two steps provide an approach to coarse localization of the pupil which can be used in image quality assessment. In experiments, we perform the second step twice for a reasonably accurate estimate. Compared with the localization method by Wildes et al. [20] where the combination of edge detection and Hough transform is also adopted, our method approximates the pupil position before edge detection and Hough transform. This will reduce the region for edge detection and the search space of Hough transform and, thus, result in lower computational demands.

### 3.2.2 Iris Normalization

Irises from different people may be captured in different size and, even for irises from the same eye, the size may change due to illumination variations and other factors. Such elastic deformation in iris texture will affect the results of iris matching. For the purpose of achieving more accurate recognition results, it is necessary to compensate for the iris deformation. Daugman [17], [18], [19] solved this problem by projecting the original iris in a Cartesian coordinate system into a doubly dimensionless pseudopolar coordinate system. The iris in the new coordinate system can be represented in a fixed parameter interval. That is, this method normalizes irises of different size to the same size. Similar to this scheme, we counterclockwise unwrap the iris ring to a rectangular block with a fixed size. Such unwrapping can be denoted as:

$$
\begin{aligned}
& I_{n}(X, Y)=I_{o}(x, y) \\
& x=x_{p}(\theta)+\left(\left(x_{i}(\theta)-x_{p}(\theta)\right) \frac{Y}{M}\right. \\
& y=y_{p}(\theta)+\left(\left(y_{i}(\theta)-y_{p}(\theta)\right) \frac{Y}{M}\right. \\
& \theta=2 \pi X / N,
\end{aligned}
$$

where $I_{n}$ is a $M \times N$ ( $64 \times 512$ in our experiments) normalized image, $\left(x_{p}(\theta), y_{p}(\theta)\right)$ and $\left(x_{i}(\theta), y_{i}(\theta)\right)$ are the coordinates of the inner and outer boundary points in the direction $\theta$ in the original image $I_{o}$. The normalization not only reduces to a certain extent the iris distortion caused by pupil movement but also simplifies subsequent processing.

### 3.2.3 Image Enhancement

The normalized iris image has low contrast and may have nonuniform brightness caused by the position of light sources. All these may affect the subsequent processing in feature extraction and matching. In order to obtain a more well-distributed texture image, we first approximate intensity variations across the whole image. The mean of each 16 × 16 small block constitutes a coarse estimate of the background illumination. This estimate is further expanded to the same size as the normalized image by bicubic interpolation. The estimated background illumination as shown in Fig. 5d is subtracted from the normalized image to compensate for a variety of lighting conditions. Then, we enhance the lighting corrected image by means of histogram equalization in each $32 \times 32$ region. Such processing compensates for the nonuniform illumination, as well as improves the contrast of the image. Fig. 5e shows the preprocessing result of an iris image, from which we can see that finer texture characteristics of the iris become clearer than those in Fig. 5c.

### 3.3 Feature Extraction

The iris has a particularly interesting structure and provides abundant texture information. So, it is desirable to explore representation methods which can capture local underlying information in an iris. From the viewpoint of texture analysis, local spatial patterns in an iris mainly involve frequency and orientation information. Generally, the iris details spread along the radial direction in the original image corresponding to the vertical direction in the normalized image (see Figs. 7 and 8). As a result, the differences of orientation information among irises seem to be not significant. That is, frequency information should account for the major differences of irises from different people. We thus propose a scheme to capture such discriminating frequency information which reflects the local structure of the iris. In general, the majority of useful information of the iris is in a frequency band of about three octaves [18]. Therefore, a bank of filters is constructed to reliably acquire such information in the spatial domain. As reliably acquire such information in the spatial domain. As

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-06.jpg?height=853&width=1418&top_left_y=241&top_left_x=279)
Fig. 6. The responses of the filters defined in (3). (a) The defined filter with $\delta_{x}=\delta_{y}$. (b) The defined filter with $\delta_{x}>\delta_{y}$. (c) Gabor filter. (d), (e), and (f) are the Fourier spectra of (a), (b), and (c), respectively.

we know, coefficients of the filtered image effectively indicate the frequency distribution of an image. Two statistic values are thus extracted from each small region in the filtered image to represent local texture information of the iris. A feature vector is an ordered collection of all features from the local regions. More details of this algorithm are presented as follows.

### 3.3.1 Spatial Filters

In the spatial domain, one can extract information of an image at a certain orientation and scale using some specific filters, such as Gabor filters [33], [34], [35], [36], [37]. Recently, Gabor filter based methods have been widely used in computer vision, especially for texture analysis [35], [36], [37]. Gabor elementary functions are Gaussians modulated by oriented complex sinusoidal functions. Here, according to the characteristics of the iris texture, we define new spatial filters to capture local details of the iris. The difference between Gabor filter and the defined filter lies in the modulating sinusoidal function. The former is modulated by an oriented sinusoidal function, whereas the latter by a circularly symmetric sinusoidal function. Their kernels

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-06.jpg?height=370&width=862&top_left_y=2215&top_left_x=95)
Fig. 7. ROIs from three iris samples (after preprocessing).

are given as follows (here, we only consider evensymmetric Gabor filters):

$$
\begin{aligned}
& G(x, y, f)=\frac{1}{2 \pi \delta_{x} \delta_{y}} \exp \left[-\frac{1}{2}\left(\frac{x^{2}}{\delta_{x}^{2}}+\frac{y^{2}}{\delta_{y}^{2}}\right)\right] M_{i}(x, y, f) ; i=1,2 . \\
& M_{1}(x, y, f)=\cos \left[2 \pi f\left(\sqrt{x^{2}+y^{2}}\right)\right] \\
& M_{2}(x, y, f)=\cos [2 \pi f(x \cos \theta+y \sin \theta)],
\end{aligned}
$$

where $M_{i}(x, y, f)$ denotes the modulating function, $M_{1}$ and $M_{2}$ are the modulating function of the defined filter and Gabor filter, respectively, $f$ is the frequency of the sinusoidal function, $\delta_{x}$ and $\delta_{y}$ are the space constants of the Gaussian envelope along the $x$ and $y$ axis, respectively, and $\theta$ denotes the orientation of Gabor filter. For the defined filter, when $\delta_{x}$ equals to $\delta_{y}$ (i.e., Gaussian function is isotropic), one can obtain a bandpass filter with a specific center frequency. When $\delta_{x}$ and $\delta_{y}$ are different, it not only considers information from every orientation but also

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-06.jpg?height=402&width=862&top_left_y=2118&top_left_x=1010)
Fig. 8. Iris samples. Images in the first row are from both eyes of two Chinese, and the first two in the second row are from Chinese and the last two from French.

Authorized licensed use limited to: UNIVERSITY OF TENNESSEE. Downloaded on August 18,2026 at 19:50:25 UTC from IEEE Xplore. Restrictions apply.
shows more interest in information in $x$ or $y$ direction (determined by $\delta_{x}$ and $\delta_{y}$ ). This is greatly different from a Gabor filter which can only provide information of an image at a certain orientation. Fig. 6 clearly shows the differences between a Gabor filter and the defined spatial filter. As mentioned earlier, local details of the iris generally spread along the radial direction, so information density in the angular direction corresponding to the horizontal direction in the normalized image is higher than that in other directions, which is validated by our experimental results in Section 4.3. Thus, we should pay more attention to useful information in the angular direction. The defined filter can well satisfy such requirements of iris recognition. In other words, the defined kernel is suitable for iris recognition.

In our experiments, we find that the upper portion of a normalized iris image (corresponding to regions closer to the pupil) provides the most useful texture information for recognition (see Fig. 7). In addition, eyelids and eyelashes rarely occlude this section. So, we extract features only in this section (called region of interest, ROI) shown as the region above the dotted line in Fig. 7. As mentioned above, useful iris information distributes in a specific frequency range. We therefore use the defined spatial filters in two channels to acquire the most discriminating iris features. $\delta_{x}$ and $\delta_{y}$ used in the first channel are 3 and 1.5, and the second channel 4.5 and 1.5. In a much shorter version of this method in [30], we vertically divided the ROI into three subregions of the same size and estimated the energy of each subregion within a frequency band. These energy measures were used as features. In contrast, using multiple filters with different frequency response for the entire ROI can generate more discriminating features since different irises have distinct dominant frequencies.This means that the improved scheme would be more effective than our earlier one [30].

### 3.3.2 Feature Vector

According to the above scheme, filtering the ROI (48 × 512) with the defined multichannel spatial filters results in

$$
F_{i}(x, y)=\iint I\left(x_{1}, y_{1}\right) G_{i}\left(x-x_{1}, y-y_{1}\right) d x_{1} d y_{1} ; \quad i=1,2,
$$

where $G_{i}$ is the $i$ th channel of the spatial filters, $I(x, y)$ denotes the ROI, and $F_{i}(x, y)$ is the filtered image. To characterize local texture information of the iris, we extract statistical features in each 8 × 8 small block of the two filtered images. In our experiments, the total number of small blocks is $768[(48 \times 512) /(8 \times 8) \times 2]$. For each small block, two feature values are captured. This generates 1,536 feature components. The feature values used in the algorithm are the mean $m$ and the average absolute deviation $\sigma$ of the magnitude of each filtered block defined as

$$
m=\frac{1}{n} \sum_{w}\left|F_{i}(x, y)\right|, \quad \sigma=\frac{1}{n} \sum_{w}| | F_{i}(x, y)|-m|,
$$

where $w$ is an 8 × 8 block in the filtered image, $n$ is the number of pixels in the block $w$, and $m$ is the mean of the block $w$. These feature values are arranged to form a 1D feature vector

$$
V=\left[m_{1}, \sigma_{1}, m_{2}, \sigma_{2} \ldots m_{768}, \sigma_{768}\right]^{\mathrm{T}} .
$$

### 3.4 Iris Matching

After feature extraction, an iris image is represented as a feature vector of length 1,536. To improve computational efficiency and classification accuracy, Fisher linear discriminant is first used to reduce the dimensionality of the feature vector and then the nearest center classifier is adopted for classification.

Two popular methods for dimensionality reduction are principal component analysis and Fisher linear discriminant. Compared with principal component analysis, Fisher linear discriminant not only reduces the dimensionality of features but also increases class separability by considering both information of all samples and the underlying structure of each class. This is also the reason that Wildes et al. [20] adopted Fisher linear discriminant rather than general distance measures for iris matching (though the feature vector includes only four components in their method). Fisher linear discriminant searches for projected vectors that best discriminate different classes in terms of maximizing the ratio of between-class to withinclass scatter. Further details of Fisher linear discriminant may be found in [38], [39].

The new feature vector $f$ can be denoted as:

$$
f=W^{T} V,
$$

where $W$ is the projection matrix and $V$ is the original feature vector derived in Section 3.3.2. The proposed algorithm employs the nearest center classifier defined in (8) for classification in a low-dimensional feature space.

$$
\begin{aligned}
& m=\arg \min _{1 \leq i \leq c} d_{n}\left(f, f_{i}\right) ; \quad n=1,2,3 . \\
& d_{1}\left(f, f_{i}\right)=\sum_{j}\left|f^{j}-f_{i}^{j}\right| \\
& d_{2}\left(f, f_{i}\right)=\sum_{j}\left(f^{j}-f_{i}^{j}\right)^{2} \\
& d_{3}\left(f, f_{i}\right)=1-\frac{f^{T} f_{i}}{\|f\|\left\|f_{i}\right\|},
\end{aligned}
$$

where $f$ and $f_{i}$ are the feature vector of an unknown sample and the $i$ th class, respectively, $f^{j}$ and $f_{i}^{j}$ are the $j$ th component of the feature vector of the unknown sample and that of the $i$ th class, respectively, $c$ is the total number of classes, $\|\bullet\|$ indicates the Euclidean norm, $d_{n}\left(f, f_{i}\right)$ denotes similarity measure, $d_{1}, d_{2}$, and $d_{3}$ are $\mathrm{L}_{1}$ distance measure, $\mathrm{L}_{2}$ distance measure (i.e., Euclidean distance) and cosine similarity measure, respectively. The feature vector $f$ is classified into the $m$ th class, the closest mean, using similarity measure $d_{n}\left(f, f_{i}\right)$.

It is desirable to obtain an iris representation invariant to translation, scale, and rotation. In our algorithm, translation invariance and approximate scale invariance are achieved by normalizing the original image at the preprocessing step. Most existing schemes achieve approximate rotation invariance either by rotating the feature vector before matching [17], [18], [19], [22], [24], [26], or by registering the input

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-08.jpg?height=595&width=1442&top_left_y=241&top_left_x=264)
Fig. 9. The distributions of the quality descriptor for different types of images.

image with the model before feature extraction [20]. Since features in our method are projection values by feature reduction, there is no explicit relation between features and the original image. We thus obtain approximate rotation invariance by unwrapping the iris ring at different initial angles. Considering that the eye rotation is not very large in practical applications,these initial angle values are -9, -6, -3, 0, 3, 6, and 9 degrees. This means that we define seven templates which denote the seven rotation angles for each iris class in the database. When matching the input feature vector with the templates of an iris class, the minimum of the seven scores is taken as the final matching distance.

## 4 Experiments

This paper presents a new method for identifying individuals from an iris image sequence. We thus perform a series of experiments to evaluate its performance. Moreover, we compare the proposed method with some existing methods for iris recognition and present detailed discussions on the overall experimental results.

Evaluating the performance of biometric algorithms is a difficult issue since it is greatly influenced by all sources of noise (such as sensor noise and environment noise), the test database and the evaluation method. Obviously, it is impossible to model all noise sources and build a test data set including biometric samples from all subjects in the world. Thus, using modern statistical methods to measure the performance of biometric algorithms is a desirable approach. In this paper, the bootstrap [43], which provides a powerful approach to estimating the underlying distribution of the observed data using computer-intensive methods, is adopted to estimate the error rates of a biometric method. The bootstrap can infer how much variation in performance measures resulted from a limited data set can be expected in a larger subject population using confidence intervals of performance measures. The bootstrap is in nature a nonparametric empirical method. Given that we have an original sample $x$ including n observed data $\left\{x_{1}, x_{2}, \ldots, x_{n}\right\}$ from an unknown probability distribution $F$, we can empirically estimate the distribution $F$ and some characteristics of interest $\theta(F)$ associated with $F$ by the bootstrap. A key step in the bootstrap is to generate thousands of random samples $x^{*}=\left\{x_{1}^{*}, x_{2}^{*}, \ldots, x_{n}^{*}\right\}$ (called bootstrap samples) with the same size as the original sample $x$ by drawing with replacement. Using the resulting bootstrap samples, one can easily estimate the statistics of interest. More details of the bootstrap may be found in [40], [41], [43].

We exploit both interval estimation (a confidence interval) and commonly used point estimation (only a numerical value) of statistical measures to characterize the performance of the methods for iris recognition. This means that the evaluation is more accurate and effective. The proposed algorithm is tested in two modes: identification (i.e., one-to-many matching) and verification (i.e., one-toone matching). In identification mode, the algorithm is measured by Correct Recognition Rate (CRR), the ratio of the number of samples being correctly classified to the total number of test samples. In verification mode, the Receiver Operating Characteristic (ROC) curve is used to report the performance of the proposed method. The ROC curve is a False Match Rate (FMR) versus False NonMatch Rate (FNMR) curve [3], [4] which measures the accuracy of matching process and shows the overall performance of an algorithm. The FMR is the probability of accepting an imposter as an authorized subject and the FNMR is the probability of an authorized subject being incorrectly rejected. Points on this curve denote all possible system operating states in different trade offs.

### 4.1 Image Database

Unlike fingerprints and face, there is no common iris database of a reasonable size. Most existing methods for iris recognition used small image sets for performance evaluation, and only the method by Daugman has been tested on a larger image set involving over 200 subjects [3], [19]. Currently, there is also no detailed comparison among the methods in [16], [17], [18], [19], [20], [21], [22], [23], [24], [25], [26], [28], [29], [30]. So, we construct an iris image database named CASIA Iris Database to compare their performance and provide detailed discussions as well. The CASIA Iris Database includes 2,255 iris image sequences from 213 subjects (note that this is currently the largest iris database we Authorized licensed use limited to: UNIVERSITY OF TENNESSEE. Downloaded on August 18,2026 at 19:50:25 UTC from IEEE Xplore. Restrictions apply.

TABLE 1
CASIA Iris Database
| Subjects |  | Age and Gender |  | Time Interval | Environment |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Chinese | 95.3\% | Age < 25 | 41\% | At lease one month between two capture stages | Normal office conditions (indoor) |
|  |  | 25 < = Age < 50 | 55\% |  |  |
| Others | 4.7\% | Age >=50 | 4\% |  |  |
|  |  | Male : Female | 7 : 3 |  |  |


can find in the public domain). Each sequence of the CASIA Iris Database contains 10 frames acquired in about half a second. All images are captured using a homemade digital optical sensor [13]. This sensor works in PAL mode (i.e., 25 frames/second) and provides near infrared illumination under which the iris exhibits more abundant texture features. The subject needs to position himself about 4 cm in front of the sensor to obtain a clear iris image. Moreover, a surface-coated semitransparent mirror is placed in front of the lens so that a person can see and keep his eye in the center of the sensor. The captured iris images are 8-bit gray images with a resolution of $320 \times 280$. In general, the diameter of the iris in an image from our database is greater than 200 pixels. This makes sure that there is enough texture information for reliable recognition. During image acquisition, short-sighted subjects are requested to take off their eyeglasses to obtain high quality iris images. However, contact eyewears are an exception. In our database, about 5.2 percent of the subjects wear contacts. The profile of the database is shown in Table 1. The subjects consist of 203 members of the CAS Institute of Automation and 10 visiting students from Europe.

The CASIA Iris Database is gradually expanded to contain more images from more subjects. Currently, it is composed of two main parts. The first one (namely our earlier database [29]) contains 500 sequences from 25 different people. Each individual provides 20 sequences (10 for each eye) captured in two different stages. In the first stage, five sequences of each eye are acquired. Four weeks later, five more sequences of each eye are obtained. The other part contains 1,755 sequences from 188 subjects, which form 256 iris classes (note that not every individual provides iris image sequences of both eyes). These sequences are captured in three stages. In the first stage, three image sequences of each eye are obtained. One month later, at least two sequences of each eye are captured (often three or four sequences per eye). In the third stage (i.e., three months later), 30 out of 188 subjects provide 138 sequences again. The total number of iris classes is thus 306 (2 × 25 + 256). Since all existing methods for iris recognition only use one image for matching, we make use of the proposed scheme for image quality assessment and selection described in Section 3.1 to form an image set for algorithm comparison. The resulting set includes 2,255 images corresponding to 306 different classes. Some samples from this set are shown in Fig. 8.

### 4.2 Performance Evaluation of Image Quality Assessment

In order to evaluate the performance of the proposed algorithm for image quality assessment, we manually collect 982 clear images, 475 motion blurred images, 431 occluded images, and 429 defocused images from the CASIA Iris Database. One third of each image class are used for training and the rest for testing. Fig. 9 shows the distributions of the quality descriptor for different types of images in training and testing stages and the two axes respectively denote two feature components of the quality descriptor (see (1) for definition).

From this figure, we can draw the following conclusions:

1. The clear images are well clustered and separated from images from the other three classes, indicating good discriminating power of the defined quality descriptor. This is further confirmed by the results shown in Table 2.
2. Severely occluded iris images are rich in middle and high frequency components caused by the eyelashes, which is an important factor in discriminating such images from clear images. The results in Fig. 9 confirm this observation.
3. The quality descriptors of motion blurred images are similarly distributed as those of defocused images. The former include many high frequency components in the vertical direction inherently caused by the scan mode of the CCD camera, whereas the latter are governed by low frequency components. Since they all lack middle frequency components, the corresponding ratios of middle frequency power to other frequency power are close.

Table 2 illustrates the classification results for the training and testing samples. The results clearly demonstrate the effectiveness of the proposed scheme for image quality assessment. Both Daugman's method [18] (measuring the total high frequency power of the Fourier spectrum of an iris image) and the method by Zhang and Salganicoff [31] (detecting the sharpness of the pupil/iris boundary) concentrate on assessing the focus of an iris image.

TABLE 2
Classification Results
| Image set | Clear | Defocused | Occluded | Motion blurred | Total |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Training | 97.86 | 100 | 99.30 | 98.73 | 98.70 |
| Testing | 97.25 | 99.65 | 98.61 | 97.79 | 98.06 |


TABLE 3
Recognition Results Using Different Similarity Measures
| Similarity measure | Correct recognition rate (\%) |  |
| :--- | :--- | :--- |
|  | Original feature set | Reduced feature set |
| $L_{7}$ distance measure | 99.11 | 98.30 |
| $L_{2}$ distance measure | 98.95 | 98.14 |
| Cosine similarity measure | 99.19 | 99.43 |


However, our algorithm can discriminate clear images from not only defocused images but also from motion blurred images and severely occluded images. The results indicate that the proposed scheme should be highly feasible in practical applications.

### 4.3 Experimental Results of Iris Recognition

For each iris class, we choose three samples taken at the first session for training and all samples captured at the second and third sessions serve as test samples. This is also consistent with the widely accepted standard for biometrics algorithm testing [3], [4]. Therefore, there are 918 images for training and 1,237 images for testing (To satisfy requirement of using images captured in different stages for training and testing, respectively, 100 images taken at the first session are not used in the experiments). Computing a point estimation of a performance measure has been extensively adopted in pattern recognition and is also easy to use. Here, it is necessary to briefly introduce how we obtain the interval estimation of a performance measure using the bootstrap. In our experiments, the CRR, FMR, and FNMR are three performance measures. A major assumption of the bootstrap for estimating an unknown distribution $F$ is that the observations $\left\{x_{1}, x_{2} \ldots x_{n}\right\}$ in an original sample $x$ are independent and identically distributed. But often, the case is just the contrary. With the FNMR as an example, if more than one matching pair per iris class is available in the known sample (i.e., at least two test samples per class), the observed data is dependent. Moreover, the bootstrap demands sampling with replacement from $n$ observations of the known sample to form thousands of bootstrap samples. This implies that the observed data in a bootstrap sample is a subset of the original observations. To satisfy these two requirements of the bootstrap, we compute confidence intervals of performance measures as follows:

1. Construct a template set including 306 different classes using 918 iris images.
2. Create a test set containing 306 iris classes by drawing known iris classes with replacement. This means that one iris class likely appears multiple times in the test set.
3. For each iris class in the resulting test set, only one test sample is chosen at random from all available test samples of this class.
4. Compute the CRR, FMR, and FNMR using the constructed template and test set.
5. Repeat Steps 2, 3, and 4 5,000 times and then, respectively, estimate the 95 percent confidence intervals of the CRR, FMR, and FNMR by the percentile method [40].

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-10.jpg?height=464&width=606&top_left_y=241&top_left_x=1139)
Fig. 10. Recognition results using features of different dimensionality.

The percentile method establishes a $(1-2 a) 100$ percent confidence interval by computing the accumulated probability of a probability distribution from both sides. If the accumulated probability exceeds $a$ in $l$ on left side and in $u$ on right side, the confidence interval is $[l, u]$. In the following results, if the performance measure is denoted by only a numerical value, this says that all 1,237 test samples are used to estimate this measure. If the performance measure is expressed by a confidence interval, this means that we adopt the bootstrap method described above to calculate this interval.

### 4.3.1 Choice of Similarity Measures

Similarity measures play an important role in iris matching. We thus perform a series of experiments to select a suitable similarity measure for texture features generated by the proposed method. Table 3 shows the recognition results obtained with three typical measures based on the original features and the dimensionality-reduced features, respectively. The dimensionality of the reduced feature vector is 200, whereas that of the original feature vector is 1,536.

As shown in Table 3, the three similarity measures lead to very similar results when the original features are used and the method's performance does not vary drastically after dimensionality reduction. This demonstrates that both dimensionality reduction and similarity measures have very small impact on recognition accuracy. The results also show that the cosine similarity measure is slightly better than the other two. Fig. 10 describes variations of the recognition rate with changes of dimensionality of the reduced feature vector using the cosine similarity measure. From this figure, we can see that with increasing dimensionality of the reduced feature vector, the recognition rate also increases rapidly. However, when the dimensionality of the reduced feature vector is up to 150 or higher, the recognition rate starts to level off at an encouraging rate of about 99.27 percent. In particular, our method achieves a recognition rate of 99.43 percent using only 200 features. In the subsequent experiments, we utilize 200 features and the cosine similarity measure for matching.

### 4.3.2 Recognition Results

We evaluate the proposed algorithm in two modes, identification and verification. In identification tests, an overall correct recognition rate of 99.43 percent is achieved using all test samples and the corresponding 95 percent Authorized licensed use limited to: UNIVERSITY OF TENNESSEE. Downloaded on August 18,2026 at 19:50:25 UTC from IEEE Xplore. Restrictions apply.

TABLE 4
False Match and False Nonmatch Rates with Different Threshold Values
| Threshold | False match rate (\%) | False non-match rate (\%) |
| :--- | :--- | :--- |
| 0.446 | 0.001 [0, 0.003] | 1.54 [0.327, 2.288] |
| 0.472 | 0.01 [0.004, 0.017] | 1.29 [0.327, 2.288] |
| 0.502 | 0.1 [0.078, 0.122] | 0.97 [0, 1.961] |


confidence interval is [98.37 percent, 100 percent]. The black lines of Fig. 13 show the verification results using the ROC curve with confidence intervals. Table 4 lists three typical system operating states in verification. In particular, if one and only one false match occurs in 100,000 trails, one can predict that the false nonmatch rate is less than 2.288 percent with a 95 percent confidence. These results are highly encouraging and indicate high performance of the proposed algorithm.

### 4.3.3 Performance Evaluation of the Defined Spatial Filter

The spatial filter defined in Section 3.3.1 is thought to be highly suitable for iris recognition since it is constructed based on the observations about the characteristics of the iris. This is confirmed by our experimental results shown in Fig. 11. Filters used in our experiments include well-known directional filters (i.e., Gabor filters in the horizontal direction) and the defined spatial filters using the same parameters as Gabor filters. Similar to the scheme for showing the ROC curve with confidence intervals in [42], we denote confidence intervals of the FMR and FNMR, respectively. Fig. 11 shows the verification results of the proposed method using different filters, which reveals that the defined filters outperform Gabor filters. Gabor filters only capture iris information in the horizontal direction, whereas the defined filters not only show interest in information in the horizontal direction but also consider information from other directions. That is, the latter can obtain more information for recognition. The results also show that one can achieve good results using Gabor filters in the horizontal direction. This indicates that information in the horizontal direction in a normalized iris is more discriminating than that in other directions, namely, higher information density in the angular direction in an original image. We find from Fig. 11 that there is considerable overlap in the FNMR confidence intervals on the two ROC curves. This is because both the defined filters and Gabor filters used in our experiments aim to capture discriminating iris information in the horizontal direction. The defined filters, however, make effective use of more information in other directions, which results in higher accuracy. The above results demonstrate that iris information in the angular direction has higher discriminability and information in other directions is a helpful supplement for more accurate recognition.

### 4.3.4 Comparison with Existing Methods

The previous methods [17], [18], [19], [20], [21], [22], [23], [24], [25], [26], [27], [28], [29], [30], [31] for iris recognition mainly focus on feature representation and matching. Therefore, we only analyze and compare the accuracy and efficiency of feature representation and matching of these methods. The methods proposed by Daugman [18], Wildes et al. [20], Boles and Boashash [22] are probably the best-known. They characterize local details of the iris based on phase, texture analysis and zero-crossing representation respectively. Here, we will present a detailed comparison between the current method and their methods (and our previous work) described in [18], [20], [22], [29], [30] on the CASIA Iris Database. For the purpose of comparison, we implement these methods according to the published papers [12], [16], [17], [18], [19], [20], [21], [22]. Because the method by Wildes et al. [20] only works in verification mode, we do not test the performance of this method in identification mode. Table 5 and Fig. 12 show the identification results, and Fig. 13 describes the verification results.

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-11.jpg?height=623&width=1371&top_left_y=1901&top_left_x=301)
Fig. 11. Performance comparison of the defined filters and Gabor filters. The left and right plots show the 95 percent confidence interval (CI) of the FMR and FNMR, respectively. The solid lines denote the bounds of the CI derived by the bootstrap and the dash-dot lines are the ROC curves based on all test samples.
Authorized licensed use limited to: UNIVERSITY OF TENNESSEE. Downloaded on August 18,2026 at 19:50:25 UTC from IEEE Xplore. Restrictions apply.

TABLE 5
Identification Results
| Methods | Correct recognition rate (\%) |
| :--- | :--- |
| Daugman [18] | 100 [100, 100] |
| Boles [22] | 92.64 [89.22, 95.10] |
| Previous [29] | 94.91 [90.85, 96.41] |
| Previous [30] | 99.19 [98.04, 100] |
| Proposed | 99.43 [98.37, 100] |


Using the bootstrap, we can approximately predict the recognition rate distributions of these methods for a larger test population. Fig. 12 shows the estimated distributions for our previous methods, Boles's method and the proposed method. Table 5 gives the 95 percent confidence intervals of these methods. Since Daugman's method obtains 100 percent recognition rate, we do not plot its probability distribution (the probability of 100 percent recognition rate is 1) in Fig. 12 in order to express the differences of other distributions more clearly. Looking at the results shown in Table 5 and Fig. 12, we can find that Daugman's method has the best performance, followed by the proposed method and the methods described in [30], [29], and [22], respectively. This conclusion is further consolidated by the verification results given in Fig. 13.

Fig. 13 shows the ROC curves with confidence intervals for these methods. The left and right plots show the 95 percent confidence interval (CI) of the FMR and FNMR, respectively. The solid lines denote the bounds of the CI derived by the bootstrap and the dash-dot lines are the

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-12.jpg?height=520&width=750&top_left_y=241&top_left_x=1063)
Fig. 12. Distributions of correct recognition rates.

ROC curves using all test samples. Fig. 13 not only indicates the performance of different methods but also provides information of how much the performance of a given method can vary. In general, the confidence interval of the FMR is smaller than that of the FNMR since one can obtain more nonmatching pairs (for estimating the FMR) than matching pairs (for estimating the FNMR) in experiments. We divide these methods into two groups and, respectively, show the results in the top and bottom plots in Fig. 13 in order to improve the legibility of the plots. The first group includes [22] and [29], and the second [18], [20], [30] and the proposed method. Two observations can be made from Fig. 13. First, in terms of performance, a clear ranking for these methods from best to worst is as follows: Daugman's

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-12.jpg?height=1063&width=1317&top_left_y=1521&top_left_x=329)
Fig. 13. ROC curves with confidence intervals.
Authorized licensed use limited to: UNIVERSITY OF TENNESSEE. Downloaded on August 18,2026 at 19:50:25 UTC from IEEE Xplore. Restrictions apply.

method, the proposed method, our previous method [30], Wildes's method, our previous method [29], and Boles's method. Second, Boles's method is close to our previous method [29] and they are much worse than the other methods. The above results show that the proposed method is only inferior to Daugman's method and much better than the others.

Fig. 13 also shows that there is overlap in some of the FNMR confidence intervals on the ROC curves, especially among Daugman's method, the proposed method, and our earlier one [30]. As we know, the intraclass and the interclass distance distributions jointly determine the verification performance of an algorithm. That is, the ROC curve is directly related to these two distance distributions. In the experiments, we learned that large matching scores from the intraclass distribution and small nonmatching scores from the interclass distribution result in the observed overlap in Fig. 13 (assume that the intraclass distance is less than the interclass distance). Large matching scores which correspond to false nonmatch pairs are mainly caused by occlusions of eyelids and eyelashes, inaccurate localization, and pupil movement (hence, iris distortion). Small nonmatching scores which correspond to false match pairs are decided to a greater extent by the inherent discrimination ability of a method. If test samples include some images which can lead to large matching scores or small nonmatching scores, the ROC curve of a method will inevitably deteriorate. Large matching scores can affect all algorithms (our current comparison experiments do not include eyelid and eyelash detection. To reduce false nonmatching caused by large matching scores, we are working on eyelid and eyelash detection, more accurate localization and more effective normalization.). However, small nonmatching scores depend on the specific iris representation. The observed overlap indicates that the discrimination ability of a given method may slightly vary with the iris characteristics (hence, test samples). For example, for iris images containing very few distinct characteristics, the texture analysis based methods have a relatively low accuracy. If test samples do not include such images, both the proposed method and the method in [30] can also achieve a quite high performance as shown in Fig. 13. Based on the above analysis, we can conclude that the range of a performance measure's confidence intervals reflects the corresponding method's dependence on test samples (the wider the range is, the stronger the dependence should be) and that the overlap in performance measures' confidence intervals among different methods implies that the performance of these methods can be almost the same on some specific test samples (the larger the overlap is, the closer the performance). Considering these two points, we can maintain the above performance ranking for the six methods shown in Fig. 13.

Our previous method [29] divided the normalized iris into eight blocks of the same size (64 × 64) and represented the texture of each block using Gabor filters at five scales and four directions. This implies that it captures less local texture information of the iris. Boles et al. only employed extremely little information along a concentric circle on the iris to represent the whole iris, which resulted in a lower accuracy as shown in Fig. 13. Different from these two methods, our current method captures much more local information. Lim et al. [23] made use of the fourth-level high frequency information of 2D Haar wavelet decomposition of an iris image for feature extraction. As we know, the fourth-level details of an image's wavelet decomposition contain essentially very low frequency information. That is, their method did not effectively exploit middle frequency components of the iris which play an important role in recognition as well. Moreover, iris features in their method are variant to eye rotation as the discrete wavelet transform is not translation invariant. When there is a rotation between a pair of irises from the same subject, their method will generate a false nonmatch. Therefore, there is no reason to expect that their method outperforms ours. The proposed method is a significant extension of our earlier algorithm presented in [30]. Compared with this earlier method, the current method utilizes multichannel spatial filters to extract texture features of the iris within a wider frequency range. This indicates that the extracted features are more discriminating, and the current method thus achieves higher accuracy. Wildes et al. made use of differences of binomial low-pass filters (isotropic Gaussian filters) to achieve overall bandpass iris representation, whereas we design more suitable spatial filters for recognition according to the iris characteristics. This leads to better performance of our method. Furthermore, their method relies on image registration and matching and is computationally demanding. In both identification and verification tests, Daugman's method is slightly better than the proposed method. It should be noted that these two methods explore different schemes to represent an iris. We extract local characteristics of the iris from the viewpoint of texture analysis, whereas Daugman used phase information to represent local shape of the iris details. In essence, Daugman analyzed the iris texture by computing and quantizing the similarity between the quadrature wavelets and each local region, which requires that the size of the local region must be small enough to achieve high accuracy. Therefore, the dimensionality of the feature vector (2,048 elements) in Daugman's method is far higher than ours (200 elements). That is, his method captures much more information in much smaller local regions, which makes his method better than ours.

### 4.4 Discussions and Future Work

Based on the above results and analysis, we can draw a number of conclusions as well as find that some issues need to be further investigated.

1. The proposed scheme for iris image quality assessment is quite feasible. It can effectively deal with the defocused, motion blurred, and occluded images. The motion blurred images used in our experiments are captured by an iris sensor working in the interlaced scan mode. As stated in Section 3.1, the motion blurred images taken by an iris sensor working in the progressive scan mode are expected to have similar frequency distribution to the defocused images. However, such an expectation need to be further verified using real images.

2. The comparison experiment described in Section 4.3.3 reveals that information along the angular direction is highly discriminating for recognition, which is consistent with the implicit reports by Daugman in [18]. We construct new multichannel spatial filters according to such a distinct distribution of the iris details and the proposed method is thus expected to achieve a satisfying recognition accuracy. In fact, our current method achieves the best performance among the existing methods based on texture analysis [20], [21], [23], [28], [29], [30].
3. Table 5 and Figs. 12 and 13 show that the proposed algorithm is only worse than Daugman's method. Increase of the dimensionality of the feature vector improves the recognition accuracy of our method but it does not outperform Daugman's method. By analyzing these two algorithms carefully, it is not difficult to find that different viewpoints for feature representation determine their differences in performance. Phase information characterized by Daugman reflects in essence local shape features of the iris, whereas texture features used by us denote statistical frequency information of a local region. By careful examination on the appearance of numerous iris images, we learn that a remarkable and important characteristic of the iris is the randomly distributed and irregular details. Local shape features are thus expected to better represent such iris details than texture features. The experimental results and analysis have indicated that local shape features could be more discriminating iris features. We are currently working on representing the iris characteristics using the shape description method in order to achieve higher accuracy.
4. The number and the class of iris samples used in our experiments are of a reasonable size. Therefore, the conclusions using the statistical bootstrap method based on such a data set are useful for both research and applications. We intend to expand our iris database to include much more iris image sequences from more races and make it publicly available to promote research on iris recognition.

## 5 Conclusions

Biometrics based personal identification methods have recently gained more interests with an increasing emphasis on security. In this paper, we have described an efficientmethod for personal identification from an iris image sequence. A quality descriptor based on the Fourier spectra of two local regions in an iris image is defined to discriminate clear iris images from low quality images due to motion blur, defocus, and eyelash occlusion. According to the distinct distribution of the iris characteristics, a bank of spatial filters is constructed for efficient feature extraction. It has been proven that the defined spatial filter is suitable for iris recognition. The experimental results have demonstrated the effectiveness of the proposed method. A detailed performance comparison of existing methods for iris recognition has been conducted on the CASIA Iris Database. Such comparison and analysis will be helpful to further improve the performance of the iris recognition methods.

## Acknowledgments

The authors would like to thank Dr. John Daugman (Cambridge University, UK), Dr. Richard Wildes (York University, Canada), and Dr. Jianguo Zhang for their helpful discussions. They also thank the anonymous referees for their constructive comments. A public version of the CASIA Iris Database is available from http:// www.sinobiometrics.com. This work has been filed for patents and is funded by research grants from the NSFC (Grant No. 69825105), the National 863 Program of China (Grant No. 2001AA114180), and the CAS.

## References

[1] Biometrics: Personal Identification in a Networked Society, A. Jain, R. Bolle and S. Pankanti, eds. Kluwer, 1999.
[2] D. Zhang, Automated Biometrics: Technologies and Systems. Kluwer, 2000.
[3] T. Mansfield, G. Kelly, D. Chandler, and J. Kane, "Biometric Product Testing Final Report," issue 1.0, Nat'l Physical Laboratory of UK, 2001.
[4] A. Mansfield and J. Wayman, "Best Practice Standards for Testing and Reporting on Biometric Device Performance," Nat'l Physical Laboratory of UK, 2002.
[5] F. Adler, Physiology of the Eye: Clinical Application, fourth ed. London: The C.V. Mosby Company, 1965.
[6] H. Davision, The Eye. London: Academic, 1962.
[7] R. Johnson, "Can Iris Patterns Be Used to Identify People?" Chemical and Laser Sciences Division LA-12331-PR, Los Alamos Nat'l Laboratory, Calif., 1991.
[8] A. Bertillon, "La Couleur de l'Iris," Rev. of Science, vol. 36, no. 3, pp. 65-73, 1885.
[9] T. Camus, M. Salganicoff, A. Thomas, and K. Hanna, Method and Apparatus for Removal of Bright or Dark Spots by the Fusion of Multiple Images, United States Patent, no. 6088470, 1998.
[10] J. McHugh, J. Lee, and C. Kuhla, Handheld Iris Imaging Apparatus and Method, United States Patent, no. 6289113, 1998.
[11] J. Rozmus and M. Salganicoff, Method and Apparatus for Illuminating and Imaging Eyes through Eyeglasses, United States Patent, no. 6069967, 1997.
[12] R. Wildes, J. Asmuth, S. Hsu, R. Kolczynski, J. Matey, and S. Mcbride, Automated, Noninvasive Iris Recognition System and Method, United States Patent, no. 5572596, 1996.
[13] T. Tan, Y. Wang, and L. Ma, A New Sensor for Live Iris Imaging, PR China Patent, no. ZL 01278644.6, 2001.
[14] http://www.iris-recognition.org/, 2002.
[15] L. Flom and A. Safir, Iris Recognition System, United Sates Patent, no. 4641394, 1987.
[16] J. Daugman, Biometric Personal Identification System Based on Iris Analysis, United States Patent, no. 5291560, 1994.
[17] J. Daugman, "High Confidence Visual Recognition of Persons by a Test of Statistical Independence," IEEE Trans. Pattern Analysis and Machine Intelligence, vol. 15, no. 11, pp. 1148-1161, Nov. 1993.
[18] J. Daugman, "Statistical Richness of Visual Phase Information: Update on Recognizing Persons by Iris Patterns," Int'l J. Computer Vision, vol. 45, no. 1, pp. 25-38, 2001.
[19] J. Daugman, "Demodulation by Complex-Valued Wavelets for Stochastic Pattern Recognition," Int'l J. Wavelets, Multiresolution and Information Processing, vol. 1, no. 1, pp. 1-17, 2003.
[20] R. Wildes, J. Asmuth, G. Green, S. Hsu, R. Kolczynski, J. Matey, and S. McBride, "A Machine-Vision System for Iris Recognition," Machine Vision and Applications, vol. 9, pp. 1-8, 1996.
[21] R. Wildes, "Iris Recognition: An Emerging Biometric Technology," Proc. IEEE, vol. 85, pp. 1348-1363, 1997.
[22] W. Boles and B. Boashash, "A Human Identification Technique Using Images of the Iris and Wavelet Transform," IEEE Trans. Signal Processing, vol. 46, no. 4, pp. 1185-1188, 1998.

[23] S. Lim, K. Lee, O. Byeon, and T. Kim, "Efficient Iris Recognition through Improvement of Feature Vector and Classifier," ETRI J., vol. 23, no. 2, pp. 61-70, 2001.
[24] R. Sanchez-Reillo and C. Sanchez-Avila, "Iris Recognition With Low Template Size," Proc. Int'l Conf. Audio and Video-Based Biometric Person Authentication, pp. 324-329, 2001.
[25] C. Sanchez-Avila and R. Sanchez-Reillo, "Iris-Based Biometric Recognition Using Dyadic Wavelet Transform," IEEE Aerospace and Electronic Systems Magazine, pp. 3-6, Oct. 2002.
[26] C. Tisse, L. Martin, L. Torres, and M. Robert, "Person Identification Technique Using Human Iris Recognition," Proc. Vision Interface, pp. 294-299, 2002.
[27] T. Tangsukson and J. Havlicek, "AM-FM Image Segmentation," Proc. IEEE Int'l Conf. Image Processing, pp. 104-107, 2000.
[28] Y. Zhu, T. Tan, and Y. Wang, "Biometric Personal Identification Based on Iris Patterns," Proc. Int'l Conf. Pattern Recognition, vol. II, pp. 805-808, 2000.
[29] L. Ma, Y. Wang, and T. Tan, "Iris Recognition Based on Multichannel Gabor Filtering," Proc. Fifth Asian Conf. Computer Vision, vol. I, pp. 279-283, 2002.
[30] L. Ma, Y. Wang, and T. Tan, "Iris Recognition Using Circular Symmetric Filters," Proc. 16th Int'l Conf. Pattern Recognition, vol. II, pp. 414-417, 2002.
[31] G. Zhang and M. Salganicoff, Method of Measuring the Focus of Close-Up Images of Eyes, United States Patent, no. 5953440, 1999.
[32] K. Castleman, Digital Image Processing. Prentice-Hall, 1997.
[33] J. Daugman, "Uncertainty Relation for Resolution in Space, Spatial Frequency, and Orientation Optimized by Two-Dimensional Visual Cortical Filters," J. Opticl Soc. of Am. A, vol. 2, pp. 11601169, 1985.
[34] T. Lee, "Image Representation Using 2D Gabor Wavelets," IEEE Trans. Pattern Analysis and Machine Intelligence, vol. 18, no. 10, pp. 959-971, Oct. 1996.
[35] D. Clausi and M. Jernigan, "Designing Gabor Filters for Optimal Texture Separability," Pattern Recognition, vol. 33, pp. 1835-1849, 2000.
[36] A. Jain, S. Prabhakar, L. Hong, and S. Pankanti, "Filterbank-Based Fingerprint Matching," IEEE Trans. Image Processing, vol. 9, no. 5, pp. 846-859, 2000.
[37] J. Zhang and T. Tan, "Brief Review of Invariant Texture Analysis Methods," Pattern Recognition, vol. 35, no. 3, pp. 735-747, 2002.
[38] P. Belhumeur, J. Hespanha, and D. Kriegman, "Eigenfaces vs. Fisherfaces: Recognition Using Class Specific Linear Projection," IEEE Trans. Pattern Analysis and Machine Intelligence, vol. 19, no. 7, pp. 711-720, July 1997.
[39] C. Liu and H. Wechsler, "Gabor Feature Based Classification Using the Enhanced Fisher Linear Discriminant Model for Face Recognition," IEEE Trans. Image Processing, vol. 11, no. 4, pp. 467-476, 2002.
[40] J. Beveridge, K. She, B. Draper, and G. Givens, "A Nonparametric Statistical Comparison of Principal Component and Linear Discriminant Subspaces for Face Recognition," Proc. IEEE Conf. Computer Vision and Pattern Recognition, pp. 535-542, 2001.
[41] R. Bolle, S. Pankanti, and N. Ratha, "Evaluation Techniques for Biometric-Based Authentication Systems (FRR)," IBM Computer Science Research Report RC 21759, 2000.
[42] J. Wayman, "Confidence Interval and Test Size Estimation for Biometric Data," Nat'l Biometric Test Center (collectedworks), pp. 91-101, 2000.
[43] B. Efron and R. Tibshirani, "Bootstrap Methods for Standard Errors, Confidence Intervals, and Other Measures of Statistical Accuracy," Statistical Science, vol. 1, pp. 54-75, 1986.

![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-15.jpg?height=309&width=254&top_left_y=219&top_left_x=1001)

Li Ma received the BSc and MSc degrees in automation engineering from Southeast University, China, in 1997 and 2000, respectively, and the PhD degree in computer science from the National Laboratory of Pattern Recognition, Chinese Academy of Sciences, in 2003. Currently, he is a research member of IBM China Research Lab. His current research interests include image processing, pattern recognition, biometrics, and multimedia.
![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-15.jpg?height=312&width=254&top_left_y=614&top_left_x=1001)

Tieniu Tan (M'92-SM'97) received the BSc degree in electronic engineering from Xi'an Jiaotong University, China, in 1984, and the MSc, DIC, and PhD degrees in electronic engineering from the Imperial College of Science, Technology and Medicine, London, UK, in 1986, 1986, and 1989, respectively. He joined the Computational Vision Group in the Department of Computer Science at The University of Reading, England, in October 1989, where he worked as a research fellow, senior research fellow, and lecturer. In January 1998, he returned to China to join the National Laboratory of Pattern Recognition, the Institute of Automation of the Chinese Academy of Sciences, Beijing, China. He is currently a professor and the director of the National Laboratory of Pattern Recognition as well as president of the Institute of Automation. He has published widely on image processing, computer vision, and pattern recognition. His current research interests include speech and image processing, machine and computer vision, pattern recognition, multimedia, and robotics. He serves as referee for many major national and international journals and conferences. He is an associate editor of Pattern Recognition and IEEE Transactions on Pattern Analysis and Machine Intelligence, the Asia editor of Image and Vision Computing. Dr. Tan was an elected member of the executive committee of the British Machine Vision Association and Society for Pattern Recognition (1996-1997) and is a founding cochair of the IEEE International Workshop on Visual Surveillance. He is a senior member of the IEEE and a member of the IEEE Computer Soceity.
![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-15.jpg?height=314&width=254&top_left_y=1521&top_left_x=1001)

Yunhong Wang received the BSc degree in electronic engineering from Northwestern Polytechnical University, the MS degree (1995) and the PhD degree (1998) in electronic engineering from Nanjing University of Science and Technology. She joined the National Lab of Pattern Recognition, Institute of Automation, Chinese Academy of Sciences in 1998, where she has been an associate professor since 2000. Her research interests include biometrics, pattern recognition, and image processing. She is a member of the IEEE and the IEEE Computer Society.
![](https://cdn.mathpix.com/cropped/5fc597c2-85c0-40fb-8872-2ea135faf304-15.jpg?height=312&width=254&top_left_y=1929&top_left_x=1001)

Dexin Zhang received the BSc degree in automation engineering from Tsinghua University in 2000. Then, he joined the National Laboratory of Pattern Recognition, Chinese Academy of Sciences, to pursue his master's degree. His research interests include biometrics, image processing, and pattern recognition.

▷ For more information on this or any other computing topic, please visit our Digital Library at http://computer.org/publications/dlib.

