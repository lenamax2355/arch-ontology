# ARCH i2b2 PCORnet Common Data Model Ontology

The Accessible Research Commons for Health (ARCH, formerly called SCILHS) is a network of 10 health centers across the United States that covers over 8 million patients. ARCH is a Clinical Data Research Network (CDRN) in the Patient-Centered Outcomes Research Institute's PCORnet.

ARCH (with much help from others) has developed an i2b2 information model that represents the PCORnet Common Data Model (CDM). This information model consists of an i2b2 ontology/terminology and a process for mapping local data elements to the ontology without changing the underlying imported data. This approach highlights i2b2's ability to separate data model from both information model and the underlying data format.

By conforming to this ontology, ARCH sites can query across the network with an interoperable data model using SHRINE, and we provide a script to programmatically generate data marts in the PCORnet data model format. This will enable detailed analysis through the PCORnet Distributed Research Network (DRN). Likewise, if PCORNet Queries were rewritten to run against the i2b2 schema, they could run reliably at every site using the PCORNet CDM i2b2 ontology.

The ontology is live at https://www.i2b2.org/webclient/. Change the username to pcori, leave the password as demouser, and click 'Login'. The existing demo data has been mapped to the PCORI ontology, so most queries involving demographics, diagnoses, procedures, and enrollment will work. This did not require any changes to the demo data, only to the information model (ontology). Adding new demo data for the remaining sections of the ontology is on our roadmap.

This release, v4.1, represents several rounds of improvement over our initial release, and its version now corresponds to the CDM version it represents: CDM 4.1. Our CDM v3.1 ontology has been vetted by ten of our sites - the mapping has been completed and it is successfully being used for inter- and intra- network querying. The enhancements in v4.1 are labeled with a (v4) in the ontology browser, and can also be seen in this [Word document](https://github.com/ARCH-commons/arch-ontology/blob/master/Documentation/CDM%20v4.0%20Ontology%20and%20Transform%20Summary.docx). They predominantly include additional modifiers in the core structure, though we have also included PCORI's new value sets where relevant (see for example Patient Preferred Language in Demographics and Payor Type in Encouhnters).

Note that we have not implemented ontologies for the following tables: death, PRO, MED_ADMIN, provider.

- Jeffrey Klann, PhD

# About the ontology

The original core ontology was generated from Dan Connolly's code to generate ontologies from the PCORnet CDM v1 spec. We  edited this significantly based on site feedback and added some clarifications on the meaning of various elements appear in the tooltips. Since then, we have manually added to the core ontology as it has moved into its present version. We also have added many terminology trees, described below. The ontology is designed to do as much as possible out-of-the-box. By default, the ontology is mapped to relevant sections in the i2b2 metadata, and some elements are computed automatically (such as number of patients enrolled). Sites can adapt the ontology to their local data through a mapping process described in the documentation, and no changes to actual data are necessary.

## What does the ontology cover?
* Demographics, v4.1: Similar to the i2b2demodata, with a more granular age tree to support pediatric age queries.
* Diagnoses, v4.1: Includes ICD-10 2015AA and ICD-9 2014AA, generated by Lori Phillips from ontologies on BioPortal.
* Procedures, v4.1: Includes ICD-9 2015AA, ICD-10-PCS 2015AA, Partners' RPDR CMS-DRG tree, Beth Israel's MS-DRG tree (version unknown), and Nathan Wilson's HCPCS tree
* Encounters, v4.1: Includes PCORnet-specific additions, and a tree of 3-digit zip codes derived from the i2b2 demo data
* Enrollment, v3.1a: To allow sites to specify which patients have "complete longitudinal data" for selected date ranges.
* Vitals, v3.1: A simple vitals implementation including height, weight, blood pressure, and smoking status.
* Labs, v4.1: Now includes both the high-priority lab categories (70) hand-picked previously, as well as the Nebraska's NELexicon of all LOINC labs! 
  * v3.1 contained: Selected high-priority lab categories (70) and their LOINC codes, based on LOINC v236. LOINC codes suggested by PCORI in the [Lab Common Measures Guidance June 2016](https://github.com/CDMFORUM/CDM-GUIDANCE/blob/master/2016-June-1_PCORnet%20Lab%20Common%20Measures_LOINC.xlsx) are now all included.
* Medications, v4.1:  RxNorm codes organized by NDF-RT (VA Drug Class), based on RxNorm's November 2015 release

## What's not in the ontology?
* Death, death cause, and patient-reported outcomes, medication administration, and provider are not implemented.
* SNOMED Clinical Findings v1.2 are available on BioPortal, but they are not included in this version of the ontology. We suspect SNOMED is not presently used, and the language from the coordinating center indicates CPT and HCPCS are preferred over LOINC for procedures at present: "Only billed procedures should be included in the PROCEDURE table. The ORDER concept may be incorporated into future phases of the CDM." 
* CPT is not included because it is not freely available. We have an integrated CPT tree that has retired codes reconciled across sites. If you have a CPT license, you can contact us to get it.
 
# Download the ontology
Take a look at the documentation first if you like, or download the whole package:
* [Zipfile download](https://github.com/ARCH-commons/arch-ontology/releases): The [full release](https://github.com/SCILHS/scilhs-ontology/releases), including pipe-delimited exports of the ontology tables, documentation, scripts, and spreadsheets to assist in mapping. 
* [Ontology Mapping Tool for PCORnet](https://community.i2b2.org/wiki/display/NCBO/PCORI+Mapping+Tools+version+1.0): The i2b2 ontology mapping tool, modified for PCORnet (not necessary, but useful if mapping a large number of terms from local codes).
* [Ontology Mapper 1.1](https://community.i2b2.org/wiki/display/NCBO/Mapping+tools+version+1.1): The i2b2 ontology mapping tool, not modified for PCORnet, but supporting UMLS MetaMap.
* [Wiki pages](https://github.com/ARCH-commons/arch-ontology/wiki):Additional documentation on the ontology implementation process
* Enabling Patient-Centric Comparative Effectiveness Research in i2b2: A conference poster illustrating the mapping process at a high level.
* [SHRINE support files](https://open.med.harvard.edu/svn/shrine-ontology/PCORI/releases): SHRINE-formatted version of the ontology and 1:1 mapping in SHRINE  XML Adaptermapping format. 
* [PopMedNet transform](https://github.com/SCILHS/i2p-transform/): Available [at this link](https://github.com/SCILHS/i2p-transform/). Transforms an i2b2 instance mapped to this ontology into the physical CDM schema.
* [Procedures with CPT codes](https://github.com/SCILHS/ontology-private): Available if you have a CPT license, in [this repository](https://github.com/SCILHS/ontology-private). Contact us for access if you are eligible.
