# case-study-WenjieLuo2333
case-study-WenjieLuo2333 created by GitHub Classroom

## Chosen Project: Keras<br>
### Brief Intro<br>
  Keras is a high-level neural networks API, capable of running on top of Tensorflow, Theano, and CNTK.<sup>[[1]](https://towardsdatascience.com/introduction-to-deep-learning-with-keras-17c09e4f0eb2)</sup><br>
  In this case study, I will focus more on a tensorflow backend Keras.<br>
  #### Chosen Languase<br>
  In my opinion, Keras is a high-level lib on Tf, Theano, CNTK written in python.<br>
  However, the backends are not pure-python frameworks.<br>
  Tensorflow and Theano's core is written in a combination of highly-optimized C++ and CUDA(Gor GPU calculation) and then packaged with user-friendly API written in Python.<br>
  CNTK is a pure C++ framework developed by CNTK.<br>
  However, the tensorflow backend Keras should be the most commonly used one.<br><br>
  #### Why choose such languages.
  The core of the Keras backends are all in C++ because of the faster working efficiency.<br>
  C++ is a Compiled language that will be compiled into bytecode before running. However, Python is an Interpreted Language which means the python will be run row by row. And each time when you run a python scripts, the interpreter works once. Thus it will have slower execution speed compared with languages like C++.<br>
  However, Python is probably the most comfortable language for users and it also that easy to integrate and have control to a C++ backend.<sup>[[2]](https://stackoverflow.com/questions/35677724/tensorflow-why-was-python-the-chosen-language)</sup><br/>Due to the user-friendly characteristic, almost all the deep learning frameworks offer python API.<br>
  I will use Python even if the project is developed today because of the ease of programming.<br><br>
  #### Build System for Keras
  Cmake and Bazel is used to build. However, according to the [Tensorflow Install Guide](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/contrib/cmake) that CMAKE build is deprecated for TensorFlow and Bazel is recommanded.GCC and [NVCC](https://en.wikipedia.org/wiki/NVIDIA_CUDA_Compiler) are needed to build a tensorflow based Keras with GPU acceleration.<br><br>
  #### Frameworks and libraries used in Keras
  ```CNTK```/```Tensorflow```/```Theano```<br>
  ```numpy```<br>
  ![image](https://github.com/ec500-software-engineering/case-study-WenjieLuo2333/blob/master/Install_Requirements_Keras.png)<br>
  Quote from [Keras Team](https://github.com/keras-team/keras/tree/master/keras/backend)
  
### Testing<br>
Keras is using Travis-CI platform for test. To make sure the test meaningful, Keras has a visual system for its [code coverage matrics](https://coveralls.io/github/phreeza/keras).All the codes that are not covered by test are clearly displayed. And for now they have a code coverage at about 81%.<br>
Due to different backends they use, although I didn't find the specific documentation, I believe Windows and Linux should be tested because all of the backends are tested according to [```.travis.yml```](https://github.com/keras-team/keras/blob/master/.travis.yml).
<br><br>

### Software Architecture<br>
Software architecture including:<br> a. how would you add / edit functionality if you wanted to? How would one use this project from external projects, or is it only usable as a standalone program?<br>b.What parts of the software are asynchronous (if any)?
<br>c.Please make diagrams as appropriate for your explanation<br>d.How are separation of concerns and information hiding handled?<br>e.What architectural patterns are used<br>f.Does the project lean more towards object oriented or functional components<br>

It offers users with flexible API to define their own functions like layers or loss functions. For example, I can always define my own loss function used in my AI model by K.function API.<br>
Keras offers integrated common used neural network layer, optimizers,loss functions and so on. Users are free to design their own models and solve their own tasks.<br>
The data in Keras are handled in tensors and flow from up to down. Thus there's no asynchronous part.<br>
The diagram of a classic architecture of Keras.<br>![image](https://github.com/ec500-software-engineering/case-study-WenjieLuo2333/blob/master/Frameworks.png)<br>
Data is handled in ways of tensor. And the final model consists of no data, thus there's no need for data security.
I think the projects build on Keras should in an MVC architecture(model, view, controller).
As is shown in diagrams, Keras can be divided in such modules based on their function. However, all the components in each module are written in an object-oriented way. Combined with the user experience, I think it's lean more towards object-oriented components.<br><br>

### Issue Analysis<br>
The aim of the issue can be various. Most of them are using issues but not a requirement for architecture change. However, there're issues for system developing and helped developers to better organize their codes.<br>
For example, the [#649 Issue](https://github.com/keras-team/keras/issues/649) reminded the keras group that there's no code coverage metrics which has a side-effect on using. And finally, the group fixed the problem and works better on this project.<br>

### Demonstration Applicaitons<br>
I build a Generative Adversarial Network on Keras to generate Anime Images.See in [Anime Generator](https://github.com/WenjieLuo2333/Anime_Generator)<br> 
The general process is to:<br>
1. Process data with functions like Keras.prepocessing.load_img to preprocess data.<br>
2. Build a network structure with Keras.layers.<br>
3. Initialize the training scripts with modules like Keras.optimizer,Keras.losses and so on.<br>
4. Start Training and get the finnal module.<br><br>
The model I trained can generate relatively good images from random noise imput.<br>
![image](https://github.com/WenjieLuo2333/Anime_Generator/blob/master/Res_DRAGAN/Predict_2.png)<br>
And for Interpolation it seems that the entries of noise is realated to the feature of pictures.<br>
![image](https://github.com/WenjieLuo2333/Anime_Generator/blob/master/Res_DRAGAN/inter_2.png)<br>
