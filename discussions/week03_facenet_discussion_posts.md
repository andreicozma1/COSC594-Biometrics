# FaceNet Discussion Posts

## Andrei Cozma — Final Post

FaceNet reframes face verification, recognition, and clustering as a shared geometric problem: learning where face images belong in an embedding space so that distances reflect identity similarity. Compared with last week’s iris method, which combined hand-designed texture features with learned dimensionality reduction, FaceNet shifts representation design toward a purely data-driven approach. A deep convolutional network learns features and invariances to pose, illumination, and other variations from a large dataset of labeled faces. &#x20;

I wondered how additional explicit alignment and normalization could complement the learned representation. Augmentation offers another direction. Illumination can alter the appearance of visible facial structure. Low resolution or occlusion can remove access to distinguishing details. I’d like to see how training with noise, blur, or compression affects recognition on real degraded images and unseen identities, including tradeoffs on clear images.&#x20;

I was also interested in how quality scores could help at different stages of the pipeline, something the paper doesn’t explore in much detail. These measures could help a system decide when to request a better image, which frames to use, and how much weight to give each observation when combining matches. During training, quality measures could also guide sample selection and weighting, while separate label checks could flag misannotations. The challenge would be managing unreliable samples without excluding difficult conditions the network needs to learn. &#x20;

Finally, while the paper focuses on recognizing identity, it leaves the authenticity of the submitted sample outside its evaluation. For authentication, I’d be interested in how FaceNet performs when combined with liveness and attack detection, particularly against presentation attacks and deepfakes. That would help assess both security and the effect of those checks on legitimate users.

## Final Replies

### Andrei Cozma — 8:44 PM

The authors partially address the effects of training data size in Section 5.5, Table 6, albeit they disclose that this evaluation was run on a smaller model, and that the effect may be even larger on larger models. Still, this gives us a glimpse into the scaling properties: with the smaller model, gains taper off quickly: validation improved from 76.3% at 2.6M images to 85.1% at 26M, then 86.2% at 260M.  To build on this question, I think it would also be super interesting to test which kinds of additional data provide the greatest improvement per added training sample: more identities, more images of each identity, or greater variation in pose, lighting, and capture conditions within each identity. This could help guide how to expand the dataset, rather than simply making it larger.   I’m curious, what kind of additional data do you all think would make the biggest difference, and in what ways? And what would be a good way to determine what the right mix is?&#x20;

### Andrei Cozma — 9:00 PM

Your point about a shared model also made me think about federated learning. Smaller organizations could potentially contribute to training using their own face data while keeping the images local. That could bring in different identities and capture conditions without requiring one company to collect everything.   I’m curious how well a shared embedding would learn across organizations whose data look very different, and how well the benefits could be shared across participating organizations. It connects to a broader research question in the field: how can organizations learn from one another when they have different data, resources, and local needs? For face recognition, those differences could include the identities represented, cameras, and capture conditions, etc.. This non-IID setting is a central challenge and core theme in federated learning.  One direction that has seen much attention recently in FL is personalization: learning together while allowing the model to adapt to each organization’s needs (e.g., local PEFT, local personalized adapter heads, etc.)

## Full Discussion Thread

### Rishi [mеtһ],  — 9/4/26, 10:50 AM

I thought this paper was interesting because FaceNet does not directly classify a face as a certain person. Rather, it encodes each face as a 128-dimensional vector, where vectors corresponding to faces of the same person are close, and faces belonging to other persons are farther. One such element was the concept of Triplet Loss where they train the model using three images: an anchor image, a positive image, which is of the same person as the anchor, and a negative image, which is of a completely different person than the anchor image. In addition, they make use of Semi-Hard Negative Mining in order to get the harder examples.

The results were very strong, with 99.63% accuracy on LFW and 95.12% on YouTube Faces. Another positive feature is that the effect of image quality, embedding size, model size and training data has been evaluated rather than providing just the final results. One of the drawbacks is that the system has been trained on about 100 to 200 million face images of 8 million identities, which means that it will be difficult to replicate the system because of the need for a huge amount of data and computing resources. In my opinion, the contribution of the paper is great as a single face embedding is enough for verification, recognition and clustering.

The question I had after reading this was: Do you think FaceNet would perform as well if it were trained on a much smaller dataset?

### Jisu Kim — 9/5/26, 2:16 AM

After reading the iris paper, this one felt very different. The previous paper spent a lot of pages on localiation, normalization, illumination correction, and filter design. FaceNet just takes roughly aligned face patches and learns the rest.

But the design work is still there, I think. It is just in a different place now. It is in the network and in how they pick the triplets. Choosing which triplets are hard enough is still something a person decides, and they had to make a new mining method to make the training work.

Also I want to add one thing from last week. I said the LDA projection was tied to 306 training classes. FaceNet does not have this problem. The embedding is not built around a fixed group of people, so you can enroll a new user by just saving their embedding. I think this is also why the same model can do clustering.

> [mеtһ],

### Jisu Kim — 9/5/26, 2:22 AM

I think the iris paper we read gives a partial answer. It was with a small database, but they could do that because they designed the filters by hand using what they knew about iris structure. FaceNet does not have that kind of built-in knowledge, so the data has to provide it.

So maybe with a small dataset you would need to put something back in, like face alignment or stronger augmentation. It would be interesting to know how small the dataset can get before that becomes necessary.

### Rishi [mеtһ],  — 9/5/26, 12:13 PM

I agree that FaceNet moves a lot of the design work from manual preprocessing into the model and training process. Your point about the embedding is also interesting because it makes the system more flexible when adding new users.

Do you think this makes FaceNet easier to use in real world systems than older methods like LDA?

### Rishi [mеtһ],  — 9/5/26, 12:26 PM

I agree. FaceNet seems to depend much more on having a large and diverse dataset, while the iris method used more hand-designed knowledge in the system. It would be interesting to see how much alignment or augmentation could help FaceNet when the training data is limited.

> [mеtһ],

### Jisu Kim — 9/5/26, 4:59 PM

That is a good question. I think it depends on the scale. If you are a big company with a large pretrained embedding, adding a new user is very easy, just save one vector. But if you are building the system from scratch, FaceNet needs a lot of data and compute to get a good embedding in the first place. LDA needs much less to get started, even if it does not scale as well later.

So maybe FaceNet is easier once it exists, but harder to build from zero.

### Laura Smith — 9/5/26, 6:05 PM

I think this paper did a really good job of explaining what made FaceNet different from older face recognition methods. Instead of having separate systems for recognition, verification, and clustering, the authors created one compact embedding where faces of the same person are close together and different people are farther apart. The results were also really good, with 99.63% accuracy on LFW and 95.12% on YouTube Faces.  I had actually seen this paper before, so it was cool to read it again now that I know more about some of the topics it talks about. I felt like I understood more of the reasoning behind the method this time around.

One thing I think the paper could have done better was compare some of its choices more directly. For example, the authors mention that they did not directly compare triplet loss to other possible losses, and they also did not fully compare different ways of choosing positive examples during training.   More side-by-side tests would have made it clearer which parts of FaceNet were making the biggest difference. One future improvement that the paper did not really discuss would be looking more closely at fairness and bias across different groups of people. Testing performance across things like age, skin tone, and other demographics could help make a system like this more reliable and fair in real-world use.

> [mеtһ],

### Laura Smith — 9/5/26, 6:10 PM

I think with any model you're training performance would decrease with less data, but I think especially so here. Because of how the model works and the way it was made, I would guess it would be more reliant on that training data than other models we've looked at. It would be interesting to test it though and see if my assumption is correct or if it can work with less data.

### Laura Smith — 9/5/26, 6:18 PM

I agree with this, but also facenet could have a centralized model that has been trained and continuously improved by a big company, then smaller companies just access that model to use it. It would definitely be too much for a small company to make and train in house.

### Dhrumil — 9/5/26, 6:52 PM

This paper describes a system where each face is converted into a low-dimensional embedding of 128 dimensions. Faces from the same person will be nearby, and faces of different people will be further away.

The key technique is called triplet loss. It uses an image as an anchor, another similar image of the same person as the positive one, and a third different image as the negative one. The aim is to bring the matching images closer and separate the non-matching ones.

Pipeline:

Face Image -> Deep CNN -> Embedding -> Distance Comparison

FaceNet gave an accuracy of 99.63% on LFW and 95.12% on YouTube Faces.

A drawback is that FaceNet needed huge amounts of training data. As it was written in 2015, it also does not completely cover modern problems such as deepfakes, privacy concerns, and demographic biases.

Question: How effective is FaceNet at dealing with modern AI-generated or deepfake faces?

### Dhrumil — 9/5/26, 6:54 PM

However, I fully support your view on the necessity to provide more comparative data. In your opinion, the research demonstrates the great performance of FaceNet, and better comparisons would help to understand which design aspects influenced the results. Your view on the topic of fairness is also very relevant. It should be taken into consideration that a face recognition system may be highly accurate, yet show different results depending on certain demographic features.

### Andrei Cozma — 9/5/26, 8:19 PM

FaceNet reframes face verification, recognition, and clustering as a shared geometric problem: learning where face images belong in an embedding space so that distances reflect identity similarity. Compared with last week’s iris method, which combined hand-designed texture features with learned dimensionality reduction, FaceNet shifts representation design toward a purely data-driven approach. A deep convolutional network learns features and invariances to pose, illumination, and other variations from a large dataset of labeled faces.

I wondered how additional explicit alignment and normalization could complement the learned representation. Augmentation offers another direction. Illumination can alter the appearance of visible facial structure. Low resolution or occlusion can remove access to distinguishing details. I’d like to see how training with noise, blur, or compression affects recognition on real degraded images and unseen identities, including tradeoffs on clear images.

I was also interested in how quality scores could help at different stages of the pipeline, something the paper doesn’t explore in much detail. These measures could help a system decide when to request a better image, which frames to use, and how much weight to give each observation when combining matches. During training, quality measures could also guide sample selection and weighting, while separate label checks could flag misannotations. The challenge would be managing unreliable samples without excluding difficult conditions the network needs to learn.

Finally, while the paper focuses on recognizing identity, it leaves the authenticity of the submitted sample outside its evaluation. For authentication, I’d be interested in how FaceNet performs when combined with liveness and attack detection, particularly against presentation attacks and deepfakes. That would help assess both security and the effect of those checks on legitimate users.

> [mеtһ],

### Andrei Cozma — 9/5/26, 8:44 PM

The authors partially address the effects of training data size in Section 5.5, Table 6, albeit they disclose that this evaluation was run on a smaller model, and that the effect may be even larger on larger models. Still, this gives us a glimpse into the scaling properties: with the smaller model, gains taper off quickly: validation improved from 76.3% at 2.6M images to 85.1% at 26M, then 86.2% at 260M.

To build on this question, I think it would also be super interesting to test which kinds of additional data provide the greatest improvement per added training sample: more identities, more images of each identity, or greater variation in pose, lighting, and capture conditions within each identity. This could help guide how to expand the dataset, rather than simply making it larger.

I’m curious, what kind of additional data do you all think would make the biggest difference, and in what ways? And what would be a good way to determine what the right mix is?

### Andrei Cozma — 9/5/26, 9:00 PM

Your point about a shared model also made me think about federated learning. Smaller organizations could potentially contribute to training using their own face data while keeping the images local. That could bring in different identities and capture conditions without requiring one company to collect everything.

I’m curious how well a shared embedding would learn across organizations whose data look very different, and how well the benefits could be shared across participating organizations. It connects to a broader research question in the field: how can organizations learn from one another when they have different data, resources, and local needs? For face recognition, those differences could include the identities represented, cameras, and capture conditions, etc.. This non-IID setting is a central challenge and core theme in federated learning.

One direction that has seen much attention recently in FL is personalization: learning together while allowing the model to adapt to each organization’s needs (e.g., local PEFT on top of the global shared model, local personalized adapter heads, etc.)
