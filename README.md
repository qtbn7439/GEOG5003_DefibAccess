# GEOG5003_DefibAccess
Spatial Data Science Project into relationship between Deprivation and Defibrillator Accessibility

Project Context:
Research Question: Is accessibility to defibrillators lower in more deprived areas in Salford?

According to the British Heart Foundation (2021), over 40,000 out of hospital cardiac arrest occur annually, with 10% surviving and a defibrillator being used in less than 10% cases. Lack of defibrillation reduces chances of survival by up to 10% every minute, whereas defibrillation within 3-5 minutes can produce survival rates of 50-70% (Perkins et al., 2015).

This report uses open spatial data to investigate the accessibility of defibrillators (AED) to deprivation levels using the study area of Salford, Greater Manchester. Accessibility is interpreted as either within reachable distance (200m) or freely available regardless of day, time or restrictions.

#**Data References:**

**AED Data**
Defibrillator data. (no date). [online] British Heart Foundation. Available at: https://www.bhf.org.uk/defibdata [Accessed 23 July 2026].

(This data set provides location, availability and access type data of all defibrillators with a Guardian registered on The Circuit. It does not have personal details of the Guardian.

The data has been provided in good faith by the registered Guardians, but may be inaccurate, incomplete or out of date. The file is updated on the first working day of every month. It is being shared here to support relevant organisations, such as Local Authorities or charities, in making decisions on where to place more defibrillators. It may also be used by academics or researchers in the field of out-of-hospital cardiac arrest and the community response.)

Statistics.gov.uk. (2026). ONSPD Online latest Postcode Centroids. [online] Available at: https://geoportal.statistics.gov.uk/datasets/84787e80aca04bb388caad29f89946b0_0/explore?location=53.486210%2c-2.229295%2c10 [Accessed 23 July 2026].
(This file contains the digital vector centroids for the National Statistics Postcode Directory in the UK as at May 2026.The centroids are of every live and terminated postcode in the United Kingdom.Contains both Ordnance Survey and ONS Intellectual Property Rights.&nbsp;&nbsp;REST URL of Feature Access Service – https://services1.arcgis.com/ESMARspQHYMw9BZ9/arcgis/rest/services/ONSPD_Online_latest_Postcode_Centroids/FeatureServer&nbsp;REST URL of WFS Server – https://dservices1.arcgis.com/ESMARspQHYMw9BZ9/arcgis/services/ONSPD_Online_latest_Postcode_Centroids/WFSServer?request=getcapabilities&amp;service=wfs&nbsp;REST URL of MapServer – 
https://services1.arcgis.com/ESMARspQHYMw9BZ9/arcgis/rest/services/ONSPD_Online_latest_Postcode_Centroids/MapServer)




#**Data Dictionary:**

	LSOA21CD	- Lower Super Output Area Code
    LSOA21NM	- Lower Super Output Area Name
    LAD24CD	 - Local Authority Code
    LAD24NM - Local Authority Name
    geometry	- Point, line or polygon geometry of spatial items
    PCD7	- Post code
    UNIQUE_IDENTIFIER - Defibrillator reference from database	
    ADDRESS_POST_CODE	- Post Code
    DEFIBRILLATORS_AVAILABILITY	- Whether a defirbrillator is available 24/7 or has varied access
    DEFIBRILLATORS_ACCESS_TYPE	- Whether a defibrillator's access is public or restricted
    LAT	- latitude
    LONG	- longitude
    BNG_E	- British National Grid Easting
    BNG_N	- British National Grid Northing
    Distance - Calculated distance from postcode centroid to nearest defibrillator
    IMDRank	- National level Deprivation ranking (1 = highest deprivation)
    IMDDecile	- National level Deprivation decile (1 = highest deprivation)
    Salford_IMDRank	- Standardised local level Deprivation ranking (1 = highest deprivation)
    Salford_IMDDecile	- Standardised local level Deprivation decile (1 = highest deprivation)
    index_right	- Result of join to determine if postcode centroid intersects with walking distance buffer
    covered - boolean value - True = within buffer, false = outside buffer
    count - sum of how many in and out of buffer dependent on chosen grouping (LSOA, Decile)
    decile_total_postcodes	- total number of postcodes within decile
    LSOA_total_postcodes	- Total number of postcodes within a LSOA
    percentage_covered - percentage of postcodes within a decile/LSOA which are within the 200m buffer
    Covered	- percentage of postcodes within a decile/LSOA which are within the 200m buffer
    Not Covered - percentage of postcodes within a decile/LSOA which are outside the 200m buffer
    Average_Distance	- Average distance from postcode centroid to defibrillator per LSOA
    Coverage_Check - Check field to ensure that covered and not coveraged sum to 100%    
		x_group - generalised group to create bivariate choropleth to denote accessbility (average distance or percentage_covered)
    y_group - generalised group to create bivariate choropleth to denote deprivation 
    xy_group - concated x_group and y_group to create four quadrants of bivariate matrix
		
