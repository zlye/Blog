---
layout: post
title: 'Analysis of Genetic Structural Variation Part 1'
date: 2023-11-06
---

![Utagawa Hiroshige 1855 Japan, National Museum of Asian art]({{ site.baseurl }}/assets/images/hiroHI_small.png "an image title"){:style="display:block; margin-left:auto; margin-right:auto"}
*Utagawa Hiroshige 1855 Japan, National Museum of Asian art* 

Rice is one of the most important crops in the world, billions of people eat rice everyday as their main source of calories. I studied rice genomics and evolution for my doctoral research. Specifically, I researched discovery and analysis of structural variation in a population of rice varieties.

In popular science writing and on the news, we often hear about how genetic differences cause different traits in an individual. But the specific type of genetic difference, also called a genetic variant is not always explained explained in detail. Imagine a genome is like a book, it contains the complete genetic code of an individual, in the form of letters A, C, G, and T. Each individual's book varies by a different letter here an there, or an insertion of an extra couple of letters here and there. These small differences are like typos in the book. Structural variants are much larger genetic differences between individuals. Structural variants are a deletion or duplication of a pharagraph or entire pages in the genome book. Structural variants can also comprise the rearrangement of pharagraphs, pages and chapters into alternate orders or backwards. In a rearrangement,all the information is still there but out of order. This class of genetic variation can encompass big parts of the book!

Structual variants take many forms and are challenging to understand. Overall structual variants effect more genetic sequence than the "typo" class of mutations. Therefore structural variants can be extremely bad for an individual and are often associated with severe and complex diseases. As a result, they are generally rare in the population, although each individual has some form of structural variation.

Over the past 10 years there has been an explosion of interest in structural variation. Many structural variants have been discovered that are responsible for important traits in domesticated plants and animals, for example gene duplications cause differences in coat color in sheep, cattle and pigs. In rice, a duplication is causes increased seed. These are just two individual examples of how structural variants influence traits. You can read about many more examples, and learn about deeper in the
[review I published] (https://www.cell.com/trends/plant-science/fulltext/S1360-1385(19)30015-9?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS1360138519300159%3Fshowall%3Dtrue#secsect0040)

In my research I wanted to gain understanding greater than anectodal examples. I decided to study structural variation as a broad phenomenon using rice as a study species.

###These are two key questions I answered through my research:###
*1. Where are structural variants in the genome?*  
*2. How do structural variants affect gene expression?*

Part I. How are structural distributed across the genome?

![Geographic origin of study samples]({{ site.baseurl }}/assets/images/map_screenArtboard 1@1.5x.png "an image title"){:style="display:block; margin-left:auto; margin-right:auto"}
*This map shows the geographic origins of each landrace sample I used in my research. Rice is a diverse species adapted to many types of environments and these samples were chosen to reflect that diversity. The colors show the major different subtypes of rice.*

I discovered structural variants in a population of rice landraces. Landraces are traditional varieties of rice, and have a high level of genetic diversity. My samples came from all around the world, their genomes were sequenced by several of my colleagues. All together I started with 4 TB of raw genome sequence data! I developed a customized bioinformatics pipeline to discover structural variants using a high performance computing cluster.  

*You can checkout at the pipeline on
[git](http://github.com/zlye/RVE/)*
it took over a year to test and develop!

Using the pipeline I discovered over 50,000 structural variants within a population of 214 rice landraces. The pipeline is complex - but I learned a lot from these 50,000 structural variants!

Let’s skip to the interesting parts - the results and what they show about rice genomics!

![Distibution of Structural variant sizes]({{ site.baseurl }}/assets/images/SizeDist2x.png){:style="display:block; margin-left:auto; margin-right:auto"}
*A summary of the number of structural variants and their size are measured as base pairs for three types of structural variants*

Most of the structural variants I discovered are deletions and small variants are more common for deletions and duplications. I found far more deletions than other types of structural variants because deletions are easier to identify using the particular type of genome sequence data I had for my samples. The pattern in structural variants' size however, is easily explained: the larger the variant the more likely it is to interfere with the overall function of the organism - when larger parts of the "genomic book" get deleted the blueprints for life don't work.

At some point, you may have heard that most of the genome is "junk DNA" while this isn’t entirely true, it is true that some parts of the genome are much more important than others.

The genome can be divided into many different classes, in this analysis I divided the rice genome into 3 different **functional classes:**
 - **Coding:** parts of genes that contain the code for building proteins. 
 - **Intron:** parts of genes that do not code for proteins
 - **Intergenic:** regions between gene

Proportion of genomic functional classes that each class of structural variant overlaps with.

![Proportion of Structural variants overlappinh each genomic class]({{site.baseurl}}/assets/images/Fractions_post.png){:style="display:block; margin-left:auto; margin-right:auto"}
*This graph shows the proportion of genomic functional classes that each type of structural variant overlaps with. This graph also includes a “whole gene” category for when an entire gene (coding + introns) is affected by a structural variant. For example, the inversion row shows that ~25% of inversions overlap with whole genes. The “break end” type of structural variant is a catch-all for variants that can’t be classified as duplications, deletions, or inversions.* 

This graph reveals a number of interesting patterns:
1. It is clear that the majority of structural variants occur in intergenic regions - this makes sense - the rice genome is about 391 million basepairs long and genes are predicted to covers 111 million base pairs. 
2. Inversions overlap far more genes that the other classes

These two observations are predicted from an evolutionary standpoint. If stuctural variants affect many base-pairs at a time it is more likely to partialy or completely change a gene - even remove it all together! Deleting a gene could have severe negative impacts for the organisms health so fewer deletions should overlap genes. On the other hand, inversions, do not delete genes, they just order them differently and the gene is more likely to still function therefore inversions are tollerated in genes.

*Are structural variants more or less likely to occur in functional sequence?*

I wanted to test if stuctural variants are randomly distributed in the genome, or if they're less likely to occurr in genes regions as predicted by evolutionary theory. To test this hypothesis I ran a simulation to create an enrichment score. The enrichment score shows if structural variants overlap a given sequence types more or less frequently than expected by chance. The enrichment score is calculated by placing the structural variants randomly across the genome 100 times and then counting the number of structural variant base-pairs that overlap each functional class. The ratio of the median random overlap base-pairs to the true total base-pair overlap is the enrichment score. 

![Structural variant overlap enrichment]({{site.baseurl}}/assets/images/FeatureEnrich1.5x.png){:style="display:block; margin-left:auto; margin-right:auto"}
*This shows the enrichment score for each class of Structural variant: break-end (BND), deletion (DEL), duplication (DUP), and inversion (INV). The enrichment is calculated for each genomic class (referred to as a feature here). Values below 1 indicate a depletion (lower likelihood of overlap) and greater than 1 indicate enrichment (higher likelihood of overlap).*


The enrichement analysis shows SVs are more likely to occur in intergenic regions and depleted from introns and exons. Interstingly they're also more likely to occur in intronic regions than coding regions. Again this makes sense - coding regions are more "important" to creating the proteins that intronic regions, althought the intronic regions still play a role gene regulation and occurr adjacent to the coding regions.

*check out enrichment analysis code 
[here](http://github.com/zlye/SV_feature_enrichment/)*

This post is just a snapshot into one element of my research into structural variants. As a biologist, I get most excited thinking about evolutionary processes. This kind of simple analysis demonstrates how evolutionary processes shape the patterns of structural genetic variation in genomes - which extends from rice to humans and many other organisms. 
