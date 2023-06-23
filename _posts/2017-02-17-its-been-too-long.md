---
title: It's Been Too Long...
date: Feb 17, 2017
tags:
  - system-administration
---

Way too long. I really didn't have any motivation to get back into working on my server for a long time now, but finally I was able to expend a Second Wind and get things fixed up. For years I have co-located a server out of the FDC Servers data center in Chicago. It was a great deal for a long time, and last year the price became too much. I don't make money from this, it is just a hobby for me, so there really was no point in continuing that relationship.

I was able to find a place to host a little closer to home, but by the time I hooked everything up, I lost a disk on the server. I had the disks in RAID-5, so no real impact; the server auto-recovered using the spare drive. There was just one problem with the change in hosting locations...I no longer have access to 6 IPv4 addresses. I am limiting myself to one, which means the sweet configuration I used to run just doesn't make sense anymore.

The previous configuration looked a little something like this:

[!|Original System Architecture]


It served it's purpose well, but I don't see a need for it anymore. I don't have separate IPs to delegate to specialize VMs. I have always run a RHEL server, but I have become something of a snob when it comes to the filesystem. I have grown to really love ZFS, but no Linux distro as of date uses it for the root filesystem.  I could go OpenIndiana, but my experience is central to Linux. So, I am switching the entire game plan to use Docker containers of all things running on RHEL with a custom configured root filesystem using ZFS in RAIDZ-2.

I am also getting out of the business of self-hosting my Authoritative DNS servers; I have moved to Google Domains to manage them. While it was fun to create the zone files, my hobby interests have changed in the past couple of years. I married my girlfriend from college. We bought a house. And we got an adorable malamute. Having your own property really puts priorities into perspective. It's expensive to furnish a home, and really a lot of the options on the market are just crap. We purchased a bookshelf after we moved in from the hardware store, and while it was nice looking and in our price range, it's still made of particle board. While this is great from a humidity control perspective, this is terrible for actually holding anything with any sort of real weight, and um, paper is heavy.\n\nI grew up under the tutelage of my father, who is a carpenter. I used to follow him to jobs during summer breaks, where I learned a lot about plumbing, framing, electrical, and removing nails. Growing up, this never really interested me, but the knowledge just never fell on deaf ears. I still absorbed what he taught me, and most importantly I learned his work ethic. So I decided to take the basics he taught me, and expand them. I had a new need being in a house for less-shitty furniture. I started with the few tools I had, and the tools my father lent me, I made a desk. It's not the best quality on the planet, but my father was never super interested in making furniture, so to be fair, I needed to practice...a lot.

Since then, I have watched a bunch of YouTube videos showing tips, techniques, and tools a framing carpenter rarely needs (which means I never saw them before). I found that there is really something quite satisfying about hand tools. Really satisfying actually. So for the past year, I have been slowly building my tool collection and my project portfolio. At this time, I have completed a number of projects.

 - Computer Desk (Red Oak and Plywood)
 - A side table for my mom (Red Oak and Plywood)
 - A wine rack (Birch and Plywood)
 - Bookcase for my nephew (Red Oak)
 - Flag Case for my grandfather's burial flag (Cherry & Maple)
 - Coffee Table for my mom (Red Oak)
 - Gift Box for my wife (Walnut)

Each of these projects I pushed myself further than the previous project. While a Bookcase is a big project, the gift box was my first time I did hand cut dovetailing.

So, you are probably wondering what to expect from this blog. Well, chaos. When you have control over the stack, all you need (on x86 anyway) is to pop ebp to let the chaos begin. Topics will range from woodworking to embedded programming. From philosophical thought to electronics and maybe even leather working. This is going to become my playground to share my knowledge, and hopefully someone can find it useful. If not, maybe Skynet Google can recreate me later on.

pop pop ret

~ sparticvs
