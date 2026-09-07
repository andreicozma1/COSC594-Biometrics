# FaceNet Discussion Posts

## Andrei Cozma — Main Post Draft

FaceNet reframes face verification, recognition, and clustering as a shared geometric problem: learning where face images belong in an embedding space so that distances reflect identity similarity. Compared with last week’s iris method, which combined hand-designed texture features with learned dimensionality reduction, FaceNet shifts representation design toward a purely data-driven approach. A deep convolutional network learns features and invariances to pose, illumination, and other variations from a large dataset of labeled faces. &#x20;

I wondered how alignment or illumination normalization could complement the learned representation. Augmentation offers another direction. Illumination can alter the appearance of visible facial structure. Low resolution or occlusion can remove access to distinguishing details. I’d like to see how training with noise, blur, or compression affects recognition on real degraded images and unseen identities, including tradeoffs on clear images. &#x20;

I was also interested in how quality scores could help at different stages of the pipeline, something the paper doesn’t explore in much detail. These measures could help a system decide when to request a better image, which frames to use, and how much weight to give each observation when combining matches. During training, quality measures could also guide sample selection and weighting, while separate label checks could flag misannotations. The challenge would be managing unreliable samples without excluding difficult conditions the network needs to learn. &#x20;

Finally, while the paper focuses on recognizing identity, it leaves the authenticity of the submitted sample outside its evaluation. For authentication, I’d be interested in how FaceNet performs when combined with liveness and attack detection, particularly against presentation attacks and deepfakes. That would help assess both security and the effect of those checks on legitimate users.

## Final Replies

1.

### Andrei Cozma8:44 PM

The authors partially address the effects of training data size in Section 5.5, Table 6, albeit they disclose that this evaluation was run on a smaller model, and that the effect may be even larger on larger models. Still, this gives us a glimpse into the scaling properties: with the smaller model, gains taper off quickly: validation improved from 76.3% at 2.6M images to 85.1% at 26M, then 86.2% at 260M.  To build on this question, I think it would also be super interesting to test which kinds of additional data provide the greatest improvement per added training sample: more identities, more images of each identity, or greater variation in pose, lighting, and capture conditions within each identity. This could help guide how to expand the dataset, rather than simply making it larger.   I’m curious, what kind of additional data do you all think would make the biggest difference, and in what ways? And what would be a good way to determine what the right mix is?&#x20;

1.

### Andrei Cozma9:00 PM

Your point about a shared model also made me think about federated learning. Smaller organizations could potentially contribute to training using their own face data while keeping the images local. That could bring in different identities and capture conditions without requiring one company to collect everything.   I’m curious how well a shared embedding would learn across organizations whose data look very different, and how well the benefits could be shared across participating organizations. It connects to a broader research question in the field: how can organizations learn from one another when they have different data, resources, and local needs? For face recognition, those differences could include the identities represented, cameras, and capture conditions, etc.. This non-IID setting is a central challenge and core theme in federated learning.  One direction that has seen much attention recently in FL is personalization: learning together while allowing the model to adapt to each organization’s needs (e.g., local PEFT, local personalized adapter heads, etc.)
