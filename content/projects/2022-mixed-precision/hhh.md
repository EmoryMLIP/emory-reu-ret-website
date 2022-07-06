This post was written by Xiaoyun Gong, Yizhou Chen, and Xiang Ji and published with minor edits. The team was advised by Dr. James Nagy. In addition to this post, the team has also created slides for a [midterm presentation](), a [poster blitz]() video, [code](), and a [paper]().

During our summer research at Emory University 2021 REU/RET program, our group focused on the algorithmic diagnosis of Chiari malformation from DENSE MRIs. We created an algorithm that can accurately and efficiently segment the cerebellum and brain stem from a magnitude image and use displacement data to classify whether or not a patient has the Chiari malformation. In doing so, we investigated two approaches; one that segments the given image by aligning and comparing the image to a known atlas and another that segments through deep learning.

## Background: Why Low Precision?

