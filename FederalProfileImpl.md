# Status of federal profile implementation

## Links

- [Federal profile](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md)

## DCAT class mapping

### Legend

- **Init status** refer to the current state of the
  implementation [dcat-iso19139.xsl](https://github.com/geonetwork/geonetwork-microservices/blob/main/modules/services/ogc-api-records/src/main/resources/xslt/ogcapir/formats/dcat/dcat-iso19139.xsl)
  - ❌ : Not implemented / To Implement
  - 🚧 : Partially implemented
  - ✅ : Implemented / No changes
  - ⭕ : Wrongly implemented, need changes
  - ❔ : Unknown / to define / to be confirmed

### dcat:Catalog

TODO

### dcat:CatalogRecord

[Annexe document](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#a-dcat--catalog)

| name               | Init status | Current status | Comment                    |
|--------------------|-------------|----------------|----------------------------|
| dcat:CatalogRecord | ⭕           |                | Mapping must be removed    |

### dcat:Dataset

[Annexe document](https://github.com/belgif/inspire-dcat/blob/main/DCATFederalProfile.md#b-dcat--dataset)

| name                           | Init status | Current status | Comment                                                                                                                                                                                                                                                   |
|--------------------------------|-------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| @rdf:about                     | ❌           |                | Must be mapped to the resolvable URL of the metadata RDF. E.g: `<apiUrl>/collections/main/items/<uuid>`                                                                                                                                                   |
| dct:title                      | ⭕           |                | The default language is mapped two times. Issue with `<xsl:template name="LocalisedString" />`                                                                                                                                                            |
| dct:description                | ⭕           |                | The default language is mapped two times. Issue with `<xsl:template name="LocalisedString" />`                                                                                                                                                            |
| dcat:contactPoint              | ⭕           |                | Currently implemented but mapped to dcat:CatalogRecord instead of dcat:Dataset                                                                                                                                                                            |
| dcat:distribution              | 🚧          |                | See distribution section                                                                                                                                                                                                                                  |
| dcat:keyword                   | ⭕           |                | The default language is mapped two times. Issue with `<xsl:template name="LocalisedString" />`                                                                                                                                                            |
| dcat:theme                     | ❌           |                | See [Example dcat:theme](#example-dcattheme)                                                                                                                                                                                                              |
| dct:subject                    | 🚧          |                | Currently only map the subject URI without labels. See [Example dct:subject](#example-dctsubject)                                                                                                                                                         |
| dct:spatial                    | 🚧          |                | Missing the "http://www.opengis.net/ont/geosparql#geoJSONLiteral" format + The `locn:geometry` shouldn't be direct child of `dct:spatial` but insead be inside a `dct:Location` element. See https://github.com/belgif/inspire-dcat/blob/main/exemple.rdf |
| dct:temporal                   | ✅           |                |                                                                                                                                                                                                                                                           |
| dct:created                    | ✅           |                |                                                                                                                                                                                                                                                           |
| dct:modified                   | ✅           |                |                                                                                                                                                                                                                                                           |
| dct:issued                     | ✅           |                |                                                                                                                                                                                                                                                           |
| foaf:page                      | ⭕           |                | Currently mapped to both 'information' and 'search' functions but should only be 'information' + all gmd:protocol values are accepted but only 'WWW:LINK-1.0-http--link' should                                                                           |
| dct:accrualPeriodicity         | 🚧          |                | Currently only map the accrualPeriodicity URI without labels. See [Example dct:accrualPeriodicity](#example-dctaccrualPeriodicity)                                                                                                                        |
| dct:identifier                 | ⭕           |                | The namespacing using the gmd:codeSpace must be removed + the rdf:datatype attribute must be removed                                                                                                                                                      |
| dcat:landingPage               | ❌           |                | Current implementation must be fully removed + New mapping must be implemented. See [Example dcat:landingPage](#example-dcatlandingPage)                                                                                                                  |
| dct:language                   | ⭕           |                | Currently only map the first resource language and not all of them + Only map the language URI without labels. See [Example dct:language](#example-dctlanguage)                                                                                           |
| dct:provenance                 | ✅           |                |                                                                                                                                                                                                                                                           |
| dct:conformsTo                 | ❌           |                | Remove current implementation + Remove implementation of prov:wasUsedBy + Implement mapping. See [Example dataset dct:conformsTo](#example-dataset-dctconformsTo)                                                                                         |
| dct:source                     | ❌           |                | See [Example dct:source](#example-dctsource)                                                                                                                                                                                                              |
| dcat:spatialResolutionInMeters | ⭕ - ❔       |                | Remove current implementation of `<xsl:template name="SpatialResolution" />` + Implement mapping. See [Example dcat:spatialResolutionInMeters](example-dcatspatialResolutionInMeters)                                                                     |
| dqv:hasQualityMeasurement      | ❌ - ❔       |                | See [Example dcat:spatialResolutionInMeters](example-dcatspatialResolutionInMeters)                                                                                                                                                                       |
| dct:accessRights               | ⭕ - ❔       |                | Mapped xpath is currently incorrect + Constraints based on the LimitationOnPublicAccess codelist must be mapped to a thesaurus. See [Example dct:accessRights](#example-dctaccessRights)                                                                  |
| adms:sample                    | ✅ - ❔       |                |                                                                                                                                                                                                                                                           |
| dct:publisher                  |             |                |                                                                                                                                                                                                                                                           |
| geodcat:custodian              |             |                |                                                                                                                                                                                                                                                           |
| dct:creator                    |             |                |                                                                                                                                                                                                                                                           |
| geodcat:distributor            |             |                |                                                                                                                                                                                                                                                           |
| geodcat:originator             |             |                |                                                                                                                                                                                                                                                           |
| geodcat:principalInvestigator  |             |                |                                                                                                                                                                                                                                                           |
| geodcat:processor              |             |                |                                                                                                                                                                                                                                                           |
| geodcat:resourceProvider       |             |                |                                                                                                                                                                                                                                                           |
| geodcat:user                   |             |                |                                                                                                                                                                                                                                                           |
| dct:rightsHolder               |             |                |                                                                                                                                                                                                                                                           |
| dct:license                    |             |                |                                                                                                                                                                                                                                                           |
| adms:representationTechnique   |             |                |                                                                                                                                                                                                                                                           |

### dcat:Distribution

TODO

### dcat:DataService

TODO


## Examples

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

#### Example dct:subject

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

#### Example dct:accrualPeriodicity

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

### Example dcat:spatialResolutionInMeters

ISO19139:
```xml
<gmd:spatialResolution>
  <gmd:MD_Resolution>
    <gmd:distance>
      <gco:Distance uom="m">0.25</gco:Distance>
    </gmd:distance>
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
    <!-- TODO -->
  </dqv:QualityMeasurement> 
</dcat:spatialResolutionInMeters>
```

### Example dct:accessRights

**If based on LimitationsOnPublicAccess codelist:**  

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

**If not based on the LimitationsOnPublicAccess codelist:**  

ISO19139:
```xml
<gmd:resourceConstraints>
  <gmd:MD_LegalConstraints>
    <gmd:useConstraints>
      <gmd:MD_RestrictionCode codeList="http://standards.iso.org/iso/19139/resources/gmxCodelists.xml#MD_RestrictionCode"
                              codeListValue="otherRestrictions"/>
    </gmd:useConstraints>
    <gmd:otherConstraints xsi:type="gmd:PT_FreeText_PropertyType">
      <gco:CharacterString xmlns:gco="http://www.isotc211.org/2005/gco">•The custodian of the resource holds the rights of property (including the rights of intellectual property) to the geographic files
        •The custodian grants the user the right to use the data for his internal use.
        •Commercial use of the data under any form is strictly forbidden
        •Custodian’s name must be mentioned each time the data are being used publically.</gco:CharacterString>
      <gmd:PT_FreeText>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#EN">•The custodian of the resource holds the rights of property (including the rights of intellectual property) to the geographic files
            •The custodian grants the user the right to use the data for his internal use.
            •Commercial use of the data under any form is strictly forbidden
            •Custodian’s name must be mentioned each time the data are being used publically.</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#FR">•Le gestionnaire du jeu de données tel qu’il est défini plus haut possède les droits de propriété (y compris les droits de propriété intellectuelle) se rapportant aux fichiers.
            • Le gestionnaire accorde au client le droit d’utiliser les données pour son usage interne.
            • L’usage des données à des fins commerciales, sous quelque forme que ce soit, est formellement interdit.
            • Le nom du gestionnaire doit apparaître lors de chaque utilisation publique des données.</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#NL">•De beheerder van de bron bezit de eigendomsrechten (ook de rechten op de intellectuele eigendom) op de geografische bestanden
            • De beheerder geeft de klant het recht de gegevens te gebruiken voor intern gebruik
            •Het commercieel gebruik van de gegevens onder welke vorm dan ook is strikt verboden
            •De naam van de beheerder moet elke keer vermeld worden als de gegevens publiek gebruikt worden.</gmd:LocalisedCharacterString>
        </gmd:textGroup>
        <gmd:textGroup>
          <gmd:LocalisedCharacterString locale="#DE">•Der Datensatzverwalter wie höher beschrieben besitzt die Eigentumsrechte (geistiges Eigentum einbegriffen) über die Dateien.
            • Der Verwalter gewährt dem Kunden das Recht, die Daten intern zu benutzen.
            • Die Daten zu irgendwelchen kommerziellen Zwecken zu benutzen ist strikt verboten.
            • Der Name des Verwalters muss bei jeder öffentlichen Benutzung der Daten gemeldet werden.</gmd:LocalisedCharacterString>
        </gmd:textGroup>
      </gmd:PT_FreeText>
    </gmd:otherConstraints>
  </gmd:MD_LegalConstraints>
</gmd:resourceConstraints>
```

Expected GeoDCAT:
```xml
<dct:accessRights>
  <dct:RightsStatement rdf:about="<url of the xlink:href attribute if gmd:otherConstraints is gmx:Anchor and not gco:CharacterString>">
    <rdfs:label xml:lang="en">•The custodian of the resource holds the rights of property (including the rights of intellectual property) to the geographic files
      •The custodian grants the user the right to use the data for his internal use.
      •Commercial use of the data under any form is strictly forbidden
      •Custodian’s name must be mentioned each time the data are being used publically.</rdfs:label>
    <rdfs:label xml:lang="fr">•Le gestionnaire du jeu de données tel qu’il est défini plus haut possède les droits de propriété (y compris les droits de propriété intellectuelle) se rapportant aux fichiers.
      • Le gestionnaire accorde au client le droit d’utiliser les données pour son usage interne.
      • L’usage des données à des fins commerciales, sous quelque forme que ce soit, est formellement interdit.
      • Le nom du gestionnaire doit apparaître lors de chaque utilisation publique des données.</rdfs:label>
    <rdfs:label xml:lang="nl">•De beheerder van de bron bezit de eigendomsrechten (ook de rechten op de intellectuele eigendom) op de geografische bestanden
      • De beheerder geeft de klant het recht de gegevens te gebruiken voor intern gebruik
      •Het commercieel gebruik van de gegevens onder welke vorm dan ook is strikt verboden
      •De naam van de beheerder moet elke keer vermeld worden als de gegevens publiek gebruikt worden.</rdfs:label>
    <rdfs:label xml:lang="de">•Der Datensatzverwalter wie höher beschrieben besitzt die Eigentumsrechte (geistiges Eigentum einbegriffen) über die Dateien.
      • Der Verwalter gewährt dem Kunden das Recht, die Daten intern zu benutzen.
      • Die Daten zu irgendwelchen kommerziellen Zwecken zu benutzen ist strikt verboten.
      • Der Name des Verwalters muss bei jeder öffentlichen Benutzung der Daten gemeldet werden.</rdfs:label>
  </dct:RightsStatement>
</dct:accessRights>
```
