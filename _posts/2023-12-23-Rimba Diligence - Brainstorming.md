---
layout: post
title: "Rimba Diligence - Brainstorming"
date: 2023-12-23
tags: [research]
categories: [research]
allowed_emails: ['amenti4k@gmail.com']
---
[https://rimba.cloud/](https://rimba.cloud/)

~~Send follow up mike wang intro to watershed employees~~

~~Schedule mike mona ESG guy~~

Do manufacturers want to take this process in house?

Larger firms are more likely to attain certification to an environmental sustainability standard - 37 percent of companies with over 100 workers had such a certificate, while only 5 percent of firms with fewer than 5 workers had attained such a status.

Rimba is compliance software for manufacturers to streamline certification reporting for their  annual audits. Their focus is on certifications like ISCC that focus on certifying sustainability across the supply chain. ISCC – as an example for this type of certificate – requires:

1. Traceability of sustainable products through the supply chain from the origin of the raw material to the final product.
2. Carbon emissions from the production of raw materials to the distribution of the final product.
3. Social and governance requirements suppliers must meet.

Broadly, compliance is a huge and growing issue in international trade. The requirements are numerous and vague which makes it difficult to implement and build a reporting system. 5 years ago, certifications were “nice to have''. Today, regulatory pressures are making certification mandatory:

- EU = mandatory Renewable Energy Directive (RED) II since 2021
- Japan = mandatory through Japan’s revised Feed-in-Tariff (FIT) since 2021
- USA = mandatory through Renewable Fuel Standard (RFS) since 2005

Their target market is companies who deal with feedstock in their supply chain, thus needing ISCC and RSPO certification. Their initial traction has been with biofuel manufacturers in Southeast Asia, but they are also having conversations with potential customers in the US and EU. Examples:

- [Apical](https://www.google.com/search?q=apical+fuel+trader&rlz=1C5CHFA_enUS892US892&oq=apical+fuel+trader&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRigATIHCAIQIRigATIHCAMQIRigATIHCAQQIRigATIGCAUQIRgVMgcIBhAhGJ8FMgcIBxAhGI8C0gEIMjg1OGoxajeoAgCwAgA&sourceid=chrome&ie=UTF-8) (biofuel trader & largest existing customer) needs ISCC to sell to Italy.
- Valero (petroleum manufacturing, $55b market cap) needs [ISCC Corsia](https://www.iscc-system.org/certification/iscc-certification-schemes/iscc-corsia/) to sell sustainable aviation fuel. CORSIA, the Carbon Offsetting and Reduction Scheme for International Aviation, is an emission mitigation instrument to address the increase in total CO2 emissions from aviation. 104 states (including all EU Member States), representing around 80% of international aviation, participate in CORSIA. Hence, the majority of airlines will be affected by the emission mitigation scheme.

ISCC and RSPO are the two top trusted certifications focused on biofuels and feedstock. RSPO is focused on palm oil and its derivatives, while ISCC has a broader certification scope for various feedstock.

**TAM bottom up calculations**

Knowns:

- [RSPO has certified about 20% of the world’s crude palm oil (CPO)](https://rspo.org/nearly-two-decades-on-europe-continues-to-drive-global-demand-for-rspo-certified-palm-oil/).
- [ISCC has certified a total of 57,000 companies.](https://www.iscc-system.org/certification/certificate-database/all-certificates/)

Assumptions:

- ISCC and RSPO have certified a similar % (so 20%) of their respective markets, as ISCC covers other feedstock (rice straw, wheat straw, rice husk, and corn stover, used cooking oil, tallow, animal fats, etc).

Number of companies globally that should be ISCC-certified: 285,000 = 57,000 * (100/20)

Vanta pricing: For a company with a headcount of 200, the contract price ranges from $16,100 to $23,400. Companies with headcounts of 1,000 and over may expect to pay in the range of $20,700 to $92,200.

Assuming an annual contract value of $25K to $75K, it represents a market opportunity of $7.1 to $21.4 billion for Rimba to address.

**Team**

Distinct advantages to exploiting the Indonesian geography: Ryan was a Sr. auditor for certification frameworks like ISCC, RSPO, and RBO, and has built a network of renewable fuel suppliers and traders in Southeast Asia. Indonesia also represents 59% of the world’s supply of palm oil.

It is currently 2 co-founders who previously worked together in this industry, and have signed their first five customers (all small to mid sized biofuel manufacturers). The founding team is not set. They are dating a third technical cofounder responsible for building the software: [Akshay Sharma](https://www.linkedin.com/in/akshay326/) (who’s already building for them), previously an ML engineer at [Klarity](https://www.klarity.ai/), a Series A AI documentation platform. They applied to Y Combinator this Monday, and I believe there may be an opportunity for us to invest before YC if they get accepted.

**What does their product do?**

Manufacturers have to go through thousands of docs (PDFs) for each transaction every week. Docs can be (1) certificates of weight (weights of raw materials they receive), (2) contracts with their suppliers, (3) delivery notes, (4) sustainability declarations from certified suppliers, (5) purchase orders, (5) certificate of analysis, (6) invoices – to name a few.

These manufacturers already track all of these for their manufacturing reports. The docs are in paper format, so they can scan them, and info is used for general ledger. If companies are not certified, they only care about the weights of each shipment, but if they are certified, they need to start tracking a lot more information such as:

- Traceability of raw materials
    - Where did they come from? Factory’s location? Overlap with deforestation areas? Labor practices?
- Track real gas emissions
    - Calculate distance, type of trucks, how long of a journey, how much weight on trucks do they carry, depending on type of truck, type of fuel they use

Docs today are manually read, scanned, and added to multiple spreadsheets that track the aforementioned stuff. With all this data, companies create a mass balance spreadsheet that tracks all their inputs, and whether they are certified or not. This dictates how much % of their sales can go into markets that require certifications.

For example, if only 30% of their input materials are certified (in blended values) because they only manage to get 30% of their supply chain as certified. Then, only 30% of their sales can go into those markets that require certification (e.g., Europe and Japan). They can cross this limit, but it’s a loan to future certified materials, so in aggregate, they can’t cross this limit. If they do, their certification gets suspended.

The mass balance helps track this, how much certified material that comes in can’t be more than the certified biofuel coming out.

Things Rimba is building to help streamline this:

1. Data Extraction and Reporting Automation:
    - Process unstructured data e.g. scanned PDF, purchase order, weight certificate, shipping documents.
    - Automates data extraction for compliance reporting; Intelligent Document Processing (IDP)
2. Material Tracking and Risk Management:
    - Trace material flows and segregate certified from non-certified materials.
    - Prevents double accounting and maintains integrity of supply chains.
3. Streamline Multiple Sustainability Certification Audit:
    - more transparency + less manual data entry + less manual calculation on excel
    - Automates cross-certification, reducing effort and duplication.

**Competitive landscape**

There are a number of successful companies that help demonstrate that there is a market here including Watershed, Greenly and Sustain Life.

Watershed is a software platform to help companies to zero carbon. Their mission is to build the tools that enable a business to:

- Measure their carbon emissions to know where they’re at today.
- Plan out different ways to reduce the carbon emissions.
- Execute on that plan by buying clean power, by engaging their suppliers, by redesigning their product.
- Actually remove carbon from the atmosphere for whatever emissions remain (i.e., via their marketplace).
- Report on that progress externally so that investors, regulators, employees, customers, can hold them accountable (i.e., automate compliance for CSRD reporting) .

[Podcast with CEO of Watershed (Scott Amyx);](https://www.youtube.com/watch?v=hnryfG0NvQA&ab_channel=ScottAmyx)

Good news: There is starting to be some convergence and people are beginning to be in the space page about the rules of the road of what you count and how when tracking GHG. Bad news: The whole point of measurement is to enable the right action, and the status quo in carbon accounting maybe enables you to publish a really detailed PDF that has all the right acronyms on it, but does not enable companies to make the right choices. As an example, for most companies, most of their carbon emissions come from Scope3. The standard approach to calculating those emissions is to look at the dollars spent on a specific category and multiply it by what the [EPA](https://sor.epa.gov/sor_internet/registry/termreg/searchandretrieve/glossariesandkeywordlists/search.do?details=&vocabName=Glossary%20Climate%20Change%20Terms&filterTerm=carbon%20footprint&checkedAcronym=false&checkedTerm=false&hasDefinitions=false&filterTerm=carbon%20footprint&filterMatchCriteria=Contains#:~:text=Definition%3A%20The%20total%20amount%20of,or%20riding%20in%20a%20car.) said in 2010 is the carbon per dollar in that category. What Watershed wants companies to actually do is redesign their products, change materials and change suppliers, and the status quo doesn’t enable that (i.e., just helps track but no actions). So Watershed wants to get the data to upgrade the quality of carbon accounting so it enables the right actions. So anyone can know the carbon footprint of a specific company, of a specific supplier, of a specific product, and you can make choices based on that.

In terms of regulations, the trend is for what’s currently being enacted in the UK and Europe to become standard practice around the world. Large companies, both public and private, are expected to report on carbon accounting at least once a year with the same rigor with which they report their financial data.

This category of carbon accounting software has gained crazy momentum in the last few years. Notably, both Watershed and Greenly were founded in 2019 and have announced growth rounds in the last 60 days:

- [Watershed raised a $100M Series C led by Greenoaks, Kleiner Perkins, and Sequoia.](https://watershed.com/blog/series-c) [Taylor Francis](https://www.linkedin.com/in/taylor-francis-4ba49640/) is cofounder/CEO.
- [Greenly raised a $52M Series B led by Fidelity.](https://techcrunch.com/2024/03/20/greenly-series-b/?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAEX2agMhPdRlrUep16_S9-9_kjbOuQeN3kD22MoCsyLyUpE-nB4xSErT6ATXY_tY-7GuEh6OEIG-YiTnGH5jbzU5WuOkEKiOow8NWMm_UGod1Ffsk1rk3G9mL3dyfEZoNsN5VxTOf45eLfIBTdr2Xk5nqsL_oftay7aV4Nizls5I) [Alexis Normand](https://www.linkedin.com/in/alexisnormand/) is cofounder/CEO.

The POV of Watershed is that if companies have pressure to take responsibility for their entire carbon supply chain, they can bring capital, resources, and expertise to decarbonize some of these lesser developed countries, because they are part of that company’s carbon supply chain. For example, when you look at a company like Apple, most of its carbon is coming from China and Taiwan from electronic suppliers (even though it appears on the US balance sheet).

This to me doesn’t connect with stats like [RSPO having certified about 20% of the world’s crude palm oil (CPO)](https://rspo.org/nearly-two-decades-on-europe-continues-to-drive-global-demand-for-rspo-certified-palm-oil/). These producers of feedstocks like palm oil are based in the less developed countries that Scott (CEO) refers to in his podcast. 20% of crude palm oil having been certified already looks like incredible progress to me. Could it be that developed countries have this misconception that the biggest GHG emissions exist in less developed countries, when that might not be the case?

—

CSRD (Corporate Sustainability Reporting Directive) is another type of certification that applies to large EU companies and public and private non-EU companies with EU business. It replaces the EU’s legacy ESG reporting program—the NFRD—and raises the bar for breadth and robustness in sustainability reporting, covering categories beyond just carbon, including pollution, water, waste, and biodiversity.

They target companies in the EU and the US who are mostly concerned about carbon emissions (doesn’t matter if they are manufacturing, banks, or software companies). They are concerned about the mandatory disclosure they have to make about carbon emissions (i.e., CSRD). This is why companies like Greenly and Watershed have taken off.

Watershed also lets companies easily repurpose their CSRD data to fulfill other reporting frameworks, like [CDP](https://www.sustain.life/blog/what-is-cdp) or [ISSB](https://www.ifrs.org/groups/international-sustainability-standards-board/). As an aside, only people who care about these reports are investors focused on ESG.

Watershed’s vision is to become the one-stop shop for corporate sustainability teams. They offer everything these teams need. It’s different to an approach like Rimba’s that’s going deeper into the end-to-end compliance requirements for a specific vertical (manufacturers) versus targeting a specific team (corporate sustainability) across many verticals. This shows in their product suite:

- [Corporate](https://watershed.com/solutions/csrd): reporting; e.g., CSRD.
- [Financial services:](https://watershed.com/solutions/finance) data to analyze portfolio’s emissions (ESG stuff)
- [Supply chain visibility:](https://watershed.com/solutions/supply-chain) gives corporations visibility over which suppliers are generating most carbon emissions (scope3 emissions i.e., GSG coming from suppliers indirectly), so they can grill them down and try cutting down their own carbon footprint.
- [Consumer goods](https://watershed.com/solutions/consumer-goods): help track carbon emissions for consumer good brands that care about consumer sentiment (i.e., make more money if they can show they are sustainable).
- [Carbon Offset Marketplace](https://watershed.com/platform/marketplace): companies can purchase carbon offsets commensurate with their unavoidable emissions. The market for carbon offsets is [expected](https://www.morganstanley.com/ideas/carbon-offset-market-growth) to grow from $2 billion in 2020 to around $250 billion by 2050.

Watershed claims to streamline emission measurement using customer data to estimate a company’s Scope 1 (owned assets emissions), Scope 2 (utility purchases emissions), and Scope 3 emissions (3rd party emissions). For example, Watershed will use an Excel spreadsheet or a purchase order PDF to estimate emissions. Watershed also works with a company’s suppliers to accurately assess a company’s Scope 3 emissions. In November 2022, Watershed [announced](https://www.axios.com/pro/climate-deals/2022/11/02/carbon-accounting-watershed-scope-3-measurement-software) a supply-chain emissions tracking module to better address Scope 3 emissions with a “combination of public and private data from suppliers to estimate the emissions footprint of the larger supply chain.”

A dated view of Watershed’s product that is no longer on its website shows an expense item-level drilldown to illustrate the exact emissions coming from particular expense areas (e.g. advertising, software, etc.).

[https://lh7-us.googleusercontent.com/__q4vhOyn42WZhJGOI55NWPqWmNCFLvvxjcCuvfc5BVYPLMWuxG7DDRc1Fqrvx8rVYXQuwdgiEvVM5XSRD9zsIgTIPFPGU4Vyu6dabamFkbTR7O7f3fAx6VDa1AWmb9McNMmLfSCr_vvPsF7KUpxzT8](https://lh7-us.googleusercontent.com/__q4vhOyn42WZhJGOI55NWPqWmNCFLvvxjcCuvfc5BVYPLMWuxG7DDRc1Fqrvx8rVYXQuwdgiEvVM5XSRD9zsIgTIPFPGU4Vyu6dabamFkbTR7O7f3fAx6VDa1AWmb9McNMmLfSCr_vvPsF7KUpxzT8)

**Watershed’s takeaway:** The majority of Watershed’s customers are technology companies. If climate reporting becomes mandatory, the market size will increase dramatically as corporations scramble to become compliant. You could potentially compare Watershed to ERP platforms like Oracle or SAP, or vertically-focused ERPs, like Veeva or Toast. If Watershed is successful the company would be considered a core system of record for managing carbon accounting. These types of ERPs can trade anywhere from 2-11x LTM revenue. [Though in this podcast](https://www.youtube.com/watch?v=hnryfG0NvQA&ab_channel=ScottAmyx), Watershed CEO does describe their focus beyond carbon accounting, “we’re not in this to play the carbon accounting game, we’re in this to be a platform that enables decarbonization and companies at the front of climate change to make different choices”.

**Why is Rimba different?**

Rimba is focused on a different niche. They noticed that aside from carbon emissions, regulators are also starting to ask for disclosure of where the raw materials are coming from, social and governance aspects of these suppliers, and carbon emissions from the transportation that is involved in the supply chain until the consumer (upstream data). These data are captured in other certifications like ISCC.

Watershed and Greenly haven’t achieved any meaningful penetration more upstream in the supply chain (producers, traders, farmers). Most of their clients are startups, financial institutions, and public companies. When Rimba talks to potential customers like Valero (petroleum manufacturing, $55b market cap), [IAG](https://en.wikipedia.org/wiki/International_Airlines_Group) (International Airlines Group), or other manufacturers, they never mention Watershed as someone that is helping them.

Where Rimba comes in is that all these companies fail to understand how to navigate legacy industries like agriculture, manufacturing, and mining, which are all growing massively in Asia and LatAm supplying these products to the EU and the US. Most companies outside of the US and the EU probably never heard of CSRD certification or carbon emissions accounting. All they care about is how they can export products overseas, and for that they need to be certified with other kinds of certificates like ISCC, RSPO, and RBO.

Well, this still begs the questions.

1. Is it the logical next step for companies like Watershed to start adding other certificates to their platform after they win over CSRD compliance? If yes, which certificates are they likely to go after next? If the market opportunity for certificates like ISCC is obviously large, what are the reasons for why they wouldn’t choose to focus on that? Are there key differences between these markets? Is it a wholly separate problem/focus?
2. Why would Watershed’s lack of experience in legacy markets affect their chances of winning? What if the only important segment that needs to be won are large corporations serving the end consumers? One could say that if you win over this segment, you can help them force similar measures across all their suppliers upstream.

[Per their CSRD website](https://watershed.com/platform/climate-disclosures/csrd), Watershed’s likely to focus on the certifications next:

[https://lh7-us.googleusercontent.com/YmWC33vb3B3-hLDtXWwMgbz6ODa7avoJ71LHPDVg_dtV03Z18dVXjzNNK-eD9iHDj5D5fYiSYyx3MajqxPSk15tS43staK2NyKsgrC3x2NhvfplB16LqNFSjdggxE8Z49YjQB_EbPrP-1wGimMZsRIM](https://lh7-us.googleusercontent.com/YmWC33vb3B3-hLDtXWwMgbz6ODa7avoJ71LHPDVg_dtV03Z18dVXjzNNK-eD9iHDj5D5fYiSYyx3MajqxPSk15tS43staK2NyKsgrC3x2NhvfplB16LqNFSjdggxE8Z49YjQB_EbPrP-1wGimMZsRIM)

**Interesting potential customer use case:**

Upstream data is unstructured (many suppliers are not sophisticated even in the US). Tim talked to the sustainability officer of a company called Highland Pellets and they sell biomass to the EU from the US. Highland sources wood chips and shingles from lumber mills and privately owned forests in the US. Many lumber mills and forest owners do not want to disclose anything. It is a constant push and pull, but Highland must be certified by certification: Sustainable Biomass Program / ISCC, and they need to track every square foot of where the trees come from. The requirements a few years ago were not very stringent, but it has gotten harder.

- If it is a certified supplier they would need less verification of supplier data. They would focus on delivery notes, sustainability certificate, and sustainability declaration.
- If the supplier is not yet certified, the company needs to verify the data themselves. (Like doing internal audit of the supplier)

Highland’s an interesting example as it shows how manufacturers struggle to get the necessary data from their suppliers. In Highland’s case the requirement is to trace where each tree comes from in which part of the forest. So Rimba has been discussing a solution by building a phone app for suppliers to take pictures of the trees before they are cut down, and Rimba will connect the app to use the photo and google maps to pinpoint the location. Right now Highland doesn’t have a solution for this yet.

CDP/SDDB/CSRD’s main audience is investors, these frameworks are meant to help public market investors determine which companies are better from a carbon accounting perspective.

ISCC on the other hand is more focused on operational data, and has a direct impact on a company’s ability to operate and do business. In order, it focuses on:

1. Traceability of raw materials
2. Deforestation, and then,
3. Carbon emissions

**CarbonChain is a competitor that’s more similar to Rimba:** Founded in [2019](https://www.linkedin.com/in/adamhearne/), [CarbonChain](https://www.carbonchain.com/) is a carbon accounting platform specifically targeted at manufacturers, commodity traders, and their banks. Companies tied to physical supply chains have a more complex emissions footprint, and can also access unique [sustainable financing](https://www.eib.org/en/stories/what-is-sustainable-finance) if they can demonstrate emissions measurement and reduction. [Customers](https://www.carbonchain.com/case-studies) include Lloyd’s, Concord, and Gunvor.

[CarbonChain Comply](https://www.prnewswire.com/news-releases/launch-of-carbonchain-comply-major-update-in-carbon-reporting-saas-for-metals-and-energy-302112380.html) offers a comprehensive solution for businesses within metals and energy supply chains who are grappling with monumental regulatory shifts on carbon emissions and rising stakeholder demand for transparent and accurate disclosure. The new one-stop shop for carbon reporting empowers sustainability leaders, compliance managers and procurement directors to streamline and satisfy every key disclosure request, no matter the format or framework. [It raised a $10M Series A led by Union Square Ventures on April 10, 2024.](https://fintech.global/2023/04/26/carbon-accounting-platform-carbonchain-scores-10m-series-a/)

They are [starting to talk about this other EU requirement called CBAM](https://www.carbonchain.com/cbam) targeted at importers of aluminum, steel, iron, fertilizers, electrical energy, hydrogen or cement into the EU.

Interesting case study: [https://www.carbonchain.com/case-study/concord](https://www.carbonchain.com/case-study/concord)

—

**Detailed description of ISCC requirements [(pdf p19 to p24)](https://www.iscc-system.org/wp-content/uploads/2024/01/ISCC_EU_201_System_Basics_4.1_January2024.pdf):**

The ISCC certification system covers three categories of requirements:

> Sustainability requirements for agricultural and forest biomass, waste and residues, feedstocks for the production of renewable fuels of nonbiological origin and recycled carbon fuels and low iLUC risk feedstocks

> Requirements for traceability and the chain of custody

> Requirements for greenhouse gas emission savings and the calculation methodology

**Sustainability requirements**

Farms and plantations that produce sustainable agricultural biomass must comply with the sustainability requirements as stated in ISCC EU System Documents 202-1 “Agricultural Biomass ISCC Principle 1” and 202-2 “Agricultural Biomass ISCC Principles 2-6” ”. The six ISCC Principles cover the following topics:

Principle 1: Protection of land with high biodiversity value or high carbon stock

Principle 2: Environmentally responsible production to protect soil, water and air

Principle 3: Safe working conditions

Principle 4: Compliance with human and labour rights and responsible community relations

Principle 5: Compliance with land rights, laws and international treaties

Principle 6: Good management practices and continuous improvement

If biofuels, bioliquids and biomass fuels are produced from forest biomass the risk of using forest biomass from unsustainable production has to be minimised, and the biomass has to met certain land-use, land-use change and forestry (LULUCF) criteria. The use of forest biomass from sustainable production shall be ensured through monitoring and enforcement systems on national level or through requirements for the management system of the harvesting operation (Art. 29 (6) of the RED II). The six ISCC Principles cover the following topics:

Principle 1: Sustainability requirements for the production of forest biomass

Principle 2: Environmentally responsible production to protect soil, water and air

Principle 3: Safe working conditions

Principle 4: Compliance with human and labor rights and responsible community relations

Principle 5: Compliance with land rights, laws and international treaties

Principle 6: Good management practices and continuous improvement

**Traceability and Chain of Custody**

Traceability and chain of custody ensure that two basic requirements are fulfilled:

1. The possibility of tracing sustainable products back and forth through the supply chain from the origin of the raw material to the final product
2. The possibility of assigning product specific information to consignments (batches) of sustainable materials and products

Traceability describes the ability to identiy and trace the origin, processing history and distribution of materials and products through supply chains. Chain of custody describes the monitoring of input and output of sustainable materials and related information and documentation requirements. The following properties of sustainable material (so-called sustainability characteristcs) are the minimum information required under ISCC:

> Type of raw material (e.g. rapeseed, sunflower, used cooking oil, etc.)

> Country of origin of the raw material

> Certification scope of raw material (e.g. the raw material is either certified according to the sustainability criteria of Art. 29 (2) – (7) of the RED II, or the raw material meets the RED II definition of waste or residue)

> Information on GHG emissions (mandatory under ISCC EU, voluntary under ISCC PLUS)

> Claim “ISCC compliant” or “EU RED compliant” (if applicable)

**Greenhouse Gas Emissions**

ISCC provides a methodology for calculating greenhouse gas (GHG) emissions for all elements of the supply chain and for determining greenhouse gas emissions savings. This can be applied to supply chains in all markets. Specific requirements apply for biofuels, bioliquids, biomass fuels, recycled carbon fuels and renewable liquid and gaseous transport fuels of nonbiological origin that are brought into the markets of the European Union. The economic operators bringing sustainable fuels into the market (i.e. the fuel supplier) must prove that the fuels where produced sustainably and that greenhouse gas emissions savings are sufficient according to the RED II.

The requirements for GHG emissions apply to all relevant supply chain elements from the production of raw materials to the distribution of the final product, including cultivation, collection and conversion processes, as well as the transport and distribution of intermediate and final products. Three different options are available to provide information on GHG emissions:

1. Use of total default values: Default values are raw material and process specific and are provided in the RED II for different types of biofuels, bioliquids and biomass fuels.
2. Use of disaggregated default values. So-called disaggregated default values are available in the RED II for the cultivation/ production of biomass, processing, and transport and distribution. Disaggregated default values allow the use of a combination of default and actual values.
3. To determine GHG emissions from cultivation the use of typical values that represent the average value in a specific area is also possible. Those typical values are often referred to as NUTS210 values. Those NUTS 2 or typical values have to be reported to the European Commission by Member States or third countries and can be used if the Commission recognizes them to be accurate . Use of actual values: Individually calculated values must be calculated based on the methodology according to the RED II.

All requirements to apply, calculate and verify the greenhouse gas emissions and emission savings are specified in ISCC EU System Document 205 “Greenhouse Gas Emissions”.

**Participants in the Certification System**

All economic operators that handle sustainable material (e.g. produce or generate, collect, process, store or trade) have to be covered by an ISCC certification. In the ISCC system the term ‘economic operator’ refers to a specific site (spatial entity) of a company where sustainable material is handled. A company may have more than one operating sites. If this is the case, every single operating site handling sustainable material has to be covered by its own certification.

For biofuels, bioliquids and biomass fuels produced from agricultural or forest biomass (including agricultural, aquaculture, fisheries and forestry residues) the supply chain starts at the farm/plantation or forest management unit (see Figure 2). The first gathering point is the first element that must be individually certified. Farms/plantations and forest management units can be covered under the certificate of the first gathering point but may also receive an individual or group certification.

[https://lh7-us.googleusercontent.com/fTf_0Q63AkpeI3S4MJ2ij7C0oAFq6PKEeo0XqJvHh5oWqN6Mm6OBhBzlRF7_o7j3jnbAMbH1FjIzlYyPt51H00wMHDAenzKA92kHpHP5ceRjDSpUiPC6RW2r1HQXZFjx7VQK2t1OrIekqkg6FTfB0Uc](https://lh7-us.googleusercontent.com/fTf_0Q63AkpeI3S4MJ2ij7C0oAFq6PKEeo0XqJvHh5oWqN6Mm6OBhBzlRF7_o7j3jnbAMbH1FjIzlYyPt51H00wMHDAenzKA92kHpHP5ceRjDSpUiPC6RW2r1HQXZFjx7VQK2t1OrIekqkg6FTfB0Uc)

Biofuels, bioliquids and biomass fuels can also be produced from bio-based waste and processing residues. Recycled carbon fuels are produced from non-renewable liquid or solid waste. For renewable liquid and gaseous transport fuels of non-biological origin (RFNBO) it is the process energy that provides the energy input for the final fuel (e.g. electricity generated from wind, solar, aerothermal, geothermal or water). This process energy has to be derived from renewable sources other than biomass.

In these cases, the supply chain starts at the point of origin (see Figure 3). The collecting point is the first element that must be individually certified. Points of origin can be covered under the certificate of the collecting point but may also receive an individual or group certification.

[https://lh7-us.googleusercontent.com/YYTV08v_9ykfbIAd5mtKnphUGrCk5TpXSG13YGeap7Or2SCxWM3Fp8AIKhk6Vbd3HE-YoY5Ux-gTAOb7THUG6iiYb7Ybm5OTeiBGE24kC75ySaz8YHm9c5_3tgZz0tv5pLBRNFyQFicjdXVviIwOBXQ](https://lh7-us.googleusercontent.com/YYTV08v_9ykfbIAd5mtKnphUGrCk5TpXSG13YGeap7Or2SCxWM3Fp8AIKhk6Vbd3HE-YoY5Ux-gTAOb7THUG6iiYb7Ybm5OTeiBGE24kC75ySaz8YHm9c5_3tgZz0tv5pLBRNFyQFicjdXVviIwOBXQ)

For all elements of the supply chain after the first gathering point or collecting point the certification requirements are the same regardless of the kind of raw material that enters the supply chain.

A valid ISCC certification is a prerequisite for any element of the supply chain that will handle sustainable material. The only exception to do this is for first gathering points and collecting points that may receive sustainable material up to three months prior to the start of the certificate’s validity. A detailed description of all relevant supply chain elements, the respective certification requirements and the requirements for handling sustainable material are stated in ISCC EU System Document 203 “Traceability and Chain of Custody”.

More random notes all over the place below

Their current workflow: Drive folder with all the pdfs per type, spreadsheet per type, mass balance report

Rimba is compliance software for manufacturers to streamline certification reporting for annual audits. They’re developing an AI enabled platform that uses LLMs and OCR to automatically extract key information from unstructured data sources (e.g. PDFs, scanned delivery notes, etc.). This addresses the challenge of manually handling thousands of such documents weekly, reducing human error leading to the risk of certification suspension.

The platform ensures accurate tracing of raw material origins and GHG (greenhouse gas emissions) calculation from transportations involved, which is crucial for meeting certification requirements. Based on customer feedback, this saves their customers from having to hire consultants, more employees to maintain certification, and reduce risk of suspension.

Their long-term goal is to expand into certifications in other industries such as textiles, plastics, food. They’ll first expand their product capabilities to integrate with various ERP softwares and – applying AI to cut down on manual review and calculations currently being done by consultants.

By accessing all data that currently lives on PDFs, they’ll focus on the following key features:

- Dashboard for visibility
- Trace material flows and segregate certified from non-certified materials.
- Prevents double accounting and maintains integrity of supply chains.
- Algorithm to match volume and source of purchased materials and sold materials
- Automates multiple certifications, reducing effort and duplication.

Rimba is compliance software for manufacturers. They streamline and automate how manufacturers follow mandatory sustainability certifications like ISCC, RSPO, RSB, starting with the renewable fuel market.

The market opportunity has grown and became more relevant in the last few years. The reason is that these sustainability certifications have become mandatory and require very stringent guidelines. Companies that don’t become certified can’t do business in the US, Europe, and Japan. The process for becoming certified and keeping the certification via annual audits lives in spreadsheets, manual work, and only happens thanks to expensive consultants. Needless to say, this is an expensive, time consuming, manual process. New technologies like OCR and LLMs allow for useful automations that can truly make a dent here, so there was never better timing to build a software company that helps automate and manage compliance for this market.

It is currently 2 co-founders who previously worked together in this industry, and have signed their first five customers (all small to mid sized biofuel manufacturers). The founding team is not set. They are still looking for a third technical cofounder responsible for building the software. They are actively dating CTOs and seem advanced with this one engineer called [Akshay Sharma](https://www.linkedin.com/in/akshay326/) (who’s already building for them), previously an ML engineer at Klarity, an AI documentation platform. They are applying to Y Combinator by Monday, and I believe there may be an opportunity to invest before YC if they get accepted.

**What does their product do?**

Manufacturers have to go through thousands of docs (PDFs) every week. Docs are either (1) certificates of weight (weights of raw materials they receive), (2) contracts with their suppliers, and (3) delivery notes.

These manufacturers already track all of these for their manufacturing reports. The docs are in paper format, so they can scan them, and info is used for general ledger. If companies are not certified, they only care about the weights of each shipment, but if they are certified, they need to start tracking a lot more information such as:

- Traceability of raw materials
    - Where did they come from? Factory’s location? Overlap with deforestation areas? Labor practices?
- Track real gas emissions
    - Calculate distance, type of trucks, how long of a journey, how much weight on trucks do they carry, depending on type of truck, type of fuel they use

Docs today are manually read, scanned, and added to multiple spreadsheets that track the aforementioned stuff. With all this data, companies create a mass balance spreadsheet that tracks all their inputs, and whether they are certified or not. This dictates how much % of their sales can go into markets that require certifications.

For example, if only 30% of their input materials are certified (in blended values) because they only manage to get 30% of their supply chain as certified. Then, only 30% of their sales can go into those markets that require certification (e.g., Europe and Japan). They can cross this limit, but it’s a loan to future certified materials, so in aggregate, they can’t cross this limit. If they do, their certification gets suspended.

The mass balance helps track this, how much certified material that comes in can’t be more than the certified biofuel coming out.

Things Rimba is building to help streamline this:

1. Data Extraction and Reporting Automation:
    - Process unstructured data e.g. scanned PDF, purchase order, weight certificate, shipping documents.
    - Automates data extraction for compliance reporting; Intelligent Document Processing (IDP)
2. Material Tracking and Risk Management:
    - Trace material flows and segregate certified from non-certified materials.
    - Prevents double accounting and maintains integrity of supply chains.
3. Streamline Multiple Sustainability Certification Audit:
    - more transparency + less manual data entry + less manual calculation on excel
    - Automates cross-certification, reducing effort and duplication.

**Some context on how the market works:**

Independent auditors run third party verification services that audit whether manufacturers are following certification guidelines.

Consultants help train and prepare manufacturers for these audits. In practice, manufacturers only learn 20-30% of what consultants tell them in Year 1, so they continue paying for their services annually to make sure they don’t get suspended in the annual audits.

Manufacturers also hire an in-house team (typically under the legal department) that make sure all the required data is gathered.

ISCC and RSPO are focused on biofuels and feedstock. 50K companies have been certified, a 25% of those that need it, so the total number of companies here is 180-200K.

Knowns:

- Some certifications are bullshit (self reported/voluntary guidelines), but others are real (third party verification via regular audits) and have real economic consequences (not allowed to sell in various markets).
- Acquiring and maintaining these real certifications is not an easy task. It’s manual, time consuming, and expensive. Currently, consultancy services like Control Union are the biggest players in helping manufacturers navigate the certification requirements (5000 employees, $600M annual revenues).

Unknowns:

- Unclear how much money manufacturers spend on consultancy services + in house employees to navigate certification processes.
- TIC companies are involved with this, but unclear how relevant is certification for the largest companies in this space.

Testing, Inspection, and Certification (TIC) market.

- Certification is part of testing, inspection and certification and the provision by an independent body of written assurance (a certificate) that the product, service or system in question meets specific requirements.It is the formal attestation or confirmation of certain characteristics of an object, person, or organization. This confirmation is often, but not always, provided by some form of external review, education, assessment, or audit.

[The Global Testing, Inspection, And Certification (TIC) Market is projected to grow](https://www.prnewswire.com/news-releases/testing-inspection-and-certification-tic-market-size-worth-usd-389-79-billion-globally-by-2030-at-5-5-cagr-verified-market-research-301917632.html) at a CAGR of 5.5% from 2022 to 2030. the market was valued at USD 233.69 Billion in 2021 and is expected to reach USD 389.79 Billion by 2030.

- SGS S.A. ($7B annual revenues, public)
- Bureau Veritas S.A. ($6B annual revenues, public)
- Intertek Group Plc. ($3.5B annual revenues, public)

Testing, Inspection, And Certification (TIC) Market industry is experiencing unprecedented growth, driven by regulatory compliance, outsourcing trends, environmental awareness, and technological advancements

- Rising Regulatory Compliance: Governments across the world are enforcing stringent regulations to ensure the safety and quality of consumer products, compelling manufacturers to engage independent TIC services.
- Outsourcing Trend: Manufacturers are increasingly outsourcing TIC services to specialized providers, aiming to meet compliance standards while streamlining operations and enhancing profitability.
- Environmental Awareness: Growing environmental consciousness has led to a surge in environmental testing and certification, driven by both governmental mandates and consumer demand.
- Technological Advancements: Continued innovation in testing, inspection, and certification technologies will enhance the industry's efficiency and capacity to address emerging challenges.

Another relevant market: [revenue attributed to environmental certificates is expected](https://guidehouseinsights.com/news-and-views/global-revenue-for-environmental-certificate-market-estimated-to-grow-to-over-$102-billion-by-2032) to increase from $37.8 billion in 2023 to $102.3 billion in 2032, at a compound annual growth rate (CAGR) of 11.7%.

Bottom up TAM analysis on SOC2 compliance annual spend:

[https://start.askwonder.com/insights/market-size-compliance-audit-software-uoqrw344c](https://start.askwonder.com/insights/market-size-compliance-audit-software-uoqrw344c)

*Therefore, we can assume that the total estimated SOC 2 spend in the U.S. every year would be (75%*9,000)*60,000 =405,000,000.*

- *Total number of SaaS companies: 9000 [USA]*
- *Avg [annual audit spend](https://trustnetinc.com/pricing/soc-ssae18-report-cost/): $20k to $100K*
- *75% of SaaS companies get SOC certification*

Similar numbers for ISCC alone:

- [Total number of ISCC certified manufacturers: 50,000](https://www.iscc-system.org/certification/certificate-database/all-certificates/) [Global]
- Avg annual audit spend: unknown; Tim’s mining company $20K.

**Customers**

Focused on the Indonesian market for palm oil; [Indonesia produces 44.5 million metric tons of palm oil, or roughly 59 percent of the world’s supply.](https://harris.uchicago.edu/news-events/news/short-term-profits-versus-long-term-sustainability-mapping-palm-oil-production#:~:text=Every%20year%2C%20between%205%2C000%20to,now%20includes%204.2%20million%20farmers) It’s in so many everyday products around the world—shampoo, deodorant, cereal, dishwashing detergent—that much of the world could scarcely function without it. Yet the massive industry is still lacking in many basic regulations. The high-yield nature of palm oil, which yields almost ten times as much product per hectare as soybean oil, makes it a lucrative prospect for corporations. And its expected market growth could nearly double to £87 billion (over $105 billion in US dollars) by 2026—what Bintang’s team calls “an agricultural gold rush.”

Largest customer: [https://www.apicalgroup.com/sustainability/progress-dashboard/](https://www.apicalgroup.com/sustainability/progress-dashboard/)

- [https://rspo.org/members/2-0235-11-000-00/](https://rspo.org/members/2-0235-11-000-00/)

Klarity

A disproportionate percentage of highly skilled, highly paid workers waste time reading similar documents over and over again.

Klarity’s platform was built over the course of four years and leverages cutting-edge Natural Language Processing and Computer Vision to understand documents as well — or better — than human reviewers. The result: The most accurate document intelligence platform available today.

Market size

Environmental certificates is a growing market. Seemingly because the carbon and energy attribute certificates can be traded in carbon markets, and a lot of money can be made that way. It’s still unclear to me how third-party verified certificates like ISCC for biofuels or Energy Star for energy efficiencies are connected to this. My guess is that if I am a biofuel producer, and now I get 40% of my production to be certified materials, perhaps I can create credentials from that that I can later sell in the markets?

Unclear the market size breakdown. How much of it is related to financial markets stuff like carbon bonds, certificates that are sold or bought by other companies to offset carbon footprint versus the actual cost of managing certification compliance. I assume that number is much smaller.

Different kinds of certifications:

- Self reported or voluntary guidelines
- Third party verification and mandatory

like ISCC, RSPO, and RSB in the context of BioFuels

His plan:

- Technical cofounder
- 10 companies under their belt

They have 5. Get another 5.

RIMBA is a compliance automation platform for manufacturing companies globally to meet industry-standard sustainability certifications.

I am looking to understand what is everything that needs to be tracked. Why not just narrow down their focus to ISCC to start? Each certification seems to be a pretty unique process (different to what he somewhat suggested in the first call that they are all kind of the same). I want to understand in detail how can software truly move the needle for ISCC (specifically one example).

1. Extracting data from invoices.
2. Who does traceability? Are companies good at this with or without software? Startups seemed to tried doing traceability but not from compliance angle. Thoughts?
3. Who tracks traceability, and who tracks greenhouse gass emission savings? How do companies get to these numbers? How do they create their methodology?

Isn’t $200k a bit too low for this to be a big problem?

ISCC requirements:

[https://lh7-us.googleusercontent.com/ko9nf--aMmXk3GUZ_CrAKkkvr2ska_I6XY3PYzl2n3nQ3GrdmH_9ovANaN22Hu5QYTBn3iI5vKrJgKbgs8uDjmtnMxcUV7ia0DDpoSm0thMEGM_ycddMm4ySQxCLohYyKKpu3I0FVLNR6E4lGlNFQZ8](https://lh7-us.googleusercontent.com/ko9nf--aMmXk3GUZ_CrAKkkvr2ska_I6XY3PYzl2n3nQ3GrdmH_9ovANaN22Hu5QYTBn3iI5vKrJgKbgs8uDjmtnMxcUV7ia0DDpoSm0thMEGM_ycddMm4ySQxCLohYyKKpu3I0FVLNR6E4lGlNFQZ8)

**Product traceability in supply chain is the process of tracking a product's origin and journey through the supply chain, from manufacturing to end-use. It involves logging manufacturing information in a database and following products at every step.**

[https://lh7-us.googleusercontent.com/FawjajLnI1UBkn2LJFgWqrWSTbEI-JIOzsHRG62qV42JjGK_jAON4C6WbxOF9tdWvjq9c7k4tSPcNj_JnVXsqL-AIktAI3wwUrNB1yYFQJnNcbEs0XGSuZj9sRizlzQDFEVfHGqX080zhJoduTWjkas](https://lh7-us.googleusercontent.com/FawjajLnI1UBkn2LJFgWqrWSTbEI-JIOzsHRG62qV42JjGK_jAON4C6WbxOF9tdWvjq9c7k4tSPcNj_JnVXsqL-AIktAI3wwUrNB1yYFQJnNcbEs0XGSuZj9sRizlzQDFEVfHGqX080zhJoduTWjkas)

Lack of product expertise. As it is right now, I worry they don’t have the experience or talent to build a great modern product to serve how this industry manages compliance. They claim to be Vanta for this sustainability certification niche, but I worry in practice they won’t get close to building a similar quality product to Vanta’s. However, I do think there is a good founder market fit with the CEO and this space, and if somehow paired with the right CTO, this could become a killer team.

- Beyond the idea. We want to see a first-gen product that’s delivering value.
- Product-centric opportunities, e.g. fundamentally superior product.
- PMF focus. Startup with a maniacal focus on validating product-market fit.
- Builders. The product is a core competency of the team, not an afterthought.
- True entrepreneurs. Not in it for the immediate gratification, glory, lifestyle.
- **Deep insight. Founders understand the problem better than most people in the world.**
- Blue ocean strategy. Product creates new market space rather than competing head-to-head.
- Wedgeable. Nearterm path to dominating an initial, narrow wedge of a larger market.
- Interesting IP created by solving very hard problems worth solving.
- Venture scale. The business should be raising VC to capitalize on its opportunities.
- **Scalable business model. If not initially, then very possible in the intermediate term.**
- **Durable business model. The company can survive/thrive outside of trends or economic cycles.**
- **Execution. There is evidence that the team can do the hard work.**
- Pre-A. We will work with founders to get them into a nice series A.

**Market**

- Does this match our stated [areas of interest](https://docs.google.com/document/d/1cP1mW7Vks8xOwPCO6IA4PN_Wgd6nW7_SVXbFI7PPCQ0/edit#bookmark=id.7g2mic7jbf16)?
    - If not, does the opportunity represent a new potential area of interest that we should further research?

It has the potential to be interesting. Staying compliant with many of these certifications looks like a cumbersome, manual process where software has very little penetration. If built the right way, the opportunity of building a Vanta for this type of compliance seems appealing to me.

- Do we intuitively understand and agree with the problem?

Obtaining and managing a sustainability certification is a manual, time consuming process. If it costs $200K a year to manage compliance (auditors, consultants, skilled labor, and certification) for a $20M revenue company, it looks like a relatively high cost.

- Do we agree with the company’s perspective on the market?
- Is this a blue ocean or red ocean market?
- How big is the market, both immediate and potential?

No numbers so far but relatively large. There are a lot of manufacturers that need to be certified, and for that have to manage their business.

- What are examples of successful companies that demonstrate that there is a market here?

There are no successful large scale product startups in this space.

This one seems to have failed: [https://jobs.techstars.com/companies/bioledger](https://jobs.techstars.com/companies/bioledger). They were trying to build a single source of truth for all transfers in the lifecycle of a biofuel. Not sure what they were trying to do or who this was for.

**Product traceability in supply chain is the process of tracking a product's origin and journey through the supply chain, from manufacturing to end-use. It involves logging manufacturing information in a database and following products at every step.**

[https://www.veriflux.io/](https://www.veriflux.io/). This other competitor also emphasizes the traceability aspect of this. RIMBA didn’t discuss this as much. Why?

- If not based in the US, are there distinct advantages to exploit in that geography?
- Is there a wedge approach to the market?
- Is the business model scalable to the degree that warrants venture capital?
- Is the business model durable enough to survive surprising dips in a market cycle or unexpected tailwinds?

**Team (Founders)**

1. Empathy: This entails a deep understanding of the customer's needs and the broader market pain points. It's not about superficial knowledge, but rather a profound comprehension that fuels the team's instincts and drives their decision-making process. This empathy allows them to connect with their customer base on a more intimate level, creating products and services that truly resonate.

2. Expertise: This isn't just about having domain experience—it's about possessing a level of understanding so deep that it sets the team apart from others. Their expertise should enable them to navigate complex industry challenges and uncover unique insights that can be turned into actionable strategies.

3. Execution: This is all about the nitty-gritty of operations. The team's ability to execute plans efficiently and resourcefully is key. It's not just about having a great idea—it's about being able to bring that idea to life in the most effective way possible.

4. Experimental: This quality is characterized by a willingness to build, test, learn, and iterate. It's about having an open mindset and the flexibility to adapt and evolve. A team with an experimental approach is unafraid of making mistakes—they see them as learning opportunities that can lead to improvement and innovation.

- Are the founders good at communicating the problem?
    - Did they teach us anything new?
- Do they understand this problem better than most people in the world?
    - What gives that insight or experience?
- Is this the right team to capitalize on the opportunity? Even if they have the right insight, make sure that this is the team to do it.
- Are the founders hands-on builders?
    - What have they built in the past?
- Who is responsible for difficult, technical work on the team?
- Would we describe this team as true entrepreneurs?
    - True entrepreneurs are resourceful and will survive the low points and exhausting grind of building a business. They are not in it for the immediate gratification, glory, lifestyle, or treat it as a stepping stone in their careers.

**Product**

- Is the company working on directly addressing the “problem,” or are they working adjacent to it?
- Is it clear who is the intended audience for this product?
- Is the product built and launched?
- What makes the product fundamentally superior or different from other options?
- Does the product deliver value to users/customers in its current state?
    - What are the top 2 reasons that users/customers get value from the product?
    - What are the top 2 improvements that users/customers would benefit from?
- Is there interesting technology or IP being built here?
- What are the associated costs to this product? Consider the cost of building and distributing the product.

**Traction (Momentum)**

- Do the founders believe they have validated a minimal degree of PMF?
- How do the founders view the process for figuring out PMF?
- How has this team shown that they can execute on their potential?
- What are recent inflection points that make this a good time to invest in the company?
- What are the primary drivers to their growth?

**Opportunity**

- Once they raise money, what is unlocked for the company moving forward? How does this accelerate them?
- Who are the Series A investors that we think would be interested in this company, if they hit the right milestones?

What big questions have been answered so far? Derisk. Validation/invalidation

Before solutions like Vanta, obtaining SOC2 certification was generally more manual and time-consuming. Here’s a breakdown of how it typically went:

- Understanding the Requirements: Companies had to deeply understand the SOC2 criteria, which involve detailed controls on security, availability, processing integrity, confidentiality, and privacy. This meant a lot of research and possibly hiring consultants to ensure full comprehension.
- Manual Documentation: Businesses needed to manually document all processes and controls relevant to the SOC2 standards. This often required extensive efforts from internal teams or expensive external consultants to map out processes, write policies, and prepare the required documentation.
- Implementing Controls: Implementing the necessary controls without a guiding software meant relying on internal knowledge and often bespoke solutions. This step could include configuring systems to meet security standards, establishing new protocols for data handling, and training employees on compliance-related issues.
- Evidence Gathering: Companies had to manually collect evidence proving the controls were in place and effective. This was often a labor-intensive process involving screenshots, logs, and records which needed to be meticulously organized and maintained.
- Auditor Interaction: Interactions with auditors were typically more hands-on and continuous, as companies had to demonstrate their compliance through meetings, emails, and document submissions without centralized platforms that streamline these interactions today.
- Remediation: Any gaps found during the audit process had to be addressed manually. This often meant revisiting and revising processes, which could be time-consuming.
- Continuous Compliance: Maintaining compliance was an ongoing effort without automated monitoring tools. Companies had to regularly check their controls manually to ensure they remained compliant over time.

[https://lh7-us.googleusercontent.com/3s0XBn201Pop5bzlrrUf6bKYgbnfPB7oothV4oZ3yDTRDpGehPLiieSEXSSPxDfJKq5XSQE9Ll9IBdEvjisnMmyq3z6ind5sVrRk6Q8BJtgzg0dCfcq8-QW7Ueii9kwQjseXGHZD3vMldmPW0KGzuUc](https://lh7-us.googleusercontent.com/3s0XBn201Pop5bzlrrUf6bKYgbnfPB7oothV4oZ3yDTRDpGehPLiieSEXSSPxDfJKq5XSQE9Ll9IBdEvjisnMmyq3z6ind5sVrRk6Q8BJtgzg0dCfcq8-QW7Ueii9kwQjseXGHZD3vMldmPW0KGzuUc)

SOC2 has technical requirements that need to be constantly monitored such as MFA authentication. What are some examples of things that need to be constantly monitored in the context of ISCC? What are the things that need to be shown / managed?

- MFA not on all resources, Vanta is integrated with all ur systems and identifies when that isn’t the case.

[https://lh7-us.googleusercontent.com/44z6HLPJwerBePnuowiireA7xRSgmcbaBriOxA3YzvdP4AfFrkuvk-odzbcaWMJ6stH83O3RQ1vqEfTvk4mDQcp-A6DqXpqi0GW2OBUitWMunlh2HuzLptDIKMYHSLrEsxw13APb8NXU8ISmsm2Vw1E](https://lh7-us.googleusercontent.com/44z6HLPJwerBePnuowiireA7xRSgmcbaBriOxA3YzvdP4AfFrkuvk-odzbcaWMJ6stH83O3RQ1vqEfTvk4mDQcp-A6DqXpqi0GW2OBUitWMunlh2HuzLptDIKMYHSLrEsxw13APb8NXU8ISmsm2Vw1E)

Going /against [https://www.ibm.com/products/openpages](https://www.ibm.com/products/openpages)

Yc application:

I dont like company description. “Made easy” what does it mean? What does the company do?

Why turbotax ? why not sth like Vanta

Rimba is a software company to help manage sustainability certification compliance for manufacturers, starting with the renewable fuel market

Carbon carbon accounting software has gained crazy momentum in the last few years. Notably, both Watershed and Greenly have announced growth rounds in the last 60 days:

- [Watershed raised a $100M Series C led by Greenoaks, Kleiner Perkins, and Sequoia.](https://watershed.com/blog/series-c) Company started in 2019, and [Taylor Francis](https://www.linkedin.com/in/taylor-francis-4ba49640/) is cofounder/CEO.
- [Greenly raised a $52M Series B led by Fidelity.](https://techcrunch.com/2024/03/20/greenly-series-b/?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAEX2agMhPdRlrUep16_S9-9_kjbOuQeN3kD22MoCsyLyUpE-nB4xSErT6ATXY_tY-7GuEh6OEIG-YiTnGH5jbzU5WuOkEKiOow8NWMm_UGod1Ffsk1rk3G9mL3dyfEZoNsN5VxTOf45eLfIBTdr2Xk5nqsL_oftay7aV4Nizls5I) Company started in 2019, and [Alexis Normand](https://www.linkedin.com/in/alexisnormand/) is cofounder/CEO.

Greenly:

[https://lh7-us.googleusercontent.com/VUnhQ7cq1D3xdLqQ7QFtp7iG6BJwB-YNA5LXuniKNzd1UpzYfxuSJRWGMbmTmsJsnTN15SoFvlyBe5XxT50fjPIWc7T48g_oyxe4DsfcwN7fX8N4zyW9B9cLUEIz7yrDIyPQFKY4g2-P06s20CK76WY](https://lh7-us.googleusercontent.com/VUnhQ7cq1D3xdLqQ7QFtp7iG6BJwB-YNA5LXuniKNzd1UpzYfxuSJRWGMbmTmsJsnTN15SoFvlyBe5XxT50fjPIWc7T48g_oyxe4DsfcwN7fX8N4zyW9B9cLUEIz7yrDIyPQFKY4g2-P06s20CK76WY)

Gadi: [“Plenty of major corporations have announced net-zero emissions targets. And while that alone won’t be enough to move the needle on climate change, these targets have gotten the ball rolling. Those net-zero goals are trickling down, too, influencing companies throughout the supply chain.”](https://techcrunch.com/2024/03/20/greenly-series-b/?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAEX2agMhPdRlrUep16_S9-9_kjbOuQeN3kD22MoCsyLyUpE-nB4xSErT6ATXY_tY-7GuEh6OEIG-YiTnGH5jbzU5WuOkEKiOow8NWMm_UGod1Ffsk1rk3G9mL3dyfEZoNsN5VxTOf45eLfIBTdr2Xk5nqsL_oftay7aV4Nizls5I)

Naturally, all of this trickles down into the manufacturers in markets like Asia and LatAm too, bcs if corporates care about CSRD, assuming that generates even more pressure for suppliers to care about other certifications like ISCC

Tim: Correct, companies in EU and US are mostly concerned about carbon emissions (doesn’t matter if they are manufacturing, bank or a software company). They are concerned about the mandatory disclosure they have to make about carbon emissions. That’s why companies like Greenly, sustain.life, watershed have taken-off.

A niche we noticed is that aside from carbon emissions, regulators are also starting to ask disclosure of where the raw material is coming from, social and governance aspect of these suppliers, and carbon emissions from the transportation that is involved in the supply chain until the consumer. These are captured in certifications like ISCC. This has not really taken off yet, so we still have a head start.

Gadi: I saw greenly helps corporates push certification measures to their suppliers. If this works, they could slowly onboard the complete supply chain into their platform to help trace carbon footprint. I’d be curious if they found some success with this

The question Id ask myself too is: Is it the logical next step for companies like Watershed to start adding other certificates to their platform after they win CSRD? If yes, which certificates are they likely to go after? If the market opportunity for certificates like ISCC is obviously large, what are the reasons for why they’d choose not to get into that market? Are there some key differences between these markets that would make it such that if Watershed expands, they’d start losing focus because this is a different problem/market?

Tim: Both watershed and greenly are more focused as a carbon accounting platform

[https://lh7-us.googleusercontent.com/YmWC33vb3B3-hLDtXWwMgbz6ODa7avoJ71LHPDVg_dtV03Z18dVXjzNNK-eD9iHDj5D5fYiSYyx3MajqxPSk15tS43staK2NyKsgrC3x2NhvfplB16LqNFSjdggxE8Z49YjQB_EbPrP-1wGimMZsRIM](https://lh7-us.googleusercontent.com/YmWC33vb3B3-hLDtXWwMgbz6ODa7avoJ71LHPDVg_dtV03Z18dVXjzNNK-eD9iHDj5D5fYiSYyx3MajqxPSk15tS43staK2NyKsgrC3x2NhvfplB16LqNFSjdggxE8Z49YjQB_EbPrP-1wGimMZsRIM)

Gadi: Greenly says they automate and streamline the data collection process, but they don’t show how their product works. Do you know how they do it?

Expertise: I am still struggling with this. The founders have clear domain expertise, and understand the process of ISCC extremely well. However, they fell short in painting the complete picture for his market. Perhaps initially due to my bad questions, but I later discovered Watershed/Greenly as two companies that are going after the carbon accounting software and a few certifications related to this by the EU. I had previously asked Tim for more successful competitors in the space, as I was alarmed his only references were dormant startups, so him not sharing this initially worried me.

- Does he think Watershed/Greenly are not direct competitors of Rimba? Was he trying to not mention these because they are already too large?
- Is it the logical next step for companies like Watershed to start adding other certificates to their platform after they win CSRD? If yes, which certificates are they likely to go after? If the market opportunity for certificates like ISCC is obviously large, what are the reasons for why they’d choose not to get into that market? Are there some key differences between the market Rimba is targeting versus Watershed’s such that if they expand to it, they’d start losing focus or be at a major disadvantage against Rimba?

CONVOS WITH CHATGPT

The data requirements for ISCC (International Sustainability & Carbon Certification) tend to be more granular and specific to the sustainability of biomass and bioenergy products, focusing deeply on the environmental impacts and traceability of raw materials. In contrast, the CSRD (Corporate Sustainability Reporting Directive) covers a broader range of sustainability data, encompassing environmental, social, and governance (ESG) factors applicable across all operations of a company. Here are examples of the types of data required for each:

### ISCC

1. Source and Origin of Biomass:
    - Type of Data: Specific details about the biomass source, including geographical location, type of biomass (e.g., agricultural residue, specific crops, waste materials), and the method of cultivation or collection.
    - Purpose: To ensure the biomass is produced or sourced sustainably, without contributing to deforestation or biodiversity loss, and to verify compliance with legal and sustainability criteria.
2. Greenhouse Gas (GHG) Emissions:
    - Type of Data: Detailed calculations of GHG emissions throughout the lifecycle of the bio-based product, from cultivation and harvesting of biomass to processing and transportation.
    - Purpose: To document reductions in GHG emissions compared to fossil fuel benchmarks, supporting claims of environmental benefit and compliance with sustainability goals.
3. Sustainability Practices:
    - Type of Data: Information on agricultural practices (e.g., use of pesticides, water management, soil conservation practices), labor conditions, and compliance with social standards.
    - Purpose: To ensure that the production of biomass adheres to environmental and social standards, promoting sustainable development and safeguarding worker rights.

### CSRD

1. Environmental Impact:
    - Type of Data: Broad data on energy use, water consumption, waste generation, recycling rates, and direct and indirect greenhouse gas emissions across the company.
    - Purpose: To assess the company’s environmental footprint and identify areas for improvement in resource efficiency and environmental stewardship.
2. Social and Employee Matters:
    - Type of Data: Information on employee diversity (e.g., gender, age, ethnicity), labor practices, health and safety statistics, and human rights considerations within the company and its supply chain.
    - Purpose: To promote social equity and worker welfare, ensuring that the company’s practices align with societal values and labor laws.
3. Governance Practices:
    - Type of Data: Details on the company’s governance structures and practices, such as board composition, executive compensation, anti-corruption and bribery policies, and shareholder rights.
    - Purpose: To provide transparency about how the company is managed and governed, ensuring accountability and alignment with the interests of stakeholders.

The ISCC's requirements are more focused on the specific environmental and social impacts of biomass production and use, requiring detailed tracking and reporting to ensure sustainability throughout the product lifecycle. In contrast, the CSRD requires a wider range of data, reflecting the company’s overall impact on sustainability, including governance aspects. Each type of reporting serves different purposes and targets different aspects of sustainability, with ISCC being more narrowly focused and CSRD encompassing a broader corporate perspective.

Understand workflow

What the product does

**What does their product do?**

Manufacturers have to go through thousands of docs (PDFs) every week. Docs are either (1) certificates of weight (weights of raw materials they receive), (2) contracts with their suppliers, and (3) delivery notes.

These manufacturers already track all of these for their manufacturing reports. The docs are in paper format, so they can scan them, and info is used for general ledger. If companies are not certified, they only care about the weights of each shipment, but if they are certified, they need to start tracking a lot more information such as:

- Traceability of raw materials
    - Where did they come from? Factory’s location? Overlap with deforestation areas? Labor practices?
- Track real gas emissions
    - Calculate distance, type of trucks, how long of a journey, how much weight on trucks do they carry, depending on type of truck, type of fuel they use

Docs today are manually read, scanned, and added to multiple spreadsheets that track the aforementioned stuff. With all this data, companies create a mass balance spreadsheet that tracks all their inputs, and whether they are certified or not. This dictates how much % of their sales can go into markets that require certifications.

For example, if only 30% of their input materials are certified (in blended values) because they only manage to get 30% of their supply chain as certified. Then, only 30% of their sales can go into those markets that require certification (e.g., Europe and Japan). They can cross this limit, but it’s a loan to future certified materials, so in aggregate, they can’t cross this limit. If they do, their certification gets suspended.

The mass balance helps track this, how much certified material that comes in can’t be more than the certified biofuel coming out.

Things Rimba is building to help streamline this:

1. Data Extraction and Reporting Automation:
    - Process unstructured data e.g. scanned PDF, purchase order, weight certificate, shipping documents.
    - Automates data extraction for compliance reporting; Intelligent Document Processing (IDP)
2. Material Tracking and Risk Management:
    - Trace material flows and segregate certified from non-certified materials.
    - Prevents double accounting and maintains integrity of supply chains.
3. Streamline Multiple Sustainability Certification Audit:
    - more transparency + less manual data entry + less manual calculation on excel
    - Automates cross-certification, reducing effort and duplication.

Further breakdown of requirements:

What makes them special?

How do they convince people to work this way?

Rimba is focused on X, while Watershed is focused on Y. But it does help demonstrate that there is a market here because of Z.