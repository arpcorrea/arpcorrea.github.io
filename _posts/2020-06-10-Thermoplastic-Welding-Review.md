---
title: "Review: On the Consolidation of Thermoplastic Welding"
excerpt: "A friendly Review on the Consolidation of Thermoplastic Welding process is presented in this link"
date: June 10, 2020
categories:
  - Review
tags:
  - Thermoplastic Welding
  - Thermoplastic Composite 
  - Consolidation
  - Review
---




The scope of this post is to share in a friendly language fundamentals of consolidation in thermoplastic welding process. First, let’s understand the meaning of “thermoplastic”. Thermoplastic is a type of polymer. Polymer? What is a polymer? Polymer is a class of material in which large molecules are built up by multiple small repeating units, called monomers, in a reactive chemical process.
 

Alright, so now we can get back and define thermoplastic! Thermoplastics can be considered as ensembles of randomly packed and entangled chains, in which their chain mobility is given by the monomer features, such as weight, compounds and polar groups. When heated, this chain entanglement becomes more flexible with increased mobility, enabling the material to soften and flow. 


<p>
    <img src="https://arpcorrea.github.io/assets/images/literature/thermoplastic.png" alt>
    <em>Thermoplastic Schematic Structure </em>
</p>

So now, consider that two or more thermoplastic independent parts, for now on called adherents, need to be assembled. This is trivial, we are everyday using screws, rivets or adhesives… is it?

Well, for high performance lightweight structures, mechanical fastenings methods exhibit problems arising from stress concentrations, thermal expansion coefficient mismatch and fabric damage induced by drilling, in addition to the negative impact of increased weight from the fasteners. Adhesive bonding, on the other hand, is incompatible with thermoplastic resins owing to their chemically inert properties, requiring excessive surface preparation.

To prevent these issues related to traditional techniques, welding, also known as fusion bonding, is considered as the most suitable process for joining thermoplastic composite parts. This process takes the advantage of uniform stress distribution, less sensitive to surface treatment, short cycle times and cost-effective process. The Defense and Space Group of the Boeing Company reported labour savings greater than 61% could be obtained by welding a composite wing structure as compared to a bolted one.

Thanks to their ability in softening and flowing, thermoplastics can be welded. Thermoplastic composite welding is defined as the joining of two or more thermoplastic parts together by softening and consolidating under pressure of their common interface. The efficiency of this welding is evaluated by comparing the weldline strength to the virginal bulk strength.



<p>
    <img src="https://arpcorrea.github.io/assets/images/literature/consolidation.PNG" alt>
	<em> First, adherents are heated to soften the material. Then, external pressure is applied, resulting in an intimate contact development between adherents. Simultaneously, healing occurs at the interfaces are into intimate contact.</em>
</p>


In the welding definition, one word might have caught your attention: “consolidating”. During consolidation, external heat and pressure are applied in order to enable two main phenomena: (I) intimate contact development and (II) interface healing. What do they mean? 

Let's start with the first phenomena, the intimate contact. The adherent’s surface is never smooth at any scale, showing a self-affine property. In the figure below, you can find a real-life roughness measured by confocal microscopy. 



<figure>
<img src="/assets/images/literature/roughness.png" alt="drawing"  style="width:500px;"/>
<figcaption>Random Roughness Measurement.</figcaption>
</figure>


In order maximize the contact area of two or more rough adherents, external pressure is applied in order to deform these asperities, like “spreading” them. Simultaneously, heat is applied in order to make the material more flexible and allow resin flow to fulfill the void-spots. This would, ideally, create a complete and tight mechanical contact, known as intimate contact, between the adherents.

On the modelling of this intimate contact phenomenon, the reader is here invited to have a more detailed read about it in a more technical literature. Beforehand, it is important to mention that modelling intimate contact is not trivial and is far from being a established and well-defined topic. Two analytical models are usually the most simple representation of the time-evolution of the intimate contact: Identical Asperities Model [Mantel and Springer(1992)] and Cantor Set Model. 

[Yang and Pitchumani (2011)], in which the real roughness is idealized in simple shape distribution. However, other more complex and reliable models considering the viscoelastic material response or even the rheology of the thermoplastic resin are available.

Great! We have already covered the first phenomena, the intimate contact. Let’s move forward and explore the second one, healing. When two thermoplastic materials are into intimate contact, chain interdiffusion across the interface is noticed, a process referred as healing or autohesion. Thus, the processes of intimate contact and healing are coupled in way that healing can occur only across areas of the interface that are into intimate contact.

The interface healing phenomena is based on the Reptation Theory [De Gennes (1971)] for bulk materials. In a straight forward explanation, this theory assumes that the polymer chain entanglement constrains single chains inside a “tube-like” region, in which are allowed to move back and forward along the curvilinear length of the tube. The following figure shows how  single chain disengages itself from the initial tube.




<figure>
<img src="/assets/images/literature/reptation.PNG" alt="drawing" caption="This is a figure caption." style="width:700px;"/>
<figcaption>At the beginning of the process, t=t0, the chain is totally encompassedby the tube. At a certain time t=t1, the chain ends escape from the tube. This disengagement continues as time progresses (t=t2), untilthe reptation time tr is reached, when the entire polymer chain scapes from the tube, characterizing full healing.</figcaption>
</figure>


At the beginning of the process, t0=0, each single chain, represented by the thin solid line in Figure \ref{fig:reptation}, is totally encompassed by a tube, which represents the chain constraints imposed by the entanglement of neighbouring chains. At a certain time t=t1 the chain ends escape from the original tube, forming the “minor chains”. The length "l" of the minor chain increases with time and reaches L at the reptation time t_r, when the entire polymer chain escapes from the tube. 


Adapting the original reptation theory (developed for the bulk material), Wool et al (Wool and OConnor (1981)] extended this theory to explain the motion of molecular chains across the weld interface. Initially, two adherents are assumed to be in perfect contact at the interface, as shown in the following figure (note that only the molecules on one side of the interface are illustrated for clarity).



<p>
    <img src="https://arpcorrea.github.io/assets/images/literature/reptation_welding.PNG" alt>
    <em>At the beginning of the processt =t0, the minor chains have zero length. As time proceeds, the lengths of the minor chains grow(t=t1) and some of them move across the interface (t=tr).</em>
</p>


At t=t0, the chains have no minor chains diffusing through the interface, and therefore, are represented by dots. As time proceeds, the lengths of the minor chains grow, and some of thechains move across the interface with an interpenetration distance &#935;, which contributes to buildup a weldline strength. At the reptation time, the interpenetration and entanglement of all the polymer chains are fully developed and the molecular configuration at the interface is identical to the virginal bulk material.

Finally, The weld strength, &#963;, is proportional to the interpenetration depth &#935;, which is related to the minor chain length &#935; ~  l^(1/2). The ultimate weld strength, &#963;∞, is achieved when the interpenetration depth and the minor chain length reach their maximum values &#935;∞ and L, respectively. 

That is it! If you need a more technical information about these topics <a href="mailto:andre.rittner-pires-correa.1@ens.etsmtl.ca?subject=[Blog]">send me an email </a>. I will be happy to support you with relevant works.
