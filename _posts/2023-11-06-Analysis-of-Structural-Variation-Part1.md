---
layout: post
title: 'Analysis of Genetic Structural Variation Part 1'
date: 2023-11-06
---

![2Utagawa Hiroshige 1855 Japan, National Museum of Asian art]({{ site.baseurl }}/assets/images/hiroHI_blog.jpg "an image title"){:style="display:block; margin-left:auto; margin-right:auto"}

One of the main topics of my Ph.D. research was the discovery and analysis of structural variation in rice. Structural variation a unique and interesting type of genetic variation. If we use a book as a metaphor for the genome, that is, the complete genetic code of an individual, individuals might vary by a letter change, or an insertion of a letter or two. Structural variants are much larger mutations, they might include a deletion or duplication of a pharagraph, or a rearrangement of many pages. Given that they affect more sequence structural variants can be extremely bad for an individual and are rare in the population in humans structural variants are associated with many severe and complex diseases.

Over the past 10 years there has been an explosion of interest in structural variation. Many structural variants have been discovered that are responsible for important traits in domesticated plants and animals, for example gene duplications cause differences in coat color in sheep, cattle and pigs. In rice, a duplication is associated with increased seed size. These are just two individual examples of how structural variants influence traits. 
#T1
[here] (https://www.cell.com/trends/plant-science/fulltext/S1360-1385(19)30015-9?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS1360138519300159%3Fshowall%3Dtrue#secsect0040){:target="_blank"}{:rel="noopener noreferrer"}
#T2
You can read about more examples, and learn about deeper in the review I published
[here] (https://www.cell.com/trends/plant-science/fulltext/S1360-1385(19)30015-9?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS1360138519300159%3Fshowall%3Dtrue#secsect0040)
#T3
![here] https://www.cell.com/trends/plant-science/fulltext/S1360-1385(19)30015-9?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS1360138519300159%3Fshowall%3Dtrue#secsect0040)
#T4
[here] https://www.cell.com/trends/plant-science/fulltext/S1360-1385(19)30015-9?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS1360138519300159%3Fshowall%3Dtrue#secsect0040)
#T5
You can read about more examples, and learn about deeper in the review I published
[here](https://www.cell.com/trends/plant-science/fulltext/S1360-1385(19)30015-9?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS1360138519300159%3Fshowall%3Dtrue#secsect0040)

In my research I wanted to study more than the known anectodal examples. Instead I wanted to study structural variation as a broad phenomenon - **what's the big picture?**

These are two key questions I answered through my research:  
*1. Where are structural variants in the genome?*  
*2. How do structural variants affect gene expression?*

Part I. How are structural distributed across the genome?

![Geographic origin of study samples] ({{ site.baseurl }}/assets/images/samplemap4a_edit.png "an image title"){:style="display:block; margin-left:auto; margin-right:auto"}

I discovered structural variants in a population of rice landraces. Landraces are traditional varieties of rice, and have a high level of genetic diversity. My samples came from all around the world, their genomes were sequenced by several of my colleagues.All together I started with 4 TB of raw genome sequence data! I developed a customized bioinformatics pipeline to discover structural variants using a high performance computing cluster. You can checkout at the pipeline on git zlye/RVE - it took over a year to test and develop!

Using the pipeline I discovered over 50,000 structural variants within a population of 214 rice landraces. The pipeline is complex - but I learned a lot from these 50,000 structural variants!

Let’s skip to the interesting parts - the results and what they mean!

![Distibution of Structural variant sizes]({{site.baseurl}} /assets/images/SV_Size_dist_edit.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

Most of the variants discovered are deletions, and the majority of structural variants are small.

At some point, you’ve probably heard that most of the genome is junk DNA while this isn’t entirely true, it is true that some parts of the genome are much more important than others.
The genome can be divided into many different classes, in this analysis I divided the rice genome into 3 different _functional classes_:
 - **Coding:** parts of genes that contain the code for building proteins. 
 - **Intron:** parts of genes that do not code for proteins
 - **Intergenic:** regions between gene

This graph shows the proportion of genomic _functional classes_ that each type of structural variant overlapps with. 

![Proportion of Structural variants overlappinh each genomic class]({{site.baseurl}}/assets/images/Fractions_edit2.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

It is clear that the majority of structural variants occur in intergenic regions - this makes sense - the rice genome is about 391 million basepairs long and genes are predicted to covers 111 million base pairs. It is also predicted from an evolutionary standpoint. If stuctural variants affect many base pairs at a time a structural variant in a gene could partialitty, or completely change a gene - even remove it all together. Deleting a gene could have severe negative impacts for the organisms health so there is throught to be strong evolutionary pressure for structural variants not to overlap genes.

*Are structural variants more or less likely to occur in functional sequence?*
I wanted to test if stuctural variants are randomly distributed in the genome, or if they're less likely to occurr in genes regions as predicted by evolutionary theory.

To test this hypothesis we ran a simulation to create an enrichment score. The enrichment score is generated by placing the structural variants randomly across the genome 100 times and then calculating the number of base pairs that overlap each functional class. The ratio of the median random overlap base pairs to the true overlap is the enrichment score. 

![Structural variant overlap enrichment]({{site.baseurl}}/images/SV_overlap_enrichment_sim_result.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

The enrichement analysis shows SVs are more likely to occur in intergenic regions and depleted from introns and exons. Interstingly they're more less likely to occur in intronic regions than coding regions. Again this makes sense - coding regions are more "important" to creating the proteins that intronic regions, althought the intronic regions still play a role gene regulation and occurr adjacent to the coding regions.

*check out enrichment analysis code [here] <http://github.com/zlye/SV_feature_enrichment/>*
check out enrichment analysis code [here] <http://github.com/zlye/SV_feature_enrichment/
