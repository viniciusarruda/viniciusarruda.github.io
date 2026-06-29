# Wasserstein CycleGAN (Optimal Transport)

Type: Research
Status: Backlog
Tags: CV, DL
Date Added: February 26, 2026
Priority Score: 11.71875%
Effort: 5
Impact: 5
Learning: 5
Visibility: 5
Longevity: 4
Confidence: 2
Normalized Value: 0.9375
Normalized Confidence: 0.25
Normalized Effort: 1

The idea is to use Wasserstein distance as the cycle consistency loss instead of the L1 loss. 

There is one implementation someone did, but I didn’t find any paper about it. 

The hypothesis is, when using two different dataset domains that are not related but not too unrelated (this I really need to find a better definition) the image translation process will output the closest (thus, the motivation of using optimal transport) output of the input as possible. 

As an example, to confirm the hypothesis:

- Suppose we have a dataset A of handwritten digits and a dataset B of handwritten vowels.
- With a normal CycleGAN, my hypothesis is that there's no guarantee the digit 1 would always map to the letter i, which are the closest in the lens of OT.
- With the OTW CycleGAN, my hypothesis is that always the digit 1 will map to the letter i.

This idea spark emerged while thinking about 101 dalmatians, on how close the dogs looks like their humans. 

Then, thinking more scientifically, humans tend to see patterns everywhere. We see faces looking to the front of the cars and buildings. We see objects in clouds. We feel that objects, animals, and etc remind us of a face of someone. 

There is also an experiment I’d like to do is to apply the L1 loss or Wasserstein distance in the (input, output) pair just for sake of curiosity on what would happen. 

Here, I’m interested in Style Transfer but keeping the “Identity”.