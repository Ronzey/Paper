# Background
## Diffrence with conventional ML
Meta learning improve a learning algorithm over **multiple leraning episodes**, 
while conventional ML considers the process of improving model predictions over **multiple data instances**.

## Salient Characteristic
The salient characteristic of contemporary neural-network
meta-learning is an explicitly defined **meta-level objective**,
and **end-to-end optimization** of the inner algorithm with
respect to this objective.

## Process
Often, meta-learning is conducted
on learning episodes sampled from a task family, leading
to a base learning algorithm that is tuned to perform well
on new tasks sampled from this family. This can be a
particularly powerful technique to improve data efficiency
when learning new tasks. 

# Inspiration
Parameter Initialization is widely used for few-shot learning, where A good initialization
is just a few gradient steps away from a solution to any
task T drawn from p(T).
