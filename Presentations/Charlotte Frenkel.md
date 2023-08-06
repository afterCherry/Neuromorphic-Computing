# merge insights from artificial and biological neural networks for neuromorphic edge intelligence 
Every single topic that we’re interested in. 
We’ve got artificial neural network, which is relevant to biological neural networks and we’ve got neuromophic all in one talk, 
so this is going pretty cool and perfect for this community. 
Go ahead.

Synergies - Neroscience - Engineering

## Q&A
1. how should we exploit and make the best of the synergies
between neuroscience and AI, more specifically, what is the right perspective
and the right starting point to make the best of these series? <br>

There are bi-directional interaction between neuroscience and AI. One is bottum-up direction,
the goal is to identify what are the brain computational primitives and how to scale them to AI oriented workloads, 
for example the bio-inspired backpropagation. The other is up-buttom direction, which will utilize algorithm.
Hardware forms a very interesting middle ground to shift some light as to how should we make the best use of neuroscience and AI. <br>

Moore’s law implicates that the hardware updates two times every two years.
For popular AI workloads, the training computor requirements scale 15 times every two years.
But now even with the Transformer models, it’s going even 700 times every two years, which is completely unsuatainable. 
So the only way to scale should be sustainable. It’s about scaling the size of GPU server forms. <br>

2. why should we bother at all with Neuroscience?

Hardware efficiency and bio-plausibility are often two sides of a same coin. 

- Start from neuroscience - based on the timing of spikes:
The question is which salt and pepper from neuroscience you take to lead to more efficient learning algorithms that can outperform conventional approaches.
What we can do for all neuromorphic intelligence is that it should be fed by insight from science and more bottom-up approach.

Synaptic plasticity take neuroscience as starting point, which is relevant to the STDP(spike-time-dependent plasticity). 脉冲时间相关突触可塑性
Every time pre-synaptic spike happens before a post-synaptic spike, there has been a relationship relevant to a casual potential synapse,
so we need to enhance the weight.
But if post-synaptic spike happens before a pre-synaptic spike, we need to depress your weight. 
This is the cinematitis between two neurons and this is a local learning rule, 
which is to tell us that for every presynaptic spike you look into the state of the postsynaptic neuron.
For stdp you have to compute every single synapse inside a time window in order to 
remember what is the spike time difference between the pre and post synaptic neuron. 
There are perhaps one hundred to one thousand synapses per neuron, so this is very expensive to do.
The problem is that when stdp is the right starting point it is very difficult to scale efficienly.

However for SDSP(spike dependent synaptic plasticity), you do not have to do such computation.
you just need to get the state of the postsynaptic neuron every time you get a presynapsic spike, 
that leads to huge silicon savings and also a huge hint to more bioplausible mechanism.
Both learning rules are local, to be specific, they are both local in space but only sdsp is local in time that you do not need to compute the time difference.
if you look this paper, you will get that voltage-based learning rules are more bio-plausible than that are purely based on the timing of spikes.

If you look into neuroscience, you can see that the RTP can slign with output independent target signals in the dentric path digital instructive pathways of cortical intermediary units 
that means the RTP can align with some of the mechanism that are used in the brain. 
Because now we made back-propapagtion more bioplausible and hardware-efficient, 
you really _release computational and memery costs_, for example we demonstrate with a chip that embeds the RTP algorithm, 
There’s only a fifteen overhead empire in an area compared to the inference on the network,
so we really demonstrate that this is a cheap learning algorithm that can implement on chip.

- Start from AI - based on the bio-plausible mechanism:
For the more AI driven approach, we have seen that bringing AI closer to neuroscience leads to more hardware efficiency. 
You really start from the working solution to real world problem because you start from back-propagation.
Weight transport you need to transpose the weight matrix during the backward path which is not bioplausible because that implies synapses would be bi-directional and this is not happen in neuron.

BP algorithm means before updating this weight matrix you need to do the full forward path and then the full backward path, 
so this is known as update locking because you should do nothing about this weight matrix before you do full forward and the backward path. 
This is not bioplausible because that implies two phases in deep learning which the brain doesn’t do. All the synapses learn in parallel and in real time in the brain.
FA(Feedback Alignment) just replace the transpose of the weight matrix and backward path by a fixed random productivity matrix, which figures out how to propagate useful error information. 
DFA(Direct Feedback Aligment) fixed random predictions of the final error in order to as a surrogate for the relay wise gradients. 
Two algorithms release the weight transport but they do not release of developing, you still have to do full of forward path before full backword path.

We got an idea that we use the _sign of the error_ here instead of the error iteself. 
You have a very nice property for classification probelms because the target of classification is just one hot encoding of the classification label. 
The target minus the network output is softmax which is strictly bounded between zero and one, so the sign of the error is known in advance according to the sign.
So you can use this property to release update locking and lead to all direct random target rejection algorithm which just use fixed random connectivity projections of this target vector.

3. how we morph these questions into interesting engineering solutions?

onchip learning.

Inference device for example your smartwatch that you want to do some keyword watching, performance is going to be within the specifications. 
Data from requirements that need to evolve over time for example you would program your device to learn a new keyboard how to do. 
The problem is that decision can be within the performance boundaries at the beginning of the lifetime of the device, 
as time went by, you will get more data out of distribution over time, 
you need more data to cover more cases that has a cost to gather and creates such massive amounts of data that’s never robust and flexible in the long term.
The second thing you can do is the thing that was done actually that is a data exchange with the cloud 
that you have to consume energy from your battery to do, 
so if you have a very tiny device battery operated devices that can be expensive and 
you might need to leak a user specific data to the cloud and therefore will come with privacy issue.
Note. End-to-end memory means there’s no external momery 
because in hardware design accessing external memory is expensive power-wise, so we would like everything happen on chip. 

Temporal data for video or speech is still an open problem. 
Suppose you have temperal data lasting one second with the temperal resolution of one millisecond 
so that you have a thousand data samples, so you need to store a copy of the network dynamics for every sample 
until you get the final error and 
you can finally back-propagate the gradients through the whole network dynamics so this is known as enrolling time. 
Give you an order of magnitude current integrated circuits that can perform on-chip training are limited, 
which leads to intractable memory and latency requirements.

The brain doesn’t do back-propogate through time.
E-prop(Eligibility Propagation) approximates the background real-time gradients as a product of two terms. 
One is error-based learning signal that is the main assumption. 
The second term is called synaptic eligibility trace that represents important of every signle synapse onto the output. 
These eligibility traces are computed exclusively forward in time and not error based, which is supported by biological evidence.
What is the super nice property is that we only need to store the current timestamp, 
which can be done online.
We don't need to wait for the final error and buffer all the network state before we can apply the updates. 
Space and time locality are everything for both of neuroscience and hardware efficiency, 
which slashes the on-chip memory requirements. 
The challenge through is that the e-prop is not fully amendable for a hardware implementation.
Here comes to another question why spikes is the e-prop proposed as a bioplausible alternative, 
from an engineering point of view that are some nice properties that spike have that we want to select. 
The eligibility traces are dependent on the selected neuron model. 
Eligiblity traces is just a simple activity low pass filtering nothing more to do, 
but for the Adaptive leaky integrating fire and iron, it becomes completely intractable.
However about this leads to a complex personal apps multi-time scale filtering.
The first challenge we need to solve for e-prop in order to make that amendable to a non-chip implementation is what neuron model should we select. 
E-prop is not by default able to learn very long time skills you need to combine that with a powerful neural model, 
what neuroscience tells us here is that you need to have threshold adaption and it’s not hardware-efficient. 
We take a configurable integrating pioneering which comes with a simplification of e-prop for space and time locality, 
so this is schematic correspondence of the approach that we propose.

The theta is firing threshold as soon as you reach it you fire a spike and you reset, it’s just a leaky integrator. 
Why no spike at the outputs is just to avoid ill-defined spike-based error definitions. 

Nice task is the delay supervision navigation that sometimes also called queue accumulation which is a typical text of neuroscience, 
You have a rodent moving along corridor. 
It seems queues on the left and right, here represented by small squares, 
there are  four cubes on the left and three cubes on the right. 
It has to decide to turn left or right for the direction which it has seen the most cubes, so in this case the good solution is that the rodent should turn left. 
It really has to maintain a working memory of what happened in the past in order to make the right decision. 
If you take vanilla background through time with a standard leaky intergrating fire neron 
with a bioplausible leakage of twenty milliseconds and network is completely unable to learn to solve the task. 
Interestingly if you just use a slighly more complex neural modal such as the Adaptive leak integrine fire near LIF where you have threshold adaptation, 
the network is able to learn to pick up the dynamics and learn to solve the task, 
so why is it so? Because for the standard leak integrating fire neuron you only have a short time concept of about twenty milliseconds of leakage biology 
while for the Adaptive leaky integrating ALI pioneer which is arguably more bioplausible, 
it embeds threshold adaptation over hundreds of milliseconds 
and this is indeed sufficient to induce long temporal dependencies in the network dynamics and learn to solve the task with network through time.

we will take a non-bioplasible neural model, so we just take LIF(leak integrated fire) neural model. 
We’ll make the leakage time constant flexible from milliseconds to seconds, 
so going with a brain potential leakage up to seconds is not bio-plausible.
we can write e-prop equations for the leak integrating fire engineering, 
so we write the output weights, recurrent weights and input weights.
The learning signals here you see is the error definition.
For the recurrent input weight you need a projection from the output readout matrix. 
Indeed the learning signals are just an error based term, 
it requires what we call a dedicated gradient memory that sums all computed by e-prop over all steps before applying them. 
It's also not bioplausible because your brain does not store all the updates in a specific part and then carry out the updates at once at the second phase, 
so you again have the duality between neuroscience and hardware, 
so we perform the updates at every time and that will work fine as long as the learning rate is small. 

Now we look at to what is inside eligibility traces you have actually three things. 
The first one I mentioned is the pre-synaptic activity low pass filtering term and you find the filtering terms depending on the leakage of the neuron, 
hence if you get a long leakage you will get a long time scale eligibility trace. 
The second term is the postsynaptic stray through estimator also, called cometimes surrogate gradient for the activation function, 
so this is just a smoothed activation spiking activation function derivative. 
The third thing is that actually the problem with e-prop - 
you have a temporal coupling of these pre and postsynaptic terms and 
this is very expensive to compute because you need to remember the product of these terms of the time. 
This temporal coupling term can be safely neglected. 
Decoupling the pre and the postsynaptic terms is storage and computation-wise. 
Now everything scales with the number of neurons and not anymore with number of synapses and 
therefore you can really cut the memory overhead. 
We show 8 bits is a sweet spot if you combine with stochastic weight updates,
you have all modified e-prop algorithm and with a two second leakage time constant, 
this is actually issued from chip measurements. 
First thing that we can do with the backpack through time trainning with network is our baseline. 
The second thing is that we can do this with only about one person memory overhead compared to the inference network,
so you take your inference on the model in case you lost a little track of it.
The challenge that we have encountered is that it’s not tractable hardware-wise not bio-plausible. 



This is a cute cheap micro photograph that everything has been implemented in less than half a millimeter squared of silicon,
so this is a tiny chip. 
No external memory that everything happens inside the chip, 
so here is the kind of high level overview you have here the chip itself, 
and it communicate with spikes with any kind of sensor, 
so it can be a spiky new morphic retina it can be used by a spiking cochlear. 
The chip doesn’t need to know anything about the sensor as long as it talks with spike, 
the people figure out how to learn with these spikes. 
Why should we use spikes, because they are even driven in sparsity where computation. 
They also allow sense or agnostic raw data. 
In order to demonstrate this task I’m going to sleep processing and learning we need different kinds of benchmarks.

This involves over six seconds with about a five millisecond temporal resolution as we have selected here. 
keywords spotting, spiking heidelberg digits dataset so what we show here is that every digits is about half a millimeter half a second in length. here on the y-axis you have the different channel and with lower channels representing lower frequencies. you will see the index represent the higher order frequencies this is six and this is seven. THe third dataset you can select now is the delayed supervision that accumulation task is in this proxy for the navigation use case. For all the learning task you need less than fifty micro watts to perform, so to give an order of magnitude and one milliwatts is the kind of low power for your phone. If you go to the microwatt range this start becoming adequate to perform user adaptation in wearables for example where the battery size is really critical. The nice blending of AI algorithm neusoscience and hardware we’ve demonstated the reckon the chip could perform end-to-end on-chip learning over second long time skills while taking a milli-second temporal resolution.
Just because we require less than one personmemory overhead.
user customization and even full chip repurposing at the edge 
（搞的是AI芯片，当然要测试AI任务，这里的变量就是硬件了，而这个硬件是自己设计出来的哎，太爽了太爽了
（落地就很爽就很爽




# Words
- correspondence 一致性
- schematic 示意图
- recurrent 经常性的
- overhead 头上的
- cortical 皮质的
- dentric 树状的
- slign 对齐
- relay 中继，转述
- depress 压抑
- implicate 暗示
- morph 变形
- exploit 开发
- colleagues 同事
- reckon  估计
- blending 混合的
- heidelberg （德国）海德堡
- clap hands 鼓掌
- gesture 手势
- agnostic 不可知的
- cochlear 耳蜗
- retina 视网膜
- morphic 形态学的
- tractable 容易驾驭的
- neuromorphic 神经形态的
- overhead 高
- derivative 衍生物
- surrogate 代理人
- stray 流浪
- duality 二元的
- arguably 可以说
- vanilla 香草
- corriodor 走廊
- rodent 啮齿动物
- extensively 广泛地
- for the sake of  为了
- amendable 可修改的
- slash 消减
- exclusively 只
- eligibility  合格
- intractable 棘手的 troublesome
- magnitude 幅度
- quarantine 隔离
- empire 帝国
- cortical 皮质的
- surrogate 代理人
- bioplausible 生物合理的
- dendritic 树突
- standpint 立场
- synergy 协同作用
- postulate 假设
- potentiate synapse 增强突触
- anticosal 反壁
- cinematitis 电影般的

# RP
Title: Exploring the Synergies between Neuroscience and AI for Neuromorphic Edge Intelligence <br>

1. Introduction <br>
Neuromorphic edge intelligence represents a cutting-edge research field that aims to merge insights from artificial neural networks and biological neural networks to create more efficient and bio-plausible computing systems. This research proposal outlines our plan to investigate the synergies between neuroscience and AI, focusing on understanding brain computational primitives, developing scalable learning algorithms, and designing hardware-efficient neuromorphic devices. The ultimate goal is to advance the field of neuromorphic edge intelligence and pave the way for sustainable and impactful solutions. <br>

2. Objectives <br>

a. Exploiting Bi-Directional Interaction: The first objective is to leverage bi-directional interaction between neuroscience and AI. We will explore the bottom-up approach to identify brain computational primitives and scale them for AI-oriented workloads. Additionally, we will investigate the up-bottom direction to develop algorithms that are more amenable to hardware implementation. <br>

b. Achieving Hardware Efficiency: The second objective is to enhance hardware efficiency through bio-plausible mechanisms. We will focus on developing learning algorithms that align with neuroscience principles and utilize spiking neural networks. The aim is to reduce memory and computational costs while achieving high performance. <br>

c. Investigating Neuromorphic Edge Solutions: The third objective is to explore on-chip learning for inference devices, such as smartwatches, that require continuous adaptation over time. We will investigate temporal data processing for tasks like keyword spotting and navigation. Our goal is to design hardware-efficient solutions that are robust and flexible for real-world applications. <br>

3. Methodology <br>

a. Biologically-Inspired Learning Algorithms: We will start by investigating spike-time-dependent plasticity (STDP) and spike-dependent synaptic plasticity (SDSP) as potential starting points for learning algorithms. We will compare the efficiency and scalability of these algorithms in terms of memory requirements and computational complexity. <br>

b. Engineering Approaches: For AI-driven solutions, we will explore feedback alignment and direct feedback alignment algorithms. We will assess their hardware efficiency and scalability to identify the most suitable approach for neuromorphic edge devices. <br>

c. Chip Implementation: We will design and implement a neuromorphic chip that incorporates the selected learning algorithms. The chip will perform on-chip learning tasks, such as delayed supervision navigation and keyword spotting. The goal is to achieve hardware efficiency and demonstrate the feasibility of neuromorphic edge intelligence. <br>

4. Expected Outcomes <br>

a. Insights into Synergies: This research will provide valuable insights into the synergies between neuroscience and AI, shedding light on how these disciplines can benefit each other to create efficient and bio-plausible computing systems. <br>

b. Hardware-Efficient Learning Algorithms: We expect to develop learning algorithms that are hardware-efficient and suitable for on-chip implementation. These algorithms will serve as a basis for enhancing the performance of neuromorphic edge devices. <br>

c. Neuromorphic Chip Demonstration: The successful implementation and demonstration of a neuromorphic chip performing on-chip learning tasks will highlight the feasibility and potential of neuromorphic edge intelligence. <br>

5. Conclusion

By investigating the synergies between neuroscience and AI for neuromorphic edge intelligence, this research proposal aims to contribute to the advancement of bio-plausible computing solutions. The proposed methodology will lead to hardware-efficient learning algorithms and demonstrate the potential of on-chip learning for edge devices. Ultimately, this research will pave the way for innovative and sustainable neuromorphic edge intelligence solutions with wide-ranging applications in various fields.
