# Roadmap

*by the [Open Knowledge Maps team](http://openknowledgemaps.org/team)*

Version: 3.0 beta (Update 2019)

# Motivation

**The open science revolution has dramatically increased the accessibility of scientific knowledge.** In 2015, 45% of research articles were published open access, with a clear upward trend (Piwowar et al. 2017). In addition, we see a huge increase in open research data, which will mark the next wave of openly accessible outputs.

**Discoverability, however, is falling behind.** With two and a half million papers published every year, and tens of thousands of new research projects launched every week, discovery becomes increasingly difficult. Traditional approaches involving search engines providing long, unstructured lists of scientific outputs are not sufficient any more. We can also see this problem reflected in the numbers: there is a high uncitedness of publications, between 12% and 82% depending on the discipline (Lariviere et al.  2008). It becomes worse when we are looking at research data, with up to 85% of datasets never being cited (Peters et al. 2016). And where it gets really gloomy is the transfer to practice. Even in application-oriented disciplines such as medicine, only a minority of results ever gets transferred to practice, and if so, with a considerable delay (Brownson et al. 2006).

These numbers highlight that accessibility does not equal discoverability and reuse of knowledge. **There is a discoverability crisis that negatively affects the efficiency and effectiveness of science and its transfer to practice** - and it cancels out many of the positive effects of increased accessibility. In many ways, we cannot cash the cheques written by the open science movement, when we do not address this issue.

# Introduction to Open Knowledge Maps

**The goal of Open Knowledge Maps is to close the gap between accessibility and discoverability** of scientific knowledge. We are a charitable non-profit organization dedicated to dramatically increasing the visibility of scientific knowledge for science and society alike. Headquartered in Vienna, Austria, Open Knowledge Maps comprises of an international community including team members, advisors, and partner organizations.

As part of our mission, we operate the largest visual search engine for research in the world. On our website, users can create knowledge maps of research topics in any discipline based on 150 million scientific outputs. These knowledge maps provide an instant overview of a topic by showing the main areas at a glance with relevant papers and concepts attached to each area. This service enables a diverse set of stakeholders to openly explore, discover, and make use of scientific content. Among our users are researchers, students, librarians, educators, science journalists and practitioners across all disciplines and geographic regions. Open Knowledge Maps increases the visibility of content from a wide variety of stakeholders such as libraries, repositories, funding organisations, and publishers.

**Open Knowledge Maps was established in 2016, but it has already become a crucial infrastructure** for researchers, students and practitioners around the world. In the last 3 years, we have had more than half a million visits on the website, and more than 140,000 maps were created. In addition, we had more than 1,500 participants in our workshops worldwide. At the same time, we have been rapidly growing our platform and coverage to a stable and user-friendly service with high availability. We have also developed an agile organisation, a strong community, and professional outreach and training efforts.

In the future, we want to enable our users to collaboratively edit the knowledge maps on our platform, thus **transforming discovery from a closed individual process to an open and collaborative one.** By sharing the results of our discoveries, we can build on top of each other’s knowledge. This process will be aided by our artificial intelligence core and result in a large-scale system of open, interactive and interlinked knowledge maps for every research topic, every field and every discipline. **Users will be able to explore the entirety of scientific knowledge within this system.** In addition, we will provide the information generated in the OKMaps system back to the open discovery infrastructure, both the knowledge models as well as metadata improved or added by our users. Therefore, Open Knowledge Maps will be the only visual interface that combines machine learning with human curation, providing a truly human-centered service as a result. https://vimeo.com/188647919

## Services
**We dramatically increase the visibility of research outputs for science and society alike.** Our approach is to use knowledge maps for discovery. Knowledge maps provide an instant overview of a topic by showing the main areas at a glance with relevant papers and concepts attached to each area. Based on this concept, we operate the largest visual search engine for research in the world. On our website https://openknowledgemaps.org, users can create knowledge maps of research topics in any discipline (see Figure 1 for an example). Users can select between two integrations: BASE, the Bielefeld Academic Search Engine, which provides an index of more than 150 million scientific outputs, and PubMed, the large bibliographic database in the natural sciences with a focus on biomedicine.

Our search service includes a wide variety of output types (21), including datasets and multimedia files, and many resources, especially from university repositories, that are not included in commercial search engines. In addition, we do not restrict language in searches, thus increasing the visibility of non-English content and making the service especially appealing to communities that communicate in a language other than English. We can already see that these efforts have paid off. **Open Knowledge Maps serves both users from the Global South and the Global North:** most of our page views are from users in Indonesia, followed by the US, India, Germany, Austria, the UK, China, Canada, and Australia. In fact, we are seeing some of the strongest growth in the Global South with countries like India (109,000 page views, a fivefold increase in 2018), South Africa (10.500 views and a threefold increase in 2018), or Nigeria (a fourfold increase to 10,000 page views in 2018).

![](images/Overview-of-research-on-digital-education-Open-Knowledge-Maps.png)
Figure 1: Knowledge Map of "digital education", online at https://openknowledgemaps.org/map/c8fe7a11ca29a8b8580e5612fcebc42a

Open Knowledge Maps supports a number of use cases, for which no comprehensive tools existed. These use cases include getting an overview of a topic at a glance and understanding the terminology related to that topic. Open Knowledge Maps also enables users to easily separate relevant from irrelevant papers with respect to their current information need by clustering papers into subtopics. Such cross-discipline overviews become more and more relevant, as the biggest problems of our time (including climate change, migration, globalisation) require an interdisciplinary approach. We also allow for direct access to OA papers within our interface, and offer annotation capabilities for these papers courtesy of Hypothesis. Thus, **we enable users to do a large part of their literature research within the same browser tab.**

Outside of open infrastructures, the need for systems providing visual overviews of scientific fields has also been identified. At the moment **Open Knowledge Maps is the only solution in this space that is free and open, and that is usable without prior knowledge.**

## Software and infrastructure

Open Knowledge Maps is based on the open source knowledge mapping framework Head Start. Head Start is a high-performance and high-availability software stack that is capable of automatically producing knowledge maps from a variety of data, including text, metadata, and references using unsupervised machine learning techniques.

Head Start includes connectors to a number of academic search engines through rOpenSci, including BASE, PubMed, OpenAIRE, PLOS, and DOAJ. We retrieve the metadata of the most relevant documents for a search term from the respective database, and create a knowledge map in four steps:

1. Documents are preprocessed by cleaning metadata like title, abstract, author, and journal by removing punctuation, filtering stopwords, transforming to lower-case and stemming.
2. Similarity of documents is then calculated based on the cosine-similarity of cleaned metadata.
3. The documents are then clustered into groups with Ward’s method of minimum variance, and placed on the map with non-metric multidimensional scaling.
4. Finally, clusters are labeled by taking the top three n-grams of keywords, weighted by Term Frequency - Inverse Document Frequency.

In short: the more words two documents have in common in their metadata, the closer they are placed to each other on the map, and the more likely they are assigned to the same area. The representation of the knowledge map is stored in a database from where it is delivered to the user facing frontend. The frontend consists of a web-based interactive visualization, which follows the Shneiderman’s (1996) principle of  "Overview first, zoom and filter, then details-on-demand". Knowledge maps are complemented by a synchronized list representation of documents and an integrated PDF viewer and annotation tool courtesy of Hypothesis.

Head Start has a client-server architecture with the user-facing search interface and interactive map frontend based on JavaScript and D3.js. The service and API layer is based on Apache/PHP, and the the natural language processing/machine learning backend is written in R. The architecture is complemented by a persistence and versioning system based on SQLite.

**The overall technical design aims to balance two goals: reliability of service and ease of maintenance.**
We choose underlying technologies according to robustness and versatility rather than novelty or specialization, in order to focus development efforts on improving the user experience. Through our choice of open source software, which themselves are developed and maintained by large communities, we avoid vendor lock-in effects and long-term dependencies.

The source code for the whole service is available under the open source MIT License on GitHub. In regular frequency we publish new releases of our software, which are available as open source packages and archived via Zenodo.


## Community Engagement

In the past years, **we have successfully established a wide array of user engagement activities**, including (1) talks and workshops at conferences, research institutions and libraries around the world, as well as via webinars, (2) engagement via our newsletter and on social media, (3) and our Enthusiasts program. These activities are aimed at our diverse stakeholder groups, involving different aspects of the discovery workflow. These aspects include both the reader’s and the author’s point of view (finding and getting found), as well as insights into the functioning of discovery tools and the discovery infrastructure in general.

**Our engagement activities are reusable, making it easy for our stakeholders to run their own trainings.** We provide them with instructions and materials that are also published on our website for [self-guided workshops and lectures](https://openknowledgemaps.org/community#training-materials). Currently, stakeholders can choose between two different formats (“The Scientific Scavenger Hunt” and “Academic SEO”). Both workshops have strong participatory elements. In “The Scientific Scavenger Hunt”, we play a game with the participants that introduces them to Open Knowledge Maps and helps improve their literature search skills along the way. In “Academic SEO”, we discuss the inner workings of search engines and tools that participants use for discovery.

In the [Enthusiasts program](https://openknowledgemaps.org/community) we involve Open Knowledge Maps power users and ambassadors in our engagement activities. Under our guidance, participants with diverse backgrounds from all around the world conduct workshops on open discovery and Open Knowledge Maps in their communities. In doing so, they collect valuable feedback on the future development of our services. These activities give us a unique opportunity to better understand our user groups and their specific needs, especially in regions and communities that we cannot reach, and thus **drive the Open Knowledge Maps development from a community perspective.**

## Openness

Open Knowledge Maps is based on the principles of open science: source code, content and data are shared under an open license. We are a building block of the open discovery infrastructure, with which we extensively collaborate. As a community-driven initiative, we develop our services in a participatory process together with our stakeholders. Our aim is to create an inclusive, sustainable and equitable infrastructure that can be used by anyone, independent of geographic area, age, or stakeholder group. Therefore, we are also conducting workshops to introduce potential users to the tool and help improve their discovery skills along the way. In our community program, the Enthusiasts program, we support power users and ambassadors to conduct workshops themselves and to give feedback from their community’s perspective.


## Sustainability

Our funding model consists of three main pillars:

(1) funded projects  
(2) membership-based funding  
(3) donations

Of these, **funded projects currently provide the largest income.** In this pillar, we create new discovery services using our open source software. **The outcome must always serve the public good.** These projects are either funded by a collaborating institution (e.g. Ludwig Boltzmann Gesellschaft or Austrian Academy of Sciences) or by a 3rd party funding body (e.g. the European Commission or Mozilla)

**Funded projects currently cover only a small percentage of our activities - the largest part is donated in-kind as volunteer efforts.** With only EUR 100,000 in funding so far, this is true even for the core team. In addition, project-based funding is highly volatile. In order to achieve financial, technical, and organisational sustainability **we want to complement funded projects with membership-based funding.** In our membership-based funding model, supporting organisations become members of Open Knowledge Maps and provide an annual contribution. In return, members get a say in the future development of Open Knowledge Maps. Members are invited to join the Board of Supporters, which participates in a yearly vote on what features and sources to implement. This establishes a true community-driven solution for the discovery of scientific knowledge.

Donations are our third pillar, and our smallest yet. In November/December 2018, we launched our first donation campaign. The feedback from the community and the results were encouraging. With the funds raised, we will be able to cover our server costs for 2019.

**We know that increased openness does not automatically lead to a more equitable world.** It needs organizations and services that translate this openness in a way that everyone can benefit from it. Open Knowledge Maps is in a prime position to do so having developed a service and interface that can be understood across geographical borders, age groups and societal stakeholders. At this moment we need more funding to do that in a sustainable way.


## Governance

Open Knowledge Maps’ structure is largely determined by the legal requirements for a “gemeinnütziger Verein” (charitable non-profit) under Austrian law (Vereinsgesetz 2002) and defined in the organization’s bylaws.

Open Knowledge Maps has the following branches (see Figure 2 below):  
(1) The executive branch, which consists of the Executive Board and the team  
(2) The advisory councils, including the Advisory Board and the Board of Supporters  
(3) The monitoring facilities, including the arbitration tribunal and the auditors  
(4) The community, with our users (including the enthusiasts), partners, and networks.

![](images/governance.png)