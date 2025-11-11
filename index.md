# DSC180A Methodology Assignment 4

**Name:** Idhant Kumar 
**Email:** ikumar@ucsd.edu

**Section:** A02
**Mentor:** Gupta

---

## Prompts

**What is the most interesting topic covered in your domain this quarter?**

The most interesting topic I encountered this quarter was how approximate computing can bridge the gap between theoretical algorithm design and practical hardware implementation. 
When I first learned about the L-Mul algorithm replacing floating-point multiplication with addition-based operations, I was skeptical about whether such an approximation could maintain acceptable accuracy in real applications. 
However, observing it achieve 97.01% accuracy compared to a 97.02% baseline on MNIST fundamentally changed my understanding of precision requirements in neural networks. 
What proved particularly compelling was discovering that neural networks exhibit natural tolerance for bounded arithmetic errors - the approximation doesn't compound catastrophically as one might initially expect. 
The most valuable aspect of this work was navigating multiple levels of abstraction, from understanding the mathematical foundations of the algorithm to implementing it in Verilog hardware description language to validating it within a complete neural network pipeline. 
This experience highlighted how much potential exists at the intersection of computer architecture and machine learning, particularly in challenging the assumption that higher precision always yields better results.

**Describe a potential investigation you would like to pursue for your Quarter 2 Project.**

For Quarter 2, I would like to investigate whether L-Mul's effectiveness extends beyond simple architectures to modern transformer-based models. 
My research question would be: "Which components of transformer architectures are sensitive to L-Mul's approximation error, and which operations can tolerate approximate arithmetic without significant accuracy degradation?"
For data sources, I would utilize pre-trained transformer models from Hugging Face (BERT-base or GPT-2 small as starting points) and evaluate performance on standardized benchmarks such as the GLUE tasks. 
Additionally, I would conduct hardware synthesis using OpenROAD or similar tools to obtain quantitative measurements of area, power, and timing characteristics rather than relying solely on simulation estimates.
My approach would involve systematically replacing standard multiplication operations with L-Mul in different transformer components - attention mechanisms (Q/K/V projections), feedforward layers, and layer normalization. 
For each configuration, I would measure both accuracy impact and projected hardware savings. The goal would be to construct a "sensitivity map" identifying which operations can safely use approximate arithmetic and which require full precision. 
This would enable mixed-precision accelerator designs where critical computational paths maintain standard multiplication while less sensitive operations leverage L-Mul's efficiency benefits. 
I believe this investigation would provide actionable insights for designing practical inference accelerators rather than purely academic validation.

**What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**

Looking back at our Quarter 1 approach, I would prioritize hardware synthesis and characterization earlier in the development cycle rather than spending extensive effort optimizing the simulation infrastructure. 
While developing the Icarus Verilog and Python integration was valuable for functional validation, it consumed significant time that could have been allocated to synthesis tools like OpenROAD or Verilator, which offer better performance and more direct paths to hardware metrics.
I would also refine our accuracy testing methodology. Our evaluation used uniformly distributed random operands in the range [-10,000, +10,000], which yielded a 1.51% average error. However, this distribution doesn't reflect actual neural network weight and activation patterns, which typically exhibit much smaller magnitudes and specific clustering behaviors. A more representative approach would involve profiling weight distributions from trained models and testing L-Mul specifically on those realistic value ranges. This would provide more honest error characterization relevant to actual deployment scenarios.
Finally, I would expand our validation beyond MNIST to include more complex tasks and architectures. While MNIST was appropriate for initial debugging and proof-of-concept, it represents a relatively simple classification problem. Testing on CIFAR-10 with a convolutional architecture or a small language modeling task would have provided more generalizable insights about L-Mul's viability across different network types and problem domains.

**What other techniques would you be interested in using in your project?**

I am particularly interested in gaining hands-on experience with the complete ASIC design flow, including synthesis, place-and-route, and power analysis with industry-standard or open-source EDA tools. Understanding timing closure, power estimation methodologies, and area optimization techniques would bridge the gap between our simulation-based validation and realistic hardware implementation.
I would also like to explore quantization-aware training techniques adapted for approximate arithmetic. Our current approach trains models using standard floating-point operations and then substitutes L-Mul during inference. However, if the training process explicitly accounts for L-Mul's approximation characteristics, the network might learn representations that are inherently more robust to these specific arithmetic errors. PyTorch's quantization APIs could potentially be adapted for this purpose.
On the architecture side, I am interested in implementing systolic array designs where L-Mul replaces traditional multiply-accumulate units in each processing element. This would provide a more realistic evaluation context that reflects how production accelerators (such as Google's TPU) actually structure matrix operations, rather than testing individual multiplication operations in isolation.
Finally, I would benefit from deepening my understanding of hardware description languages and digital design principles. Developing greater fluency with Verilog would allow me to focus on architectural decisions and optimization rather than struggling with language syntax and simulation semantics during implementation.
