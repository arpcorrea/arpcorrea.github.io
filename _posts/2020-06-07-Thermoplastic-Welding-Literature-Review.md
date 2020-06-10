---
title: "Literature Review: Thermoplastic Welding: on the Consolidation step"
excerpt: "A Literature Review on the Consolidation step of a thermoplastic welding process if presented in this link"
date: June 08, 2020
categories:
  - Literature Review
tags:
  - Thermoplastic Welding
  - Thermoplastic Composite 
  - Consolidation
---


The scope of this post is to diffuse in a friendly language the fundamentals of consolidation in thermoplastic welding process. First, let’s understand the meaning of “thermoplastic”. Thermoplastic is a type of polymer. Polymer? What is a polymer? Polymer is a class of material in which large molecules are build up by multiple small repeating units, called monomers, in a reactive chemical process.
 
Alright, so now we can get back to thermoplastic! Thermoplastics can be considered as ensembles of randomly packed and entangled polymer chains, whose mobility is driven by the monomer features (such as weight and compound) and polar groups. Under heating, these entangled chains gain more mobility, enabling the material to soften and flow. 

Cool! We have already defined the first part of the work: thermoplastics. So now, consider that two or more independent parts, for now on called adherents, need to be assembled. This is trivial, we are everyday using screws, rivets or adhesives… is it?

Well, mechanical fastenings methods exhibit problems arising from stress concentrations, thermal expansion coefficient mismatch and fabric damage induced by drilling, in addition to the negative impact of increased weight from the fasteners. Adhesive bonding, on the other hand, is incompatible with thermoplastic resins owing to their chemically inert properties, requiring excessive surface preparation.

To overcome these limitations, thermoplastics can be welded, thanks to their ability in softening and flowing, as previously mentioned. Thermoplastic composite welding is defined as the joining of two or more parts together by softening and consolidating under pressure of their common interface. The efficiency of this welding is evaluated by comparing the weldline strength to the virginal bulk strength.


![GitHub Logo]({{ site.url }}/assets/images/literature/consolidation.PNG)

In the welding definition, one word might have caught your attention: “consolidating”. During consolidation, external heat and pressure are applied in order to enable two main phenomena: (I) intimate contact development and (II) interface healing. What do they mean? 

The adherent’s surface is never smooth at any scale, showing a self-affine property. In the figure below, you can find a real-life roughness measured by confocal microscopy. 


![GitHub Logo]({{ site.url }}/assets/images/literature/roughness.png)

Once the reader understood that the adherent’s surface is rough, lets continue the explanation over intimate contact. In order maximize the contact area of two or more adherents, external pressure is applied in order to deform these asperities, like “spreading” them. Simultaneously, heat is applied in order to make the material more flexible and allow resin flow to fulfill the void-spots. This would, ideally, create a complete and tight mechanical contact between the adherents.

On the modelling of this intimate contact phenomenon, the reader is here invited to have a more detailed read about it in a more technical literature. Beforehand, it is important to mention that modelling intimate contact is not trivial and is far from being a established and well-defined topic. Two analytical models are usually the most simple representation of the time-evolution of the intimate contact: Identical Asperities Model [Mantel and Springer(1992)] and Cantor Set Model 

[Yang and Pitchumani (2011)], in which the real roughness is idealized in simple shape distribution. However, other more complex and reliable models considering the viscoelastic material response or even the rheology of the thermoplastic resin are available.

Great! We have already covered the first phenomena, the intimate contact. Let’s move forward and explore the second one, healing. When two thermoplastic materials are into intimate contact, a chain interdiffusion across the interface is noticed, a process referred as healing or autohesion. Thus, the processes of intimate contact and healing are coupled in way that healing can occur only across areas of the interface that are into intimate contact.

The interface healing phenomena is based on the Reptation Theory [De Gennes (1971)] for bulk materials. In a straight forward explanation, this theory assumes that the polymer chain entanglement constrains single chains inside a “tube-like” region, in which are allowed to move back and forward along the curvilinear length of the tube. The following figure shows how  single chain disengages itself from the initial tube.

![GitHub Logo]({{ site.url }}/assets/images/literature/reptation.PNG)
Adapting the original reptation there (developed for the bulk material), Wool et al (Wool and OConnor (1981)] extended this theory to explain the motion of molecular chains across the weld interface. Initially, two adherents are assumed to be in perfect contact at the interface, as shown in the following figure (note that only the molecules on one side of the interface are illustrated for clarity).

![GitHub Logo]({{ site.url }}/assets/images/literature/reptation_welding.PNG)

At t=t0, the chains have no minor chains diffusing through the interface, and therefore, are represented by dots. As time proceeds, the lengths of the minor chains grow, and some of thechains move across the interface with an interpenetration distance X, which contributes to buildup a weldline strength. At the reptation time, the interpenetration and entanglement of all the polymer chains are fully developed and the molecular configuration at the interface is identical to the virginal bulk material.


