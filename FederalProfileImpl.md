# Status of federal profile implementation

- [Status of federal profile implementation](#status-of-federal-profile-implementation)
  - [Links](#links)
  - [DCAT class mapping](#dcat-class-mapping)
    - [Legend](#legend)
    - [dcat:Catalog](#dcatcatalog)
    - [dcat:CatalogRecord](#dcatcatalogrecord)
    - [dcat:Dataset](#dcatdataset)
    - [dcat:Distribution](#dcatdistribution)
    - [dcat:DataService](#dcatdataservice)
  - [Examples](#examples)
    - [Example vcard:Organization](#example-vcardorganization)
    - [Example dcat:theme](#example-dcattheme)
    - [Example dct:subject](#example-dctsubject)
    - [Example dct:accrualPeriodicity](#example-dctaccrualperiodicity)
    - [Example dcat:landingPage](#example-dcatlandingpage)
    - [Example dct:language](#example-dctlanguage)
    - [Example dataset dct:conformsTo](#example-dataset-dctconformsto)
    - [Example dct:source](#example-dctsource)
    - [Example dcat:spatialResolutionInMeters](#example-dcatspatialresolutioninmeters)
    - [Example dqv:hasQualityMeasurement](#example-dqvhasqualitymeasurement)
    - [Example dct:accessRights](#example-dctaccessrights)
    - [Example foaf:Organization](#example-foaforganization)
    - [Example adms:representationTechnique](#example-admsrepresentationtechnique)
    - [Example dcat:themeTaxonomy](#example-dcatthemetaxonomy)
    - [Example dcat:Distribution](#example-dcatdistribution)
    - [Example dcat:servesDataset](#example-dcatservesdataset)
    - [Example service dct:conformsTo](#example-service-dctconformsto)
    - [Example service dct:type](#example-service-dcttype)

## Links

- [Federal profile](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md)

## DCAT class mapping

### Legend

- **Init status** refer to the current state of the
  implementation [dcat-iso19139.xsl](https://github.com/geonetwork/geonetwork-microservices/blob/main/modules/services/ogc-api-records/src/main/resources/xslt/ogcapir/formats/dcat/dcat-iso19139.xsl)
  - ❌ : Not implemented / To Implement
  - 🚧 : Partially implemented
  - ✅ : Implemented / No changes needed
  - ⭕ : Wrongly implemented, need changes
  - ❔ : Unknown / to define / to be confirmed

### dcat:Catalog

[Annexe document](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#a-dcat--catalog)

| name               | Init status | Current status | Comment                                                                                                                                                    |
|--------------------|-------------|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dct:title          | ❌           |                | Must be hardcoded value                                                                                                                                    |
| dct:description    | ❌           |                | Must be hardcoded value                                                                                                                                    |
| dct:publisher      | ❌           |                | Must be hardcoded value                                                                                                                                    |
| dcat:dataset       | ❌           |                | Dataset described is this record (if dataset metadata). Dataset is currently on the ROOT level, need to be nested in dcat:Catalog                          |
| dcat:service       | ❌           |                | Service described is this record (if service metadata). Service is currently on the ROOT level, need to be nested in dcat:Catalog                          |
| foaf:homepage      | ❌           |                | Must be hardcoded value. @rdf:resource value always set to "https://www.geo.be/home"                                                                       |
| dct:language       | ❌           |                | See [Example dct:language](#example-dctlanguage) with adapted XPATH from ISO                                                                               |
| dct:issued         | ❌           |                |                                                                                                                                                            |
| dct:spatial        | ❌           |                | Replicate current implementation of dataset dct:spatial mapping                                                                                            |
| dcat:themeTaxonomy | ❌           |                | Create one dcat:themeTaxonomy for each expected dataset and service thesaurus. See [Example dcat:themeTaxonomy](#example-dcatthemeTaxonomy)                |
| dct:hasPart        | ✅           |                | No implementation needed                                                                                                                                   |
| dct:isPartOf       | ❌           |                | Must contain the URL of the full GeoDCAT export = `<micro_service_url>/collections/main/items`                                                             |
| dcat:record        | ✅           |                | No implementation needed                                                                                                                                   |
| dcat:distribution  | ❌           |                | @rdf:resource value set to XML export of the metadata. Example: https://www.geo.be/metadataServices/rest/catalogs/1/resources/{uuid}/xml                   |
| dcat:catalog       | ✅           |                | No implementation needed                                                                                                                                   |
| dcat:contactPoint  | ❌           |                | See [Example vcard:Organization](#example-vcardOrganization) with adapted XPATH from ISO and usage of `vcard:Kind` element instead of `vcard:Organization` |
| dct:identifier     | ❔           |                | Lien vers le XML. Example: https://www.geo.be/metadataServices/rest/catalogs/1/resources/{uuid}/xml                                                        |
| dcat:theme         | ❌           |                | See [Example dcat:theme](#example-dcattheme)                                                                                                               |

### dcat:CatalogRecord

[Annexe document](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#a-dcat--catalog)

| name               | Init status | Current status | Comment                    |
|--------------------|-------------|----------------|----------------------------|
| dcat:CatalogRecord | ⭕           |                | Mapping must be removed    |

### dcat:Dataset

[Annexe document](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#b-dcat--dataset)

| name                           | Init status | Current status | Comment                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------|-------------|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| @rdf:about                     | ❌           |                | Must be mapped to the resolvable URL of the metadata RDF. E.g: `<apiUrl>/collections/main/items/<uuid>`                                                                                                                                                                                                                                                                                  |
| dct:title                      | ⭕           |                | The default language is mapped two times. Issue with `<xsl:template name="LocalisedString" />`                                                                                                                                                                                                                                                                                           |
| dct:description                | ⭕           |                | The default language is mapped two times. Issue with `<xsl:template name="LocalisedString" />`                                                                                                                                                                                                                                                                                           |
| dcat:contactPoint              | ⭕           |                | Currently implemented but mapped to dcat:CatalogRecord instead of dcat:Dataset + Currently implement a logic to define what `vcard:` class must be used between `vcard:Individual`, `vcard:Organization` or `vcard:Kind`. The logic must be simplified to always use `vcard:Organization` and the mapping must be improved. See [Example vcard:Organization](#example-vcardOrganization) |
| dcat:distribution              | 🚧          |                | See [distribution section](#dcatdistribution)                                                                                                                                                                                                                                                                                                                                            |
| dcat:keyword                   | ⭕           |                | The default language is mapped two times. Issue with `<xsl:template name="LocalisedString" />`                                                                                                                                                                                                                                                                                           |
| dcat:theme                     | ❌           |                | See [Example dcat:theme](#example-dcattheme)                                                                                                                                                                                                                                                                                                                                             |
| dct:subject                    | 🚧          |                | Currently only map the subject URI without labels. See [Example dct:subject](#example-dctsubject)                                                                                                                                                                                                                                                                                        |
| dct:spatial                    | 🚧          |                | Missing the "http://www.opengis.net/ont/geosparql#geoJSONLiteral" format + The `locn:geometry` shouldn't be direct child of `dct:spatial` but instead be inside a `dct:Location` element. See https://github.com/belgif/inspire-dcat/blob/main/exemple.rdf                                                                                                                               |
| dct:temporal                   | ✅           |                |                                                                                                                                                                                                                                                                                                                                                                                          |
| dct:created                    | ✅           |                |                                                                                                                                                                                                                                                                                                                                                                                          |
| dct:modified                   | ✅           |                |                                                                                                                                                                                                                                                                                                                                                                                          |
| dct:issued                     | ✅           |                |                                                                                                                                                                                                                                                                                                                                                                                          |
| foaf:page                      | ⭕           |                | Currently mapped to both 'information' and 'search' functions but should only be 'information' + all gmd:protocol values are accepted but only 'WWW:LINK-1.0-http--link' should                                                                                                                                                                                                          |
| dct:accrualPeriodicity         | 🚧          |                | Currently only map the accrualPeriodicity URI without labels. See [Example dct:accrualPeriodicity](#example-dctaccrualPeriodicity)                                                                                                                                                                                                                                                       |
| dct:identifier                 | ⭕           |                | The namespacing using the gmd:codeSpace must be removed + the rdf:datatype attribute must be removed                                                                                                                                                                                                                                                                                     |
| dcat:landingPage               | ❌           |                | Current implementation must be fully removed + New mapping must be implemented. See [Example dcat:landingPage](#example-dcatlandingPage)                                                                                                                                                                                                                                                 |
| dct:language                   | ⭕           |                | Currently only map the first resource language and not all of them + Only map the language URI without labels. See [Example dct:language](#example-dctlanguage)                                                                                                                                                                                                                          |
| dct:provenance                 | ✅           |                |                                                                                                                                                                                                                                                                                                                                                                                          |
| dct:conformsTo                 | ❌           |                | Remove current implementation + Remove implementation of prov:wasUsedBy + Implement mapping. See [Example dataset dct:conformsTo](#example-dataset-dctconformsTo)                                                                                                                                                                                                                        |
| dct:source                     | ❌           |                | See [Example dct:source](#example-dctsource)                                                                                                                                                                                                                                                                                                                                             |
| dcat:spatialResolutionInMeters | ⭕           |                | (If raster dataset) Remove current implementation of `<xsl:template name="SpatialResolution" />` + Implement mapping. See [Example dcat:spatialResolutionInMeters](#example-dcatspatialResolutionInMeters)                                                                                                                                                                               |
| dqv:hasQualityMeasurement      | ❌           |                | (If vector dataset) See [Example dqv:hasQualityMeasurement](#example-dqvhasQualityMeasurement)                                                                                                                                                                                                                                                                                           |
| dct:accessRights               | ⭕           |                | Mapped xpath is currently incorrect, must only include constraint based on LimitationOnPublicAccess codelist + must be mapped to a thesaurus. See [Example dct:accessRights](#example-dctaccessRights)                                                                                                                                                                                   |
| adms:sample                    | ✅           |                |                                                                                                                                                                                                                                                                                                                                                                                          |
| dct:publisher                  | ⭕           |                | Currently implement a logic to define what `foaf:` class must be used between `foaf:Person`, `foaf:Organization` or `foaf:Agent`. The logic must be simplified to always use the `foaf:Organization` and the mapping improved. See [Example foaf:Organization](#example-foafOrganization)                                                                                                |
| geodcat:custodian              | ❌           |                | Reuse same logic as `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                                                                                                                                                                                          |
| dct:creator                    | ⭕           |                | Same comment as `dct:publisher`                                                                                                                                                                                                                                                                                                                                                          |
| geodcat:distributor            | ❌           |                | Reuse same logic as `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                                                                                                                                                                                          |
| geodcat:originator             | ❌           |                | Reuse same logic as `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                                                                                                                                                                                          |
| geodcat:principalInvestigator  | ❌           |                | Reuse same logic as `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                                                                                                                                                                                          |
| geodcat:processor              | ❌           |                | Reuse same logic as `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                                                                                                                                                                                          |
| geodcat:resourceProvider       | ❌           |                | Reuse same logic as `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                                                                                                                                                                                          |
| geodcat:user                   | ❌           |                | Reuse same logic as `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                                                                                                                                                                                          |
| dct:rightsHolder               | ⭕           |                | Currently mapped to role 'owner'. Must be mapped to role 'user' with a definition for `gmd:organizationName` + Same comment as `dct:publisher`                                                                                                                                                                                                                                           |
| dct:license                    | ⭕           |                | Currently, too much fields are mapped to dct:license. The XPATH must be updated                                                                                                                                                                                                                                                                                                          |
| adms:representationTechnique   | ⭕           |                | Current URL is incorrect "https://inspire.ec.europa.eu/metadata-codelist/SpatialRepresentationTypeCode" must become "https://inspire.ec.europa.eu/metadata-codelist/SpatialRepresentationType" + Currently, only the URI is mapped without the labels. See [Example adms:representationTechnique](#example-admsrepresentationTechnique)                                                  |

### dcat:Distribution

[Annexe document](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#d-dcat--distribution)

1. During conversion of a dataset (and dataset only), fetch the global atom feed described in
   the [Federal download service](https://www.geo.be/catalog/details/5cfe8a91-3dc9-4cf6-a40a-6a6d6f3124ab) using the
   XSLT `document()` function. (Atom feed
   URL: https://ac.ngi.be/remoteclient-open/GeoBePartners-open/ATOM/Atomfeed-en.xml)
2. Traverse the atom feed to search for an entry corresponding to the current dataset.
3. If one is found, fetch the dataset atom feed located in the `/feed/entry/id` element using the XSLT `document()`
   function and map it as follows

**The current implementation of the dcat:Distribution is solely based on
the `gmd:distributionInfo/gmd:MD_Distribution/gmd:transferOptions` and must be removed.**

| name                | Init status | Current status | Comment                                                                                                                     |
|---------------------|-------------|----------------|-----------------------------------------------------------------------------------------------------------------------------|
| dct:title           | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dcat:accessURL      | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dct:description     | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dct:format          | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dcat:mediaType      | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dcat:downloadURL    | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dcat:compressFormat | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dct:conformsTo      | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dcat:byteSize       | ✅           |                |                                                                                                                             |
| adms:status         | ✅           |                |                                                                                                                             |
| dct:spatial         | ⭕           |                | Reuse same logic as what is implemented for dataset dct:spatial. See [Example dcat:Distribution](#example-dcatDistribution) |
| dct:temporal        | ⭕           |                | See [Example dcat:Distribution](#example-dcatDistribution)                                                                  |
| dct:type            | ✅           |                |                                                                                                                             |

### dcat:DataService

[Annexe document](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#c-dcat--dataservice)

| name                          | Init status | Current status | Comment                                                                                                                                                                                                                    |
|-------------------------------|-------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dct:title                     | ⭕           |                | The default language is mapped two times. Issue with <xsl:template name="LocalisedString" />                                                                                                                               |
| dct:description               | ⭕           |                | The default language is mapped two times. Issue with <xsl:template name="LocalisedString" />                                                                                                                               |
| dcat:endpointURL              | ✅ - ❔       |                | Currently mapped to `gmd:transferOptions/*/gmd:onLine/*/gmd:linkage/gmd:URL` with removed query parameters.                                                                                                                |
| dcat:endpointDescription      | ⭕           |                | Need to be removed                                                                                                                                                                                                         |
| dcat:servesDataset            | ⭕           |                | Currently mapped to Dataset with dcat:CatalogRecord. Must be mapped to dataset URI. See [Example dcat:servesDataset](#example-dcatservesDataset)                                                                           |
| dct:accessRights              | ⭕           |                | Same as dataset implementation. See [Example dct:accessRights](#example-dctaccessRights)                                                                                                                                   |
| dcat:keyword                  | ⭕           |                | Same as dataset implementation.                                                                                                                                                                                            |
| dcat:theme                    | ❌           |                | Same as dataset implementation. See [Example dcat:theme](#example-dcattheme)                                                                                                                                               |
| dct:created                   | ✅           |                |                                                                                                                                                                                                                            |
| dct:modified                  | ✅           |                |                                                                                                                                                                                                                            |
| dct:issued                    | ✅           |                |                                                                                                                                                                                                                            |
| dct:conformsTo                | ⭕           |                | Currently mapped to service protocol + `gmd:DQ_DomainConsistency` + `gmd:referenceSystemInfo`. Mapping on `gmd:DQ_DomainConsistency` must be removed. See [Example service dct:conformsTo](#example-service-dctconformsTo) |
| dct:type                      | ⭕           |                | Current mapping OK but miss the skos:Concept detailed element. See [Example service dct:type](#example-service-dcttype)                                                                                                    |
| geodcat:distributor           | ❌           |                | Role "publisher" currently mapped to `dct:publisher` which is not OK for services. Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                 |
| geodcat:originator            | ❌           |                | Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                    |
| geodcat:principalInvestigator | ❌           |                | Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                    |
| geodcat:processor             | ❌           |                | Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                    |
| geodcat:resourceProvider      | ❌           |                | Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                    |
| geodcat:user                  | ❌           |                | Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                    |
| dct:creator                   | ⭕           |                | Currently mapped to role "author" which is not OK for services. Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                    |
| geodcat:custodian             | ❌           |                | Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                                                                                    |
| dct:rightsHolder              | ⭕           |                | Currently mapped to role "owner" which is not OK for services. Reuse same logic as dataset `dct:publisher`. See [Example foaf:Organization](#example-foafOrganization)                                                     |
| dct:license                   | ⭕           |                | Same as dataset implementation                                                                                                                                                                                             |

## Examples

### Example vcard:Organization

- [Annexe document: vcard:Organization](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#m-vcard-organization)
- [Annexe document: vcard:Address](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#n-vcard-address)

ISO19139:

```xml
<gmd:contact>
  <gmd:CI_ResponsibleParty gmd:CI_ResponsibleParty="http://www.isotc211.org/2005/gmd http://schemas.opengis.net/iso/19139/20060504/gmd/gmd.xsd">
    <gmd:individualName>
      <gco:CharacterString>Benoît Fricheteau</gco:CharacterString>
    </gmd:individualName>
    <gmd:organisationName gmd:organisationName="gmd:PT_FreeText_PropertyType">
      <gco:CharacterString>FPS Finance - General Administration of Patrimonial Documentation (GAPD)</gco:CharacterString>
      <gmd:PT_FreeText>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#EN">FPS Finance - General Administration of Patrimonial Documentation (GAPD)</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#FR">SPF Finances - Administration Générale de la Documentation Patrimoniale (AGDP)</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#NL">FOD Financien - Algemene Administratie van de Patrimoniumdocumentatie (AAPD)</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#DE">FOD Finanzen - Generalverwaltung Vermögensdokumentation (GVVD)</gmd:LocalisedCharacterString>
        </gmd:textGroup>
      </gmd:PT_FreeText>
    </gmd:organisationName>
    <gmd:contactInfo>
      <gmd:CI_Contact>
        <gmd:address>
          <gmd:CI_Address>
            <gmd:deliveryPoint gmd:deliveryPoint="gmd:PT_FreeText_PropertyType">
              <gco:CharacterString>Koning Albert II laan, 33 bus 50</gco:CharacterString>
              <gmd:PT_FreeText>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#EN">Koning Albert II laan, 33 bus 50</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#FR">Boulevard du Roi Albert II, 33 bte 50</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#NL">Koning Albert II laan, 33 bus 50</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#DE">Boulevard du Roi Albert II, 33 bte 50</gmd:LocalisedCharacterString>
                </gmd:textGroup>
              </gmd:PT_FreeText>
            </gmd:deliveryPoint>
            <gmd:city gmd:city="gmd:PT_FreeText_PropertyType">
              <gco:CharacterString>Schaarbeek</gco:CharacterString>
              <gmd:PT_FreeText>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#EN">Schaarbeek</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#FR">Schaerbeek</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#NL">Schaarbeek</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#DE">Schaerbeek</gmd:LocalisedCharacterString>
                </gmd:textGroup>
              </gmd:PT_FreeText>
            </gmd:city>
            <gmd:postalCode>
              <gco:CharacterString>1030</gco:CharacterString>
            </gmd:postalCode>
            <gmd:country gmd:country="gmd:PT_FreeText_PropertyType">
              <gco:CharacterString>Belgium</gco:CharacterString>
              <gmd:PT_FreeText>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#EN">Belgium</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#FR">Belgique</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#NL">België</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#DE">Belgien</gmd:LocalisedCharacterString>
                </gmd:textGroup>
              </gmd:PT_FreeText>
            </gmd:country>
            <gmd:electronicMailAddress>
              <gco:CharacterString>datadelivery@minfin.fed.be</gco:CharacterString>
            </gmd:electronicMailAddress>
          </gmd:CI_Address>
        </gmd:address>
        <gmd:onlineResource>
          <gmd:CI_OnlineResource>
            <gmd:linkage>
              <gmd:URL>https://finance.belgium.be/en/experts-partners/open-data-patrimony</gmd:URL>
            </gmd:linkage>
            <gmd:name gmd:name="gmd:PT_FreeText_PropertyType">
              <gco:CharacterString>https://finance.belgium.be/en/experts-partners/open-data-patrimony</gco:CharacterString>
              <gmd:PT_FreeText>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#EN">https://finance.belgium.be/en/experts-partners/open-data-patrimony</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#FR">https://finances.belgium.be/fr/experts_partenaires/donnees-ouvert-patrimoine</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#NL">https://financien.belgium.be/nl/experten_partners/open-patrimoniumdata</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#DE">https://finance.belgium.be/en/experts-partners/open-data-patrimony</gmd:LocalisedCharacterString>
                </gmd:textGroup>
              </gmd:PT_FreeText>
            </gmd:name>
          </gmd:CI_OnlineResource>
        </gmd:onlineResource>
      </gmd:CI_Contact>
    </gmd:contactInfo>
    <gmd:role>
      <gmd:CI_RoleCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_RoleCode" codeListValue="pointOfContact"/>
    </gmd:role>
  </gmd:CI_ResponsibleParty>
</gmd:contact>
```

Expected GeoDCAT:

```xml
<dcat:contactPoint>
  <vcard:Organization>
    <vcard:organization-name xml:lang="en">FPS Finance - General Administration of Patrimonial Documentation (GAPD)</vcard:organization-name>
    <vcard:organization-name xml:lang="fr">SPF Finances - Administration Générale de la Documentation Patrimoniale (AGDP)</vcard:organization-name>
    <vcard:organization-name xml:lang="nl">FOD Financien - Algemene Administratie van de Patrimoniumdocumentatie (AAPD)</vcard:organization-name>
    <vcard:organization-name xml:lang="de">FOD Finanzen - Generalverwaltung Vermögensdokumentation (GVVD)</vcard:organization-name>
    <vcard:hasEmail rdf:resource="datadelivery@minfin.fed.be"/>
    <vcard:hasURL rdf:resource="https://finance.belgium.be/en/experts-partners/open-data-patrimony"/>
    <vcard:hasAddress>
      <vcard:Address>
        <vcard:street-address xml:lang="en">Koning Albert II laan, 33 bus 50</vcard:street-address>
        <vcard:street-address xml:lang="fr">Boulevard du Roi Albert II, 33 bte 50</vcard:street-address>
        <vcard:street-address xml:lang="nl">Koning Albert II laan, 33 bus 50</vcard:street-address>
        <vcard:street-address xml:lang="de">Boulevard du Roi Albert II, 33 bte 50</vcard:street-address>
        <vcard:locality xml:lang="en">Schaarbeek</vcard:locality>
        <vcard:locality xml:lang="fr">Schaerbeek</vcard:locality>
        <vcard:locality xml:lang="nl">Schaarbeek</vcard:locality>
        <vcard:locality xml:lang="de">Schaerbeek</vcard:locality>
        <vcard:postal-code>1030</vcard:postal-code>
        <vcard:country-name xml:lang="en">Belgium</vcard:country-name>
        <vcard:country-name xml:lang="fr">Belgique</vcard:country-name>
        <vcard:country-name xml:lang="nl">België</vcard:country-name>
        <vcard:country-name xml:lang="de">Belgien</vcard:country-name>
      </vcard:Address>
    </vcard:hasAddress>
  </vcard:Organization>
</dcat:contactPoint>
```

---

### Example dcat:theme

For each ISO19139 gmd:keyword defined by a thesaurus, it must be mapped to a dcat:theme instead of a dcat:keyword:

Eg. ISO19319

```xml
<gmd:descriptiveKeywords>
  <gmd:MD_Keywords>
    <gmd:keyword gmd:keyword="gmd:PT_FreeText_PropertyType">
      <gmx:Anchor gmx:Anchor="http://www.eionet.europa.eu/gemet/concept/14931">sub-national boundary</gmx:Anchor>
      <gmd:PT_FreeText>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#EN">sub-national boundary</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#FR">frontière infranationale</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#NL">binnengrens</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#DE">Innerstaatliche Grenze</gmd:LocalisedCharacterString>
        </gmd:textGroup>
      </gmd:PT_FreeText>
    </gmd:keyword>
    <gmd:keyword gmd:keyword="gmd:PT_FreeText_PropertyType">
      <gmx:Anchor gmx:Anchor="http://www.eionet.europa.eu/gemet/concept/14930">national boundary</gmx:Anchor>
      <gmd:PT_FreeText>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#EN">national boundary</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#FR">frontière nationale</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#NL">landsgrens</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#DE">Staatsgrenze</gmd:LocalisedCharacterString>
        </gmd:textGroup>
      </gmd:PT_FreeText>
    </gmd:keyword>
    <gmd:type>
      <gmd:MD_KeywordTypeCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#MD_KeywordTypeCode" codeListValue="theme"/>
    </gmd:type>
    <gmd:thesaurusName>
      <gmd:CI_Citation>
        <gmd:title gmd:title="gmd:PT_FreeText_PropertyType">
          <gmx:Anchor gmx:Anchor="https://www.eionet.europa.eu/gemet/en/themes/">GEMET - Concept themes, version 4.01</gmx:Anchor>
          <gmd:PT_FreeText>
            <gmd:textGroup>
              <gmd:LocalisedCharacterString locale="#EN">GEMET - Concept themes, version 4.01</gmd:LocalisedCharacterString>
            </gmd:textGroup>
          </gmd:PT_FreeText>
        </gmd:title>
        <gmd:date>
          <gmd:CI_Date>
            <gmd:date>
              <gco:Date>2012-07-20</gco:Date>
            </gmd:date>
            <gmd:dateType>
              <gmd:CI_DateTypeCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_DateTypeCode" codeListValue="publication"/>
            </gmd:dateType>
          </gmd:CI_Date>
        </gmd:date>
        <gmd:identifier>
          <gmd:MD_Identifier>
            <gmd:code>
              <gmx:Anchor gmx:Anchor="http://csw.geo.be/eng/thesaurus.download?ref=external.theme.gemet">geonetwork.thesaurus.external.theme.gemet</gmx:Anchor>
            </gmd:code>
          </gmd:MD_Identifier>
        </gmd:identifier>
      </gmd:CI_Citation>
    </gmd:thesaurusName>
  </gmd:MD_Keywords>
</gmd:descriptiveKeywords>
```

GeoDCAT

```xml
<dcat:Dataset>
  <!-- ... -->
  <dcat:theme>
    <skos:Concept rdf:about="http://www.eionet.europa.eu/gemet/concept/14931">
      <skos:prefLabel xml:lang="en">sub-national boundary</skos:prefLabel>
      <skos:prefLabel xml:lang="fr">frontière infranationale</skos:prefLabel>
      <skos:prefLabel xml:lang="nl">binnengrens</skos:prefLabel>
      <skos:prefLabel xml:lang="de">Innerstaatliche Grenze</skos:prefLabel>
      <skos:inScheme rdf:resource="https://www.eionet.europa.eu/gemet/en/themes"/>
    </skos:Concept>
  </dcat:theme>
  <dcat:theme>
    <skos:Concept rdf:about="http://www.eionet.europa.eu/gemet/concept/14930">
      <skos:prefLabel xml:lang="en">national boundary</skos:prefLabel>
      <skos:prefLabel xml:lang="fr">frontière nationale</skos:prefLabel>
      <skos:prefLabel xml:lang="nl">landsgrens</skos:prefLabel>
      <skos:prefLabel xml:lang="de">Staatsgrenze</skos:prefLabel>
      <skos:inScheme rdf:resource="https://www.eionet.europa.eu/gemet/en/themes"/>
    </skos:Concept>
  </dcat:theme>
  <!-- ... -->
</dcat:Dataset>
```

---

### Example dct:subject

ISO19139:

```xml
<gmd:topicCategory>
  <gmd:MD_TopicCategoryCode>planningCadastre</gmd:MD_TopicCategoryCode>
</gmd:topicCategory>
```

Actual GeoDCAT result:

```xml
<dct:subject rdf:resource="http://inspire.ec.europa.eu/metadata-codelist/TopicCategory/planningCadastre"/>
```

Expected result:

```xml
<dct:subject>
  <skos:Concept rdf:about="http://inspire.ec.europa.eu/metadata-codelist/TopicCategory/planningCadastre">
    <skos:prefLabel xml:lang="en">Planning / Cadastre</skos:prefLabel>
    <skos:prefLabel xml:lang="fr">Planification/Cadastre</skos:prefLabel>
    <skos:prefLabel xml:lang="nl">Planning/kadaster</skos:prefLabel>
    <skos:prefLabel xml:lang="de">Planungsunterlagen/Kataster</skos:prefLabel>
    <skos:inScheme rdf:resource="http://inspire.ec.europa.eu/metadata-codelist/TopicCategory"/>
  </skos:Concept>
</dct:subject>
```

See https://inspire.ec.europa.eu/metadata-codelist/TopicCategory/ for complete list of possible values with labels:

- EN: https://inspire.ec.europa.eu/metadata-codelist/TopicCategory/TopicCategory.en.rdf
- FR: https://inspire.ec.europa.eu/metadata-codelist/TopicCategory/TopicCategory.fr.rdf
- NL: https://inspire.ec.europa.eu/metadata-codelist/TopicCategory/TopicCategory.nl.rdf
- DE: https://inspire.ec.europa.eu/metadata-codelist/TopicCategory/TopicCategory.de.rdf

---

### Example dct:accrualPeriodicity

ISO19139:

```xml
<gmd:resourceMaintenance>
  <gmd:MD_MaintenanceInformation>
    <gmd:maintenanceAndUpdateFrequency>
      <gmd:MD_MaintenanceFrequencyCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#MD_MaintenanceFrequencyCode" codeListValue="annually"/>
    </gmd:maintenanceAndUpdateFrequency>
  </gmd:MD_MaintenanceInformation>
</gmd:resourceMaintenance>
```

Actual GeoDCAT:

```xml
<dct:accrualPeriodicity rdf:resource="http://publications.europa.eu/resource/authority/frequency/ANNUAL"/>
```

Expected GeoDCAT:

````xml
<dct:accrualPeriodicity>
  <skos:Concept rdf:about="http://publications.europa.eu/resource/authority/frequency/ANNUAL">
    <skos:prefLabel xml:lang="en">annual</skos:prefLabel>
    <skos:prefLabel xml:lang="fr">annuel</skos:prefLabel>
    <skos:prefLabel xml:lang="nl">jaarlijks</skos:prefLabel>
    <skos:prefLabel xml:lang="de">jährlich</skos:prefLabel>
    <skos:inScheme rdf:resource="http://publications.europa.eu/resource/authority/frequency"/>
  </skos:Concept>
</dct:accrualPeriodicity>
````

See http://publications.europa.eu/resource/authority/frequency for list of labels.

---

### Example dcat:landingPage

ISO19139:

```xml
<gmd:fileIdentifier>
  <gco:CharacterString>629ad470-71dc-11eb-af47-3448ed25ad7c</gco:CharacterString>
</gmd:fileIdentifier>
```

Expected GeoDCAT:

```xml
<dcat:landingPage rdf:resource="https://www.geo.be/catalog/details/629ad470-71dc-11eb-af47-3448ed25ad7c"/>
```

---

### Example dct:language

ISO19139:

```xml
<gmd:identificationInfo>
  <gmd:MD_DataIdentification>
    <!-- ... -->
    <gmd:language>
      <gmd:LanguageCode codeList="http://www.loc.gov/standards/iso639-2/" codeListValue="eng"/>
    </gmd:language>
    <gmd:language>
      <gmd:LanguageCode codeList="http://www.loc.gov/standards/iso639-2/" codeListValue="ger"/>
    </gmd:language>
    <gmd:language>
      <gmd:LanguageCode codeList="http://www.loc.gov/standards/iso639-2/" codeListValue="fre"/>
    </gmd:language>
    <gmd:language>
      <gmd:LanguageCode codeList="http://www.loc.gov/standards/iso639-2/" codeListValue="dut"/>
    </gmd:language>
    <!-- ... -->
  </gmd:MD_DataIdentification>
</gmd:identificationInfo>
```

Actual GeoDCAT:

```xml
<dct:language rdf:resource="http://publications.europa.eu/resource/authority/language/ENG"/>
```

Expected GeoDCAT:

```xml
<dcat:Dataset>
  <!-- ... -->
  <dct:language>
    <skos:Concept rdf:about="http://publications.europa.eu/resource/authority/language/ENG">
      <skos:prefLabel xml:lang="en">English</skos:prefLabel>
      <skos:prefLabel xml:lang="fr">anglais</skos:prefLabel>
      <skos:prefLabel xml:lang="nl">Engels</skos:prefLabel>
      <skos:prefLabel xml:lang="de">Englisch</skos:prefLabel>
      <skos:inScheme rdf:resource="https://publications.europa.eu/resource/authority/language"/>
    </skos:Concept>
  </dct:language>
  <dct:language>
    <skos:Concept rdf:about="https://publications.europa.eu/resource/authority/language/DEU">
      <skos:prefLabel xml:lang="en">German</skos:prefLabel>
      <skos:prefLabel xml:lang="fr">allemand</skos:prefLabel>
      <skos:prefLabel xml:lang="nl">Duits</skos:prefLabel>
      <skos:prefLabel xml:lang="de">Deutsch</skos:prefLabel>
      <skos:inScheme rdf:resource="https://publications.europa.eu/resource/authority/language"/>
    </skos:Concept>
  </dct:language>
  <dct:language>
    <skos:Concept rdf:about="https://publications.europa.eu/resource/authority/language/FRA">
      <skos:prefLabel xml:lang="en">French</skos:prefLabel>
      <skos:prefLabel xml:lang="fr">français</skos:prefLabel>
      <skos:prefLabel xml:lang="nl">Frans</skos:prefLabel>
      <skos:prefLabel xml:lang="de">Französisch</skos:prefLabel>
      <skos:inScheme rdf:resource="https://publications.europa.eu/resource/authority/language"/>
    </skos:Concept>
  </dct:language>
  <dct:language>
    <skos:Concept rdf:about="http://publications.europa.eu/resource/authority/language/NLD">
      <skos:prefLabel xml:lang="en">Dutch</skos:prefLabel>
      <skos:prefLabel xml:lang="fr">néerlandais</skos:prefLabel>
      <skos:prefLabel xml:lang="nl">Nederlands</skos:prefLabel>
      <skos:prefLabel xml:lang="de">Niederländisch</skos:prefLabel>
      <skos:inScheme rdf:resource="https://publications.europa.eu/resource/authority/language"/>
    </skos:Concept>
  </dct:language>
  <!-- ... -->
</dcat:Dataset>
```

See http://publications.europa.eu/resource/authority/language for URL and labels.

---

### Example dataset dct:conformsTo

ISO19139:

```xml
<gmd:result>
  <gmd:DQ_ConformanceResult>
    <gmd:specification>
      <gmd:CI_Citation>
        <gmd:title gmd:title="gmd:PT_FreeText_PropertyType">
          <gmx:Anchor gmx:Anchor="http://data.europa.eu/eli/reg/2010/1089">COMMISSION REGULATION (EU) No 1089/2010 of 23 November 2010 implementing Directive 2007/2/EC of the European Parliament and of the Council as regards interoperability of spatial data sets and services</gmx:Anchor>
          <gmd:PT_FreeText>
            <gmd:textGroup>
              <gmd:LocalisedCharacterString locale="#EN">COMMISSION REGULATION (EU) No 1089/2010 of 23 November 2010 implementing Directive 2007/2/EC of the European Parliament and of the Council as regards interoperability of spatial data sets and services</gmd:LocalisedCharacterString>
            </gmd:textGroup>
            <gmd:textGroup>
              <gmd:LocalisedCharacterString locale="#FR">Règlement (UE) N° 1089/2010 de la Commission du 23 novembre 2010 portant modalités d'application de la directive 2007/2/CE du Parlement européen et du Conseil en ce qui concerne l'interopérabilité des séries et des services de données géographiques</gmd:LocalisedCharacterString>
            </gmd:textGroup>
            <gmd:textGroup>
              <gmd:LocalisedCharacterString locale="#NL">Verordening (EU) n r. 1089/2010 van de Commissie van 23 november 2010 ter uitvoering van Richtlijn 2007/2/EG van het Europees Parlement en de Raad betreffende de interoperabiliteit van verzamelingen ruimtelijke gegevens en van diensten met betrekking tot ruimtelijke gegevens</gmd:LocalisedCharacterString>
            </gmd:textGroup>
            <gmd:textGroup>
              <gmd:LocalisedCharacterString locale="#DE">Verordnung (EG) Nr. 1089/2010 der Kommission vom 23. November 2010 zur Durchführung der Richtlinie 2007/2/EG des Europäischen Parlaments und des Rates hinsichtlich der Interoperabilität von Geodatensätzen und -diensten</gmd:LocalisedCharacterString>
            </gmd:textGroup>
          </gmd:PT_FreeText>
        </gmd:title>
        <gmd:date>
          <gmd:CI_Date>
            <gmd:date>
              <gco:Date>2010-12-08</gco:Date>
            </gmd:date>
            <gmd:dateType>
              <gmd:CI_DateTypeCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_DateTypeCode" codeListValue="publication"/>
            </gmd:dateType>
          </gmd:CI_Date>
        </gmd:date>
      </gmd:CI_Citation>
    </gmd:specification>
    <!-- ... -->
  </gmd:DQ_ConformanceResult>
</gmd:result>
```

Expected GeoDCAT result:

```xml
<dct:conformsTo>
  <dct:Standard rdf:about="http://data.europa.eu/eli/reg/2010/1089">
    <dct:title xml:lang="en">COMMISSION REGULATION (EU) No 1089/2010 of 23 November 2010 implementing Directive 2007/2/EC of the European Parliament and of the Council as regards interoperability of spatial data sets and services</dct:title>
    <dct:title xml:lang="fr">Règlement (UE) N° 1089/2010 de la Commission du 23 novembre 2010 portant modalités d'application de la directive 2007/2/CE du Parlement européen et du Conseil en ce qui concerne l'interopérabilité des séries et des services de données géographiques</dct:title>
    <dct:title xml:lang="nl">Verordening (EU) n r. 1089/2010 van de Commissie van 23 november 2010 ter uitvoering van Richtlijn 2007/2/EG van het Europees Parlement en de Raad betreffende de interoperabiliteit van verzamelingen ruimtelijke gegevens en van diensten met betrekking tot ruimtelijke gegevens</dct:title>
    <dct:title xml:lang="de">Verordnung (EG) Nr. 1089/2010 der Kommission vom 23. November 2010 zur Durchführung der Richtlinie 2007/2/EG des Europäischen Parlaments und des Rates hinsichtlich der Interoperabilität von Geodatensätzen und -diensten</dct:title>
    <dct:issued>2010-12-08</dct:issued>
  </dct:Standard>
</dct:conformsTo>
```

---

### Example dct:source

ISO19139:

```xml
<gmd:aggregationInfo>
  <gmd:MD_AggregateInformation>
    <gmd:aggregateDataSetIdentifier>
      <gmd:MD_Identifier>
        <gmd:code>
          <gco:CharacterString>fb1e2993-2020-428c-9188-eb5f75e284b9</gco:CharacterString>
        </gmd:code>
      </gmd:MD_Identifier>
    </gmd:aggregateDataSetIdentifier>
    <gmd:associationType>
      <gmd:DS_AssociationTypeCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#DS_AssociationTypeCode" codeListValue="geometricFeatures" />
    </gmd:associationType>
  </gmd:MD_AggregateInformation>
</gmd:aggregationInfo>
```

Expected GeoDCAT:

```xml
<dct:source rdf:resource="<apiUrl>/collections/main/items/fb1e2993-2020-428c-9188-eb5f75e284b9" />
```

---

### Example dcat:spatialResolutionInMeters

ISO19139:

```xml
<gmd:spatialResolution>
  <gmd:MD_Resolution>
    <gmd:distance>
      <gco:Distance uom="m">0.25</gco:Distance>
    </gmd:distance>
    <gmd:equivalentScale>
      <gmd:MD_RepresentativeFraction>
        <gmd:denominator>
          <gco:Integer>10000</gco:Integer>
        </gmd:denominator>
      </gmd:MD_RepresentativeFraction>
    </gmd:equivalentScale>
  </gmd:MD_Resolution>
</gmd:spatialResolution>
```

Actual GeoDCAT:
```xml
<dcat:spatialResolutionInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">0.25</dcat:spatialResolutionInMeters>
```

Expected GeoDCAT:

```xml
<dcat:spatialResolutionInMeters>
  <dqv:QualityMeasurement>
    <sdmx-attribut:unitMeasure>
      <skos:Concept rdf:about="http://qudt.org/vocab/unit/M">
        <skos:prefLabel xml:lang="en">Meter</skos:prefLabel>
        <skos:inScheme rdf:resource="http://qudt.org/vocab/unit/"/>
      </skos:Concept>
    </sdmx-attribut:unitMeasure>
    <dqv:value>0.25</dqv:value>
  </dqv:QualityMeasurement>
</dcat:spatialResolutionInMeters>
```

---

### Example dqv:hasQualityMeasurement

ISO19139:

```xml
<gmd:spatialResolution>
  <gmd:MD_Resolution>
    <gmd:distance>
      <gco:Distance uom="m">0.25</gco:Distance>
    </gmd:distance>
    <gmd:equivalentScale>
      <gmd:MD_RepresentativeFraction>
        <gmd:denominator>
          <gco:Integer>10000</gco:Integer>
        </gmd:denominator>
      </gmd:MD_RepresentativeFraction>
    </gmd:equivalentScale>
  </gmd:MD_Resolution>
</gmd:spatialResolution>
```

Actual GeoDCAT:
```xml
<dcat:spatialResolutionInMeters rdf:datatype="http://www.w3.org/2001/XMLSchema#decimal">0.25</dcat:spatialResolutionInMeters>
```

Expected GeoDCAT:

```xml
<dqv:hasQualityMeasurement>
  <dqv:QualityMeasurement>
    <geodcat:spatialResolutionAsScale>10000</geodcat:spatialResolutionAsScale>
  </dqv:QualityMeasurement>
</dqv:hasQualityMeasurement>
```

---

### Example dct:accessRights

ISO19139:

```xml
<gmd:resourceConstraints gmd:resourceConstraints="http://www.isotc211.org/2005/srv http://schemas.opengis.net/iso/19139/20060504/srv/srv.xsd">
  <gmd:MD_LegalConstraints>
    <gmd:accessConstraints>
      <gmd:MD_RestrictionCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#MD_RestrictionCode" codeListValue="otherRestrictions"/>
    </gmd:accessConstraints>
    <gmd:otherConstraints gmd:otherConstraints="gmd:PT_FreeText_PropertyType">
      <gmx:Anchor gmx:Anchor="http://inspire.ec.europa.eu/metadata-codelist/LimitationsOnPublicAccess/noLimitations">No limitations on public access</gmx:Anchor>
      <gmd:PT_FreeText>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#EN">No limitations on public access</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#FR">Pas de restrictions concernant l'accès public</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#NL">Geen beperkingen op openbare toegang</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#DE">Öffentliche Zugang nicht beschränkt</gmd:LocalisedCharacterString>
        </gmd:textGroup>
      </gmd:PT_FreeText>
    </gmd:otherConstraints>
  </gmd:MD_LegalConstraints>
</gmd:resourceConstraints>
```

Expected GeoDCAT:

```xml
<dct:accessRights>
  <skos:Concept rdf:about="http://publications.europa.eu/resource/authority/access-right/PUBLIC">
    <skos:prefLabel xml:lang="en">public</skos:prefLabel>
    <skos:prefLabel xml:lang="fr">public</skos:prefLabel>
    <skos:prefLabel xml:lang="nl">openbaar</skos:prefLabel>
    <skos:prefLabel xml:lang="de">öffentlich</skos:prefLabel>
    <skos:inScheme rdf:resource="http://publications.europa.eu/resource/authority/access-right"/>
  </skos:Concept>
</dct:accessRights>
```

See http://publications.europa.eu/resource/authority/access-right for values and labels

---

### Example foaf:Organization

[Annexe document: foaf:Organization](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#e-foaf-organization)  
[Annexe document: locn:Address](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#g-locn-address)  

ISO19139:
```xml
<gmd:pointOfContact>
  <gmd:CI_ResponsibleParty gmd:CI_ResponsibleParty="http://www.isotc211.org/2005/gmd http://schemas.opengis.net/iso/19139/20060504/gmd/gmd.xsd">
    <gmd:individualName>
      <gco:CharacterString>Benoît Fricheteau</gco:CharacterString>
    </gmd:individualName>
    <gmd:organisationName gmd:organisationName="gmd:PT_FreeText_PropertyType">
      <gco:CharacterString>FPS Finance - General Administration of Patrimonial Documentation (GAPD)</gco:CharacterString>
      <gmd:PT_FreeText>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#EN">FPS Finance - General Administration of Patrimonial Documentation (GAPD)</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#FR">SPF Finances - Administration Générale de la Documentation Patrimoniale (AGDP)</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#NL">FOD Financien - Algemene Administratie van de Patrimoniumdocumentatie (AAPD)</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#DE">FOD Finanzen - Generalverwaltung Vermögensdokumentation (GVVD)</gmd:LocalisedCharacterString>
        </gmd:textGroup>
      </gmd:PT_FreeText>
    </gmd:organisationName>
    <gmd:contactInfo>
      <gmd:CI_Contact>
        <gmd:address>
          <gmd:CI_Address>
            <gmd:deliveryPoint gmd:deliveryPoint="gmd:PT_FreeText_PropertyType">
              <gco:CharacterString>Koning Albert II laan, 33 bus 50</gco:CharacterString>
              <gmd:PT_FreeText>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#EN">Koning Albert II laan, 33 bus 50</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#FR">Boulevard du Roi Albert II, 33 bte 50</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#NL">Koning Albert II laan, 33 bus 50</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#DE">Boulevard du Roi Albert II, 33 bte 50</gmd:LocalisedCharacterString>
                </gmd:textGroup>
              </gmd:PT_FreeText>
            </gmd:deliveryPoint>
            <gmd:city gmd:city="gmd:PT_FreeText_PropertyType">
              <gco:CharacterString>Schaarbeek</gco:CharacterString>
              <gmd:PT_FreeText>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#EN">Schaarbeek</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#FR">Schaerbeek</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#NL">Schaarbeek</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#DE">Schaerbeek</gmd:LocalisedCharacterString>
                </gmd:textGroup>
              </gmd:PT_FreeText>
            </gmd:city>
            <gmd:postalCode>
              <gco:CharacterString>1030</gco:CharacterString>
            </gmd:postalCode>
            <gmd:country gmd:country="gmd:PT_FreeText_PropertyType">
              <gco:CharacterString>Belgium</gco:CharacterString>
              <gmd:PT_FreeText>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#EN">Belgium</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#FR">Belgique</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#NL">België</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#DE">Belgien</gmd:LocalisedCharacterString>
                </gmd:textGroup>
              </gmd:PT_FreeText>
            </gmd:country>
            <gmd:electronicMailAddress>
              <gco:CharacterString>datadelivery@minfin.fed.be</gco:CharacterString>
            </gmd:electronicMailAddress>
          </gmd:CI_Address>
        </gmd:address>
        <gmd:onlineResource>
          <gmd:CI_OnlineResource>
            <gmd:linkage>
              <gmd:URL>https://finance.belgium.be/en/experts-partners/open-data-patrimony</gmd:URL>
            </gmd:linkage>
            <gmd:name gmd:name="gmd:PT_FreeText_PropertyType">
              <gco:CharacterString>https://finance.belgium.be/en/experts-partners/open-data-patrimony</gco:CharacterString>
              <gmd:PT_FreeText>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#EN">https://finance.belgium.be/en/experts-partners/open-data-patrimony</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#FR">https://finances.belgium.be/fr/experts_partenaires/donnees-ouvert-patrimoine</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#NL">https://financien.belgium.be/nl/experten_partners/open-patrimoniumdata</gmd:LocalisedCharacterString>
                </gmd:textGroup>
                <gmd:textGroup>
                  <gmd:LocalisedCharacterString locale="#DE">https://finance.belgium.be/en/experts-partners/open-data-patrimony</gmd:LocalisedCharacterString>
                </gmd:textGroup>
              </gmd:PT_FreeText>
            </gmd:name>
          </gmd:CI_OnlineResource>
        </gmd:onlineResource>
      </gmd:CI_Contact>
    </gmd:contactInfo>
    <gmd:role>
      <gmd:CI_RoleCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#CI_RoleCode" codeListValue="publisher"/>
    </gmd:role>
  </gmd:CI_ResponsibleParty>
</gmd:pointOfContact>
```

Expected GeoDCAT:

```xml
<dct:publisher>
  <foaf:Organization>
    <foaf:name xml:lang="en">FPS Finance - General Administration of Patrimonial Documentation (GAPD)</foaf:name>
    <foaf:name xml:lang="fr">SPF Finances - Administration Générale de la Documentation Patrimoniale (AGDP)</foaf:name>
    <foaf:name xml:lang="nl">FOD Financien - Algemene Administratie van de Patrimoniumdocumentatie (AAPD)</foaf:name>
    <foaf:name xml:lang="de">FOD Finanzen - Generalverwaltung Vermögensdokumentation (GVVD)</foaf:name>
    <foaf:mbox rdf:resource="datadelivery@minfin.fed.be"/>
    <foaf:workplaceHomepage rdf:resource="https://finance.belgium.be/en/experts-partners/open-data-patrimony"/>
    <locn:address>
      <locn:Address>
        <locn:thoroughfare xml:lang="en">Koning Albert II laan, 33 bus 50</locn:thoroughfare>
        <locn:thoroughfare xml:lang="fr">Boulevard du Roi Albert II, 33 bte 50</locn:thoroughfare>
        <locn:thoroughfare xml:lang="nl">Koning Albert II laan, 33 bus 50</locn:thoroughfare>
        <locn:thoroughfare xml:lang="de">Boulevard du Roi Albert II, 33 bte 50</locn:thoroughfare>
        <locn:postName xml:lang="en">Schaarbeek</locn:postName>
        <locn:postName xml:lang="fr">Schaerbeek</locn:postName>
        <locn:postName xml:lang="nl">Schaarbeek</locn:postName>
        <locn:postName xml:lang="de">Schaerbeek</locn:postName>
        <locn:postCode>1030</locn:postCode>
        <locn:adminUnitL1 xml:lang="en">Belgium</locn:adminUnitL1>
        <locn:adminUnitL1 xml:lang="fr">Belgique</locn:adminUnitL1>
        <locn:adminUnitL1 xml:lang="nl">België</locn:adminUnitL1>
        <locn:adminUnitL1 xml:lang="de">Belgien</locn:adminUnitL1>
      </locn:Address>
    </locn:address>
  </foaf:Organization>
</dct:publisher>
```

---

### Example adms:representationTechnique

ISO19139:

```xml
<gmd:spatialRepresentationType>
  <gmd:MD_SpatialRepresentationTypeCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#MD_SpatialRepresentationTypeCode" codeListValue="vector"/>
</gmd:spatialRepresentationType>
```

Actual GeoDCAT:

```xml
<adms:representationTechnique rdf:resource="http://inspire.ec.europa.eu/metadata-codelist/SpatialRepresentationTypeCode/vector"/>
```

Expected GeoDCAT:

```xml
<adms:representationTechnique>
  <skos:Concept rdf:about="http://inspire.ec.europa.eu/metadata-codelist/SpatialRepresentationType/vector">
    <skos:prefLabel xml:lang="en">Vector</skos:prefLabel>
    <skos:inScheme rdf:resource="http://inspire.ec.europa.eu/metadata-codelist/SpatialRepresentationType"/>
  </skos:Concept>
</adms:representationTechnique>
```

See https://inspire.ec.europa.eu/metadata-codelist/SpatialRepresentationType for complete list of possible values with
labels:

- EN: https://inspire.ec.europa.eu/metadata-codelist/SpatialRepresentationType/SpatialRepresentationType.en.rdf

### Example dcat:themeTaxonomy

Example of expected thesaurus in DCAT:

```xml
<dcat:Dataset>
  <!-- ... -->
  <dct:language>
    <skos:Concept rdf:about="http://publications.europa.eu/resource/authority/language/ENG">
      <skos:prefLabel xml:lang="en">English</skos:prefLabel>
      <skos:prefLabel xml:lang="fr">anglais</skos:prefLabel>
      <skos:prefLabel xml:lang="nl">Engels</skos:prefLabel>
      <skos:prefLabel xml:lang="de">Englisch</skos:prefLabel>
      <skos:inScheme rdf:resource="https://publications.europa.eu/resource/authority/language"/>
    </skos:Concept>
  </dct:language>
  <!-- ... -->
  <dct:accessRights>
    <skos:Concept rdf:about="http://publications.europa.eu/resource/authority/access-right/PUBLIC">
      <skos:prefLabel xml:lang="en">public</skos:prefLabel>
      <skos:prefLabel xml:lang="fr">public</skos:prefLabel>
      <skos:prefLabel xml:lang="nl">openbaar</skos:prefLabel>
      <skos:prefLabel xml:lang="de">öffentlich</skos:prefLabel>
      <skos:inScheme rdf:resource="http://publications.europa.eu/resource/authority/access-right"/>
    </skos:Concept>
  </dct:accessRights>
  <!-- ... -->
</dcat:Dataset>
```

Expected GeoDCAT:

```xml
<dcat:Catalog>
  <!-- ... -->
  <dcat:themeTaxonomy>
    <skos:ConceptScheme rdf:about="https://publications.europa.eu/resource/authority/language">
      <dct:title xml:lang="en">Language</dct:title>
      <dct:identifier>http://publications.europa.eu/resource/authority/language</dct:identifier>
    </skos:ConceptScheme>
  </dcat:themeTaxonomy>
  <dcat:themeTaxonomy>
    <skos:ConceptScheme rdf:about="http://publications.europa.eu/resource/authority/access-right">
      <dct:title xml:lang="en">Access righ</dct:title>
      <dct:issued>2016-07-21</dct:issued>
      <dct:identifier>http://publications.europa.eu/resource/authority/access-right</dct:identifier>
    </skos:ConceptScheme>
  </dcat:themeTaxonomy>
  <!-- ... -->
</dcat:Catalog>
```

**Remarks:**

- For the implementation, keep as much local version of thesauri as possible and use these versions for the mapping
- In case we don't have a local version, fallback on querying the URL as an attempt to gather the information
- If the query returns an HTML, skip this `dcat:themeTaxonomy`

### Example dcat:Distribution

Dataset atom feed:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<feed xmlns="http://www.w3.org/2005/Atom" xmlns:georss="http://www.georss.org/georss" xml:lang="en">
  <title>SUVIM station network</title>
  <subtitle>The Solar Ultraviolet - Visible Irradiance Monitoring network (SUVIM) is formed of observation stations operated by the Royal Belgian Institute for Space Aeronomy (IASB-BIRA)</subtitle>
  <logo>https://www.geo.be/thumbs/uv-station-suvim.jpg</logo>
  <link href="http://publish.geo.be/geonetwork/srv/api/records/59129f4b-a61b-467c-9b41-1f92e4338151/attachments/Atomfeed-en.xml" rel="self" hreflang="en" title="feed containing the pre-defined dataset"/>
  <link href="http://publish.geo.be/geonetwork/srv/api/records/5cfe8a91-3dc9-4cf6-a40a-6a6d6f3124ab/attachments/Atomfeed-en.xml" rel="up" type="application/xml"/>
  <id>http://publish.geo.be/geonetwork/srv/api/records/59129f4b-a61b-467c-9b41-1f92e4338151/attachments/Atomfeed-en.xml</id>
  <rights>Copyright (c) 2020, NGI Belgium; all rights reserved</rights>
  <updated>2021-12-13T13:28:05Z</updated>
  <author>
    <name>Royal Belgian Institute for Space Aeronomy (IASB-BIRA)</name>
    <email>david.bolsee@aeronomie.be</email>
  </author>
  <entry>
    <title>SUVIM station network (EPSG code for projection system: EPSG:4326 - Distribution format: Esri Shapefile)</title>
    <id>https://ac.ngi.be/remoteclient-open/GeoBePartners-open/BIRA-IASB/59129f4b-a61b-467c-9b41-1f92e4338151_x-shapefile_4326.zip</id>
    <link href="https://ac.ngi.be/remoteclient-open/GeoBePartners-open/BIRA-IASB/59129f4b-a61b-467c-9b41-1f92e4338151_x-shapefile_4326.zip" type="application/x-shapefile" rel="alternate" hreflang="en"/>
    <rights>Copyright (c) 2020, NGI Belgium; all rights reserved</rights>
    <updated>2021-12-13T13:28:05Z</updated>
    <category term="http://www.opengis.net/def/crs/EPSG/0/EPSG:4326" label="EPSG code for projection system: EPSG:4326"/>
    <georss:box>49.33 2.54 51.50 6.65</georss:box>
  </entry>
</feed>
```

Expected GeoDCAT:

```xml
<dcat:distribution>
  <dcat:Distribution>
    <dct:title xml:lang="en">SUVIM station network</dct:title>
    <dcat:accessURL rdf:resource="https://ac.ngi.be/remoteclient-open/GeoBePartners-open/BIRA-IASB/59129f4b-a61b-467c-9b41-1f92e4338151_x-shapefile_4326.zip"/>
    <dct:description>The Solar Ultraviolet - Visible Irradiance Monitoring network (SUVIM) is formed of observation stations operated by the Royal Belgian Institute for Space Aeronomy (IASB-BIRA)</dct:description>
    <!-- 1-1 mapping must be defined with https://publications.europa.eu/resource/authority/file-type codelist  -->
    <dct:format rdf:resource="https://publications.europa.eu/resource/authority/file-type/SHP"/>
    <!-- 1-1 mapping must be defined with https://www.iana.org/assignments/media-types/media-types.xhtml codelist  -->
    <dcat:mediaType rdf:resource="https://www.iana.org/assignments/media-types/application/vnd.shp"/>
    <dcat:downloadURL rdf:resource="https://ac.ngi.be/remoteclient-open/GeoBePartners-open/BIRA-IASB/59129f4b-a61b-467c-9b41-1f92e4338151_x-shapefile_4326.zip"/>
    <dcat:compressFormat rdf:resource="https://www.iana.org/assignments/media-types/application/vnd.shp"/>
    <dct:conformsTo rdf:resource="http://www.opengis.net/def/crs/EPSG/0/4326"/>
    <dct:spatial>
      <dct:Location>
        <locn:geometry rdf:datatype="http://www.opengis.net/ont/geosparql#wktLiteral"><![CDATA[POLYGON((2.54 51.50,6.65 51.50,6.65 49.33,2.54 49.33,2.54 51.50))]]></locn:geometry>
        <locn:geometry rdf:datatype="http://www.opengis.net/ont/geosparql#gmlLiteral"><![CDATA[<gml:Envelope srsName="http://www.opengis.net/def/crs/OGC/1.3/CRS84"><gml:lowerCorner>2.54 49.33</gml:lowerCorner><gml:upperCorner>6.65 51.50</gml:upperCorner></gml:Envelope>]]></locn:geometry>
        <locn:geometry rdf:datatype="https://www.iana.org/assignments/media-types/application/vnd.geo+json"><![CDATA[{"type":"Polygon","crs":{"type":"name","properties":{"name":"urn:ogc:def:crs:OGC:1.3:CRS84"}},"coordinates":[[[2.54,51.50],[6.65,51.50],[6.65,49.33],[2.54,49.33],[2.54,51.50]]]}]]></locn:geometry>
        <dcat:bbox rdf:datatype="http://www.opengis.net/ont/geosparql#wktLiteral"><![CDATA[POLYGON((2.54 51.50,6.65 51.50,6.65 49.33,2.54 49.33,2.54 51.50))]]></dcat:bbox>
        <dcat:bbox rdf:datatype="http://www.opengis.net/ont/geosparql#gmlLiteral"><![CDATA[<gml:Envelope srsName="http://www.opengis.net/def/crs/OGC/1.3/CRS84"><gml:lowerCorner>2.54 49.33</gml:lowerCorner><gml:upperCorner>6.65 51.50</gml:upperCorner></gml:Envelope>]]></dcat:bbox>
        <dcat:bbox rdf:datatype="https://www.iana.org/assignments/media-types/application/vnd.geo+json"><![CDATA[{"type":"Polygon","crs":{"type":"name","properties":{"name":"urn:ogc:def:crs:OGC:1.3:CRS84"}},"coordinates":[[[2.54,51.50],[6.65,51.50],[6.65,49.33],[2.54,49.33],[2.54,51.50]]]}]]></dcat:bbox>
      </dct:Location>
    </dct:spatial>
    <!-- <dct:temporal /> -->
  </dcat:Distribution>
</dcat:distribution>
```

**Note:** each `/feed/entry` must be mapped to its own `dcat:distribution` element.

---

### Example dcat:servesDataset

In ISO19139:

```xml
<srv:operatesOn uuidref="067c8ccb-50fa-4918-9f6b-6b1248b3bef3"
                xlink:href="http://csw.geo.be/eng/csw?service=CSW&amp;request=GetRecordById&amp;version=2.0.2&amp;outputSchema=http://www.isotc211.org/2005/gmd&amp;elementSetName=full&amp;id=067c8ccb-50fa-4918-9f6b-6b1248b3bef3"/>
```

Actual GeoDCAT:

```xml
<dcat:servesDataset rdf:parseType="Resource">
   <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#string">067c8ccb-50fa-4918-9f6b-6b1248b3bef3</dct:identifier>
   <foaf:isPrimaryTopicOf>
      <dcat:CatalogRecord rdf:about="http://csw.geo.be/eng/csw?service=CSW&amp;request=GetRecordById&amp;version=2.0.2&amp;outputSchema=http://www.isotc211.org/2005/gmd&amp;elementSetName=full&amp;id=067c8ccb-50fa-4918-9f6b-6b1248b3bef3"/>
   </foaf:isPrimaryTopicOf>
</dcat:servesDataset>
```

**Note:** Some other cases are implemented but not shown here. All cases can be changed to the new implementation.

Expected GeoDCAT:

```xml
<dcat:servesDataset rdf:resource="<apiUrl>/collections/main/items/067c8ccb-50fa-4918-9f6b-6b1248b3bef3" />
```

---

### Example service dct:conformsTo

In ISO19139:

```xml
<gmd:MD_Metadata>
  <!-- ... -->
  <gmd:referenceSystemInfo>
    <gmd:MD_ReferenceSystem>
      <gmd:referenceSystemIdentifier>
        <gmd:RS_Identifier>
          <gmd:code>
            <gco:CharacterString>31370</gco:CharacterString>
          </gmd:code>
        </gmd:RS_Identifier>
      </gmd:referenceSystemIdentifier>
    </gmd:MD_ReferenceSystem>
  </gmd:referenceSystemInfo>
  <gmd:referenceSystemInfo>
    <gmd:MD_ReferenceSystem>
      <gmd:referenceSystemIdentifier>
        <gmd:RS_Identifier>
          <gmd:code>
            <gco:CharacterString>3812</gco:CharacterString>
          </gmd:code>
        </gmd:RS_Identifier>
      </gmd:referenceSystemIdentifier>
    </gmd:MD_ReferenceSystem>
  </gmd:referenceSystemInfo>

  <gmd:distributionInfo>
    <gmd:MD_Distribution>
      <gmd:transferOptions>
        <gmd:MD_DigitalTransferOptions>
          <gmd:onLine>
            <gmd:CI_OnlineResource>
              <gmd:linkage>
                <gmd:URL>https://wms.ngi.be/inspire23/utility/wms?service=wms&amp;version=1.3.0&amp;request=GetCapabilities</gmd:URL>
              </gmd:linkage>
              <gmd:protocol>
                <gco:CharacterString>OGC:WMS</gco:CharacterString>
              </gmd:protocol>
              <!-- ... -->
            </gmd:CI_OnlineResource>
          </gmd:onLine>
        </gmd:MD_DigitalTransferOptions>
      </gmd:transferOptions>
    </gmd:MD_Distribution>
  </gmd:distributionInfo>
  <!-- ... -->
</gmd:MD_Metadata>
```

Actual GeoDCAT:

```xml
<dcat:DataService>
  <!-- ... -->
  <dct:conformsTo rdf:parseType="Resource">
    <rdf:type rdf:resource="http://purl.org/dc/terms/Standard"/>
    <rdf:type rdf:resource="http://www.w3.org/2004/02/skos/core#Concept"/>
    <dct:type rdf:resource="http://inspire.ec.europa.eu/glossary/SpatialReferenceSystem"/>
    <dct:title xml:lang="en">31370</dct:title>
  </dct:conformsTo>
  <dct:conformsTo rdf:parseType="Resource">
    <rdf:type rdf:resource="http://purl.org/dc/terms/Standard"/>
    <rdf:type rdf:resource="http://www.w3.org/2004/02/skos/core#Concept"/>
    <dct:type rdf:resource="http://inspire.ec.europa.eu/glossary/SpatialReferenceSystem"/>
    <dct:title xml:lang="en">3812</dct:title>
  </dct:conformsTo>

  <dct:conformsTo rdf:resource="http://www.opengeospatial.org/standards/wms"/>
  <!-- ... -->
</dcat:DataService>
```

Expected GeoDCAt:

```xml
<dcat:DataService>
  <!-- ... -->
  <dct:conformsTo rdf:resource="http://www.opengis.net/def/crs/EPSG/0/31370" />
  <dct:conformsTo rdf:resource="http://www.opengis.net/def/crs/EPSG/0/3812" />
  <dct:conformsTo rdf:resource="http://www.opengis.net/def/serviceType/ogc/wms"/>
  <!-- ... -->
</dcat:DataService>
```

List of protocol values: https://inspire.ec.europa.eu/metadata-codelist/ProtocolValue

---

### Example service dct:type

Actual ISO19139:

```xml
<srv:serviceType>
  <gco:LocalName>view</gco:LocalName>
</srv:serviceType>
```

Actual GeoDCAT:

```xml
<dct:type rdf:resource="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType/view"/>
```

Expected GeoDCAT:

```xml
<dct:type>
  <skos:Concept rdf:about="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType/view">
    <skos:prefLabel xml:lang="en">View Service</skos:prefLabel>
    <skos:prefLabel xml:lang="nl">Raadpleegdienst</skos:prefLabel>
    <skos:prefLabel xml:lang="fr">Service de consultation</skos:prefLabel>
    <skos:prefLabel xml:lang="de">Darstellungsdienste</skos:prefLabel>
    <skos:inScheme rdf:resource="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType"/>
  </skos:Concept>
</dct:type>
```

See http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceType for list of labels.

---
