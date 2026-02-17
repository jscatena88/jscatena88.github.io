+++
title = "Molded Silicone Parts for a Vintage Honda CJ360T"
date = 2024-02-25
description = "Using 2-part silicone and 3D printed molds to recreate out-of-production rubber bushings for a 1976 Honda CJ360T."

aliases = ["/2024/02/25/molded-silicone-parts-for-a-vintage-honda/"]

[taxonomies]
tags = ["3dprinting", "motorcycle"]
+++

## Background

I own several motorcycles, and in my pursuit of novelty I usually buy and sell bikes fairly regularly. Most bikes stick around for 1-3 riding seasons on average. However, one bike I can never bring myself to sell. It is the first motorcycle I ever bought (back in 2014) a 1976 Honda CJ360T I've named Josie.

![Josie Side Profile](/assets/molded_silicone/IMG_20180630_195125.jpg)

As reliable as these old hondas are they are still 50 year old bikes and tend to require a fair bit of maintenance and tinkering, but that is half the fun. This post is my experience using tools in my home office to remake an out of production rubber part for my bike.

### The Part

On each side of the CJ is an airbox that holds the air filter and feeds air into the carbs. They are held onto the bike with 3 bolts (Part #20). To keep vibrations down there is a rubber bushing that isolates the airbox from the frame (part #16). Finally, there is a metal washer/collar piece that is the interface between the bolt and the bushing. Refer to the part diagram below for a visual representation.

<figure>
  <img src="/assets/molded_silicone/PartDiagram.png" alt="Part Diagram">
  <figcaption>Diagram from <a href="https://www.partzilla.com/catalog/honda/motorcycle/1976/cj360t-a/air-cleaner-side-cover">Partzilla</a></figcaption>
</figure>

The rubber bushings on my motorcycle are all either missing or in various states of disintegration. The Honda part number of the bushing is `31403-323-000` and while it is no longer manufactured, some suppliers do have new-old-stock examples available.

<figure>
  <img src="/assets/molded_silicone/HON-31403-323-000-2.jpg" alt="OEM Part">
  <figcaption>Picture of the original part <a href="https://www.partswarehouse.com/Honda-Rubber-HON-31403-323-000-p/HON-31403-323-000.htm">courtesy of PartsWarehouse</a></figcaption>
</figure>

They seem to go for ~$4 each with shipping on top of that. I need six of them which would come to $24 plus shipping (~$8 when I looked). This got me thinking about trying to produce these parts myself. These are not the only degrading rubber parts on a bike as old as this and some of those parts aren't available anymore at all. So a success here would allow me to make quite a few parts for this bike.

### The Plan

My plan was to use 2 part silicone and cast it in a 3d printed mold. This type of silicone is most often used for making molds however a recent [video on the FormLabs youtube channel](https://youtu.be/xDoUztSoyvk) got me thinking about using it with a 3d printed mold to produce a final part. I ordered a cheap kit on Amazon with seemingly decent reviews, and started 3D modeling while awaiting its arrival.

## Mold V1

### Design

I went to Fusion 360 and started by modeling the bushing itself. From there I modeled a cube over the part and subtracted out the bushing from the middle. This left me with a solid cube with a negative space in the middle in the shape of the part I wanted. I split this cube into 3 parts, one cylinder for the middle and two halves that hold the cylinder in place. The two halves got a set of four holes so they could be bolted together with M3 hardware. For each half I added a hole into the molding chamber, one for silicone to be injected into and the other for air to escape from. To that end, I placed one hole on the bottom and one on the top.

![Bushing Model](/assets/molded_silicone/Bushing.PNG)

![V1 Split](/assets/molded_silicone/V1Split.PNG)

![V1 Final](/assets/molded_silicone/V1Final.PNG)

My plan was to use a large syringe to inject the silicone into the mold. I sourced a kit off amazon that had large syringes and a length of tubing. I sized the holes on the outside of the mold to accept the tubing.


<figure>
  <img src="/assets/molded_silicone/PXL_20240225_181432659.MP.jpg" alt="Mold V1">
  <figcaption>Mold V1 after printing in Gray PLA on my Prusa MK2</figcaption>
</figure>


### Casting

Upon receiving my silicone, I jumped right into trying my mold out. After filling the mold the part needed to cure overnight. However, I quickly realized I needed some way to seal off the fill hole of the mold. I ended up wrapping the whole mold in strips of duct tape to try and seal off both holes, but the duct tape did not stick well to the silicone covered mold and the seal was anything but liquid tight. Additionally, while the 2 part silicone claims a 6 hour cure time I found that it was still very liquidy even after 6 hours (based on the leftovers in the mixing cup). Looking at reviews for the product this seems to be a common complaint. Thankfully, since this is platinum-cure silicone the cure can be sped up with heat. I put the mold and mixing cup of leftovers in a warm spot and by the next morning they were set up.

### Results

Finally it was time to de-mold the parts and the results were less than ideal. However, that was to be expected for a first shot, and the lessons I learned allowed me to quickly iterate my next attempt.

![V1 Results](/assets/molded_silicone/PXL_20240225_181503049.MP.jpg)

A large amount of air ended up being trapped in the mold and because of that ~1/3 of the part was just missing. I think this had two causes; first, the poor seal of the duct tape covering on the fill port let some silicone seep out and air took its place. Second, bubbles in the silicone mix rose to the surface becoming one large air pocket.

The first issue can be addressed with a better designed mold. For the second, I do not have access to a vacuum chamber which is the proper way to deal with bubbles in the mix. However the mix I am using advertises its ability to degas itself after pouring. This is likely accomplished with its relatively low viscosity and long cure time.

## Mold V2

### Design

Armed with the lessons learned from my first mold design and my first casting experience I tried again. This time I decided to make the mold with an open top. This would allow bubbles in the mix to rise to the surface without getting trapped. Pouring the mix in from an open top would also mean there is no fill port to seal.

The new design started out just as before with a cube that had the model of the busing itself subtracted from the middle. Next I cut out the top of the mold with a circle just barely wider than the bushing itself (this was to create a lip I could use to gauge the height during the pour). Next, I split the cube with very shallow cone shape to create a separate top piece. I split this top in half lengthwise and added bolt holes. This gave me 3 pieces; a bottom with the pug for the central hole and two top halves that could be pulled away from the side. By pulling away from the side the mold could cast the undercut of the bushing shape and still be pulled away after curing.

Finally, I decided to try for 2 parts in one go this time since the smallest batch of mix you can feasibly make is quite a bit more than what is needed for a single bushing, and any leftovers are effectively just a waste. To do that I just copied all three pieces, shifted the copies over and combined them to the original bodies.

![V2 Split 1](/assets/molded_silicone/V2Split.PNG)
![V2 Split 2](/assets/molded_silicone/V2Split2.PNG)

![V2 Final](/assets/molded_silicone/V2Final.PNG)


![Mold V2 First Picture](/assets/molded_silicone/PXL_20240225_184117452.MP.jpg)
![Mold V2 Second Picture](/assets/molded_silicone/PXL_20240225_184133340.MP.jpg)

### Casting

This time casting went much smoother. I let the silicone sit for about 30 minutes after mixing so that most of the bubbles could dissipate before I tried pouring it. I then poured the mix into the mold, pouring slowly, filling the bottom completely before letting any silicone get into the top. I did this to avoid trapping air under the shelf in the mold. The seal between the mold pieces isn't perfect but the mix is viscous enough to not leak out. Finally, I put the poured molds on to my 3d printer's build plate with the heat set to 45°C and placed a cardboard box over them.

### Results

After the pieces were fully cured I was able to remove them from the mold without too much difficulty and the results were much better. Below is a picture of the two pieces after I trimmed the flashing off of them.

![v2 results](/assets/molded_silicone/PXL_20240225_190009421.MP.jpg)

There are still quite a few bubbles in the parts, however they seem solid enough to be usable. For my next attempt I will probably let the silicone sit even longer before pouring it and see if that helps.

## Wrap Up

I have yet to try these parts on my bike. I need to cast 4 more and then I will try them out. I have some concerns about their durability as they quite a bit softer than I imagine the OEM parts are but only time will tell. Either way I am quite impressed with how easy this process is and already have at least one other part I want to try remaking. I am also planning on looking into pigments for 2 part silicone so I can make the parts black and get a more OEM look. I will try to post an update on how these parts work in the field and any other parts I end up making with the same process.
