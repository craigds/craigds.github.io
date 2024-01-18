# Ubuntu 18.04 → 22.04 Upgrade (2023)

### Background

Koordinates has one monolithic backend app (“dandelion”) which contains all the code for backend task processing, format conversion, a set of REST APIs, worker configuration, web views, and most other things that Koordinates does.

Before 2023, Dandelion was built as a Docker image based on Ubuntu 18.04 (Bionic). The software has 102 apt dependencies and 794 python dependencies, about 50 of which are custom-built.

### Upgrading to Jammy (Ubuntu 22.04)

In 2023 I spearheaded the project of upgrading the operating system to Ubuntu 22.04 (Jammy), a project that needed doing but was big enough that no one else wanted to take it on.

This involved upgrading all the custom apt dependencies to newer versions, and testing the changes. For 14 projects, it meant porting significant fork patches onto much newer upstream versions.

This also meant finding and testing alternatives for end-of-life libraries we were using for:

* Writing JPEG2000 images
* Rendering PDF exports of data
* Rendering on-demand and pregenerated map tiles
* Writing to ESRI File Geodatabases

### Outcomes
An end-to-end test suite (that I championed previously) gave me confidence that the changes were acceptable and performed well.

As part of this project I also ensured all dependencies were built for both AMD64 and ARM64 architectures, so that Dandelion could have native images for Apple Silicon, for a much faster development experience. This reduced the time taken to run the test suite on a developer laptop from 20 minutes to 11 minutes.

The project was completed and deployed to production in January 2024 with minimal user disruption, and was considered a huge success.
